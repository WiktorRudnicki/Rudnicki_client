<template>
  <v-app>
    <v-main>
      <div class="d-flex flex-columm">
        <div :class="ms-3">
          <v-img
            :src="'http://localhost:3000/images/' + al.pic"
            max-width="300"
            max-height="300"
          ></v-img>
          <h1>
            {{ al.titel }}
          </h1>
          <br />
          <span>Artist: {{ al.artist }}</span>
          <br />
          <span> Typ: {{ al.typ }} </span>
          <span> Preis: {{ al.preis }} Euro </span>
          <span> Rating: {{ al.rating }} </span>
          <v-rating
            color="warning"
            empty-icon="mdi-star-outline"
            full-icon="mdi-star"
            hover
            length="5"
            size="36"
            :value="al.rating"
          ></v-rating>
          <br />
          <span>Anzahl: {{ al.stueckzahl }}</span>
          <v-btn @click="buyalb()" :to="'/Details/' + al.id">Purchase </v-btn>
        </div>
        <div>
          <span v-for="(song, id) in songs"
          :key="id"> Titel: {{ song.titel }} Länge {{ song.laenge}} <br><br></span>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    songs: [],
    album: [],
    headers: {
      text: 'Titel',
      align: 'start',
    },
  }),
  props: {
    id: {
      type: String,
    },
  },
  computed: {
    al() {
      return this.album.find((el) => el.id == this.id);
    },
  },
  async created() {
    const response = await axios.get('http://localhost:3000/shop');
    this.album = response.data;
    console.log(this.album);
    const res = await axios.get(`http://localhost:3000/shop/song/${this.al.id}`);
    this.songs = res.data;
  },
  methods: {
    async buyalb() {
      if (this.al.stueckzahl == 1) {
        await axios.delete(`http://localhost:3000/shop/${this.al.id}`);
        this.$router.push({ name: 'Home', url: 'http://localhost:8080' });
      } else {
        await axios.patch(`http://localhost:3000/shop/${this.al.id}`);
        this.$router.push({ name: 'Home', url: 'http://localhost:8080' });
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
