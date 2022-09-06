<template>
  <v-app>

    <Navbar/>

    <v-main>
      <router-view/>
    </v-main>

    <BottomNavbar class="d-sm-none"/>
  </v-app>
</template>

<script>

import BottomNavbar from "./components/BottomNavbar.vue"
import Navbar from "./components/Navbar.vue"

export default {
  name: 'App',

  components: {BottomNavbar, Navbar},

  data: () => ({
    //
  }),
};
</script>
