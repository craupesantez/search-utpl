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
  <v-card-text class="py-2">
    <!-- <a href=""> -->
    <v-list-item ripple @click="() => {}" :href="post.link">
      <v-img
        :src="post.pagemap.cse_image[0].src"
        class="mr-4"
        max-width="110"
        min-width="110"
      ></v-img>
      <v-list-item-content>
        <span
          class="text-uppercase font-weight-regular text-caption"
          v-text="post.title">
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
  </v-card-text>
</template>
<script>
export default {
  data: () => ({}),
  props: ["post"],
};
</script>