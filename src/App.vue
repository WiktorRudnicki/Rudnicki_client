<template>
  <v-app>
    <v-main>
      <appbar></appbar>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';
import appbar from './components/appbar.vue';

export default {
  name: 'App',
  data: () => ({
    album: [],
  }),
  async created() {
    const response = await axios.get('http://localhost:3000/shop');
    this.album = response.data;
    console.log(this.album);
  },
  components: {
    appbar,
  },
};
</script>
