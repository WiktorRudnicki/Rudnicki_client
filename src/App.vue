<template>
  <v-app>
    <v-main>
      <appbar></appbar>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

import appbar from './components/appbar.vue';

export default {
  name: 'App',

  data: () => ({
    //
  }),
  components: {
    appbar,
  },
};
</script>
