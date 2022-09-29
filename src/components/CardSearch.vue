<template>
  <div>
    <v-card-text class="py-0">
      <v-chip v-for="(keyword, i) in keywords" :key="i" class="mr-2">
        {{ keyword }}
      </v-chip>
    </v-card-text>

    <v-list three-line>
      <v-list-item
        v-for="(item, i) in searching"
        :key="i"
        ripple
        @click="() => {}"
      >
        <v-img
          :src="item.image"
          class="mr-4"
          max-width="64"
          min-width="64"
        ></v-img>

        <v-list-item-content>
          <span
            class="text-uppercase font-weight-regular text-caption"
            v-text="item.category"
          ></span>

          <div v-text="item.title"></div>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </div>
</template>

<script>
export default {
  data: () => ({}),
  props: ["post"],
};
</script>