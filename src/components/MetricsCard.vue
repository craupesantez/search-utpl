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
      <v-list-item ripple @click="() => {}" :href="post.url">
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
      <v-col cols="2">
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5"> Autores </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h2" cols="5"> {{ post.authors.length }} </v-col>
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

      <v-col cols="2">
        <v-card max-width="300">
          <v-list-item two-line>
            <v-list-item-title class="text-h5"> Lectores en Mendeley </v-list-item-title>
          </v-list-item>
          <v-card-text>
            <v-row>
              <v-col class="text-h4" cols="5"> {{ post.readers.mendeley }} </v-col>
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
    urlIcons:"https://www.google.com/imgres?imgurl=https%3A%2F%2Flookaside.fbsbx.com%2Flookaside%2Fcrawler%2Fmedia%2F%3Fmedia_id%3D100039870145061&imgrefurl=https%3A%2F%2Fwww.facebook.com%2FAltmetric%2F&tbnid=31_1Zr_j_5lrQM&vet=12ahUKEwjfwZ3kma77AhXixykDHbdJDywQMygFegUIARCxAQ..i&docid=GXIMgSLJ_rjIgM&w=625&h=625&q=almetrics%20icons&ved=2ahUKEwjfwZ3kma77AhXixykDHbdJDywQMygFegUIARCxAQ",
  }),
  props: ["post"],
  created: function () {
    // `this` points to the vm instance
    this.last_updated = moment(this.post.last_updated).format('YYYY-MM-DD');
  }
};
</script> 