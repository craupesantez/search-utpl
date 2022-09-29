<template>
  <v-card class="mx-auto mt-1">
    <v-system-bar></v-system-bar>
    <v-toolbar flat color="transparent">
        <v-btn icon type="button" v-on:click="doSearch()">
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
      <v-text-field
        v-model="q"
        type="text"
        append-icon="mdi-magnify"
        label="buscador website"
        single-line
      ></v-text-field>

    </v-toolbar>
    <v-card-text class="py-0">
        <PostCard v-for="post in searchResult.items"
            v-bind:post="post"></PostCard>
    </v-card-text>
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
import _ from 'lodash';
import PostCard from "../components/PostCard.vue";
export default {
  components: {
    PostCard,
  },
  data: (vm) => ({
    q: "",
    searchResult: "",
    page: 1,
    start:1,
    pageBefore:1,
    visiblePagination: false,
    key:"AIzaSyD8xMPy8gXY1OPi_9Hiwl1Kv76sirXNnhs",
    cx:"3493648eba43943a2",
    api:"https://www.googleapis.com/customsearch/v1"
  }),
  watch: {
    q: function () {
      console.log(this.q);
      this.visiblePagination = true;
      this.debouncedDoSearch();
      if(this.q.length==0){
        this.searchResult = "";
        this.visiblePagination = false;
        this.page = 1;
        this.pageBefore = 1;
      }
    },
    page: function () {
      if(this.pageBefore < this.page){
        this.start = this.start + 10; 
        this.pageBefore = this.page;
      }else{
        this.start = this.start - 10; 
        this.pageBefore = this.page;
      }  
      console.log("valor de start",this.start);
      this.doSearch();
    }
  },
  created: function () {
    // _.debounce is a function provided by lodash to limit how
    // often a particularly expensive operation can be run.
    // In this case, we want to limit how often we access
    // yesno.wtf/api, waiting until the user has completely
    // finished typing before making the ajax request. To learn
    // more about the _.debounce function (and its cousin
    // _.throttle), visit: https://lodash.com/docs#debounce
    this.debouncedDoSearch = _.debounce(this.doSearch, 500);
  },
  methods: {
    doSearch: async function () {
      try {
        var app = this;
        await axios
        .get(
          `${this.api}?key=${this.key}&cx=${this.cx}&start=${this.start}&q=${this.q}`
        )
        .then( (response)=> {
          app.searchResult = response.data;

          console.log("Resultado: " ,app.searchResult);
        })
      } catch (error) {
        console.log(error.message);
      }
      
        
    },
  },
};
</script>