<template>
  <v-app>
    <v-main>
      <Cd_Cards> </Cd_Cards>
    </v-main>
  </v-app>
</template>

<script>

// eslint-disable-next-line camelcase
import Cd_Cards from '../components/cd_cards.vue';

export default {
  name: 'Home',

  components: {
    Cd_Cards,
  },
};
</script>
