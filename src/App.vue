<template>
  <v-app>
    <v-app-bar app color="yellow darken-2" dark>
      <h1>Matching Game</h1>
    </v-app-bar>

    <v-main>
      <matching-game />
    </v-main>
  </v-app>
</template>

<script>
import MatchingGame from './components/MatchingGame.vue';

export default {
  name: "App",

  components: {
    MatchingGame
  },

  data: () => ({
    //
  })
};
</script>
