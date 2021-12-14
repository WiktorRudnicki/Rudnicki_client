<template>
  <v-app>
    <v-main>
      <div>
        <v-img />
        <h2>{{ title }}</h2>
        <v-btn @click="buyalb()">Purchase </v-btn>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    album: [],
    songs: [],
  }),
  async created() {
    const response = await axios.get('http://localhost:3000/shop/');
    this.album = response.data;
    const res = await axios.get("'http://localhost:3000/shop/songs/' + this.album.id");
    this.songs = res.data;
  },
  methods: {
    async purchase() {
      if (this.album.stueckzahl > 0) {
        await axios.get("'http://localhost:3000/shop/' + this.album.id");
        window.location.reload();
      } else {
        await axios.delete("'http://localhost:3000/shop/' + this.album.id");
        this.$router.push({ name: 'Home', url: 'http://localhost:8080' });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
