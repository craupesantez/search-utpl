<template>
  <v-card class="mx-auto mt-1">
    <v-system-bar></v-system-bar>
    <v-row>
      <v-col cols="10">
        <v-toolbar flat color="transparent">
          <v-btn icon type="button" v-on:click="doSearch()">
            <v-icon>mdi-arrow-left</v-icon>
          </v-btn>
          <v-text-field
            v-model="q"
            type="text"
            append-icon="mdi-magnify"
            :label="`ingrese el ${select.state}`"
            single-line
          ></v-text-field>
        </v-toolbar>
      </v-col>
      <v-col cols="2">
        <v-select
          v-model="select"
          :hint="`${select.state}, ${select.abbr}`"
          :items="items"
          item-text="state"
          item-value="abbr"
          label="Select"
          persistent-hint
          return-object
          single-line
        ></v-select>
      </v-col>
    </v-row>

    <v-card-text class="py-0">
      <MetricsCard v-bind:post="searchResult"></MetricsCard>
    </v-card-text>
    <v-carousel
      cycle
      height="200"
      hide-delimiter-background
      show-arrows-on-hover
    >
      <v-carousel-item v-for="(citation, i) in citations" :key="i">
        <v-sheet :color="colors[i]" height="100%">
          <v-row class="fill-height" align="center" justify="center">
            <v-col cols="1">
              <v-img
                :src="citation.images.small"
                alt="Sunny image"
                width="92"
              ></v-img>
            </v-col>
            <v-col cols="5">
              <a :href="citation.url">
                <div class="text-h5">{{ citation.title }}</div>
              </a>
            </v-col>
            
          </v-row>
        </v-sheet>
      </v-carousel-item>
    </v-carousel>
    <div class="text-center">
      <v-pagination
        v-model="page"
        :length="4"
        circle
        v-show="visiblePagination"
      ></v-pagination>
    </div>
  </v-card>
</template>

<script>
import axios from "axios";
import _ from "lodash";
import MetricsCard from "../components/MetricsCard.vue";
export default {
  components: {
    MetricsCard,
  },
  data: (vm) => ({
    q: "",
    searchResult: "",
    citations: "",
    dataAPImetrics: "",
    page: 1,
    start: 1,
    pageBefore: 1,
    enableMetricsCard: false,
    visiblePagination: false,
    colors: ["white"],
    slides: [
      { title: "First" },
      { title: "Second" },
      { title: "Third" },
      { title: "Fourth" },
      { title: "Fifth" },
    ],
    select: { state: "DOI", abbr: "doi" },
    items: [
      { state: "DOI", abbr: "doi" },
      { state: "ISBN", abbr: "isbn" },
      { state: "arXiv ID", abbr: "arxiv" },
      { state: "PubMed ID", abbr: "pmid" },
    ],
    key: "AIzaSyD8xMPy8gXY1OPi_9Hiwl1Kv76sirXNnhs",
    //doi:'',
    //cx:"3493648eba43943a2",
    //api:"https://www.googleapis.com/customsearch/v1"
    //api: "https://api.altmetric.com/v1/doi/",
    api: "https://api.altmetric.com/v1/",
    apiCitations: "citations/1d",
  }),
  watch: {
    q: function () {
      console.log(this.q);
      this.visiblePagination = true;
      this.debouncedDoSearch();
      if (this.q.length == 0) {
        this.searchResult = "";
        this.visiblePagination = false;
        this.page = 1;
        this.pageBefore = 1;
      }
    },
    page: function () {
      if (this.pageBefore < this.page) {
        this.start = this.start + 10;
        this.pageBefore = this.page;
      } else {
        this.start = this.start - 10;
        this.pageBefore = this.page;
      }
      console.log("valor de start", this.start);
      this.doSearch();
    },
  },
  created: function () {
    // _.debounce is a function provided by lodash to limit how
    // often a particularly expensive operation can be run.
    // In this case, we want to limit how often we access
    // yesno.wtf/api, waiting until the user has completely
    // finished typing before making the ajax request. To learn
    // more about the _.debounce function (and its cousin
    // _.throttle), visit: https://lodash.com/docs#debounce

    this.debouncedDoSearch = _.debounce(this.doSearch, 5000);
    this.getCitations();
  },
  methods: {
    doSearch: async function () {
      try {
        var app = this;
        await axios
          .get(
            //`${this.api}?key=${this.key}&cx=${this.cx}&start=${this.start}&q=${this.q}`
            `${this.api}${this.select.abbr}/${this.q}`
          )
          .then((response) => {
            app.searchResult = response.data;
            console.log("ruta de busqueda", this.api + this.select.abbr + "/");
            console.log("para buscar el error", response);

            console.log("Resultado: ", app.searchResult);
          });
      } catch (error) {
        this.searchResult = null;
        console.log("mensaje de error ", error.message);
      }
    },
    getCitations: async function () {
      try {
        var app = this;
        await axios.get(`${this.api}${this.apiCitations}`).then((response) => {
          app.dataAPImetrics = response.data;
          console.log("get data altmetrics ", app.dataAPImetrics);
          if (app.dataAPImetrics !== null) {
            app.citations = app.dataAPImetrics.results;
            console.log("citations ", app.citations);
          }
        });
      } catch (error) {
        this.dataAPImetrics = null;
        console.log("Error en API Altmetrics ", error.message);
      }
    },
  },
};
</script>