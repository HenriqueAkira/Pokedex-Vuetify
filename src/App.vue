<template>
  <v-app>
    <v-main>
      <router-view/>
    </v-main>

    <Navbar/>
  </v-app>
</template>

<script>

import Navbar from "./components/Navbar.vue"

export default {
  name: 'App',

  components: {Navbar},

  data: () => ({
    //
  }),
};
</script>
