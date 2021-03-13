<template>
  <v-container class="card-section">
    <div v-for="card in disneyCards" :key="card.id">
      <card
        :card="card"
        @card-selected="cardPicked"
        :cardSelected="cardSelected"
        :guess1="guess1"
        :guess2="guess2"
      />
    </div>
  </v-container>
</template>

<script>
import getDisneyCards from "../data";
import shuffle from "lodash.shuffle";
import Card from "./Card.vue";

export default {
  components: { Card },
  data() {
    return {
      disneyCards: shuffle(getDisneyCards()),
      guess1: null,
      guess2: null,
      cardSelected: false,
    };
  },
  methods: {
    cardPicked(card) {
      if (!this.guess1) {
        this.guess1 = card.name;
        return;
      }

      if (this.guess1 && !this.guess2) {
        this.guess2 = card.name;
        return;
      }
    },
  },
};
</script>

<style>
.card-section {
  display: flex;
  flex-direction: row;
  flex-flow: wrap;
}
</style>
