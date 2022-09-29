<template>
  <v-app>
    <Navbar></Navbar>
    <v-main class="ma-4">
      <!-- <div>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link> |
        <router-link to="/search">Search</router-link> |
        <router-link to="/search-veutify">Search-Veutify</router-link>
      </div> -->
      <router-view> </router-view>
      
    </v-main>
  </v-app>
</template>

<script>

import Navbar from "./components/Navbar.vue";
export default {
  name: "App",
  components:{
    Navbar,
},
  data: () => ({
    //
  }),
};
</script>
