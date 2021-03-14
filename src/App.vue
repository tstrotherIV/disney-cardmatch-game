<template>
  <v-app>
    <v-main>
      <matching-game />
    </v-main>
  </v-app>
</template>

<script>
import MatchingGame from "./components/MatchingGame.vue";

export default {
  name: "App",

  components: {
    MatchingGame,
  },

  data: () => ({
    //
  }),
};
</script>
