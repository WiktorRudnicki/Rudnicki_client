<template>
  <v-app>
    <v-row class="d-flex flex-wrap justify-center">
      <v-card
        v-for="(alb, id) in this.album"
        :key="id"
        style="width: 300px"
        class="ma-3 d-flex flex-column padding: 10px"
      >
        <v-img :src="'http://localhost:3000/images/' + alb.pic"></v-img>
        <h1>
          {{ alb.titel }}
        </h1>
        <br />
        <span>Artist: {{ alb.artist }}</span>
        <br />
        <span> Typ: {{ alb.typ }} </span>
        <span> Preis: {{ alb.preis }} Euro </span>
        <span> Rating: {{ alb.rating }} </span>
        <v-rating
          color="warning"
          empty-icon="mdi-star-outline"
          full-icon="mdi-star"
          hover
          length="5"
          size="36"
          :value="alb.rating"
          ></v-rating>
        <br />
        <span>Anzahl: {{ alb.stueckzahl }}</span>
        <br />
        <v-btn :to="'/Details/' + alb.id" style="width: 100px">
          Details
        </v-btn>
      </v-card>
    </v-row>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    album: [],
  }),
  async created() {
    const response = await axios.get('http://localhost:3000/shop');
    this.album = response.data;
  },
};
</script>
