<template>
  <!-- <div>
          <div>
              <a href="">
                  <img :src="post.pagemap.cse_image[0].src">
              </a>
              <div>
                  <h5>
                      <a :href="post.link">{{ post.title }}></a>
                  </h5>
              </div>
          </div>
      </div> -->

  <v-container fluid>
    <v-card-text class="py-2">
      <!-- <a href=""> -->
      <v-list-item ripple @click="() => {}" :href="post.url" v-if="post.hasOwnProperty('url')">
        <v-img
          :src="post.images.small"
          class="mr-4"
          max-width="110"
          min-width="110"
        ></v-img>
        <v-list-item-content>
          <span
            class="text-uppercase font-weight-regular text-caption"
            v-text="post.title"
          >
          </span>
          <div v-text="post.title"></div>
        </v-list-item-content>

        <!-- </a> -->
        <!-- <div>
        <h5>
          <a :href="post.link">{{ post.title }}></a>
        </h5>
      </div> -->
      </v-list-item>
      <v-list-item ripple @click="() => {}" :href="post.details_url">
        <v-img
          :src="urlIcons"
          class="mr-4"
          max-width="110"
          min-width="110"
        ></v-img>
        <v-list-item-content>
          <span
            class="text-uppercase font-weight-regular text-caption"
            v-text="altmetric"
          >
          </span>
          <div v-text="altmetric"></div>
        </v-list-item-content>
      </v-list-item>
    </v-card-text>
    <v-row dense>
      <v-col cols="2" v-show="post.hasOwnProperty('authors')">
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5"> Autores </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h2" cols="5" v-if="post.hasOwnProperty('authors')"> {{ post.authors.length }} </v-col>
              <v-col cols="5">
                <v-img
                  src="https://cdn.icon-icons.com/icons2/2358/PNG/512/fabrication_fake_news_author_unethical_icon_143313.png"
                  alt="Sunny image"
                  width="92"
                ></v-img>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>
        </v-card>
      </v-col>
      <v-col cols="2">
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5"> Ultima Actualización </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h7" cols="5"> {{ last_updated }} </v-col>
              <v-col cols="5">
                <v-img
                  src="https://cdn.icon-icons.com/icons2/2560/PNG/512/calendar_alert_notification_date_appointment_icon_153130.png"
                  alt="Sunny image"
                  width="92"
                ></v-img>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>
        </v-card>
      </v-col>

      <v-col cols="2">
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5"> Citas de twitter </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h4" cols="5"> {{ post.cited_by_tweeters_count }} </v-col>
              <v-col cols="5">
                <v-img
                  src="https://cdn.icon-icons.com/icons2/122/PNG/512/twitter_socialnetwork_20007.png"
                  alt="Sunny image"
                  width="92"
                ></v-img>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>
        </v-card>
      </v-col>

      <v-col cols="2" >
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5" > Lectores en Mendeley </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h4" cols="5"> {{ post.readers.mendeley }} </v-col>
              <v-col cols="5">
                <v-img
                  src="https://cdn.icon-icons.com/icons2/1381/PNG/512/mendeleydesktop_93629.png"
                  alt="Sunny image"
                  width="92"
                ></v-img>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>
        </v-card>
      </v-col>

      <v-col cols="2">
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5"> Tipo </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h5" cols="5"> {{ post.type }} </v-col>
              <v-col cols="5">
                <v-img
                  src="https://cdn.icon-icons.com/icons2/34/PNG/256/documentediting_editdocuments_text_documentedi_2820.png"
                  alt="Sunny image"
                  width="92"
                ></v-img>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
  <script>
  import moment from 'moment';
export default {
  data: () => ({
    postTwitter: "Post Twitter ",
    altmetric: "Metricas  en sitio Altmetrics",
    last_updated:'',
    urlIcons:'https://cdn.icon-icons.com/icons2/1852/PNG/512/iconfinder-browserwindowwithstats-4417108_116626.png',
  }),
  props: ["post"],
  created: function () {
    // `this` points to the vm instance
    this.last_updated = moment(this.post.last_updated).format('YYYY-MM-DD');
  }
};
</script> 