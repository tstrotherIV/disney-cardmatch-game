<template>
  <div class="background">
    <h1 v-if="matchedThemAll" class="d-flex justify-center pa-10 white--text">
      Thanks for playing! See you real soon!
    </h1>
    <h1 v-else class="d-flex justify-center pa-10 white--text"></h1>

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
  </div>
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
      if (this.guess1 && this.guess2) return;
      if (this.guess1 === card) return;
      if (this.guess1 === null) {
        this.guess1 = card;
        return;
      }
      this.guess2 = card;

      const [DisCard1, DisCard2] = this.getMatchingCards(card.name);

      if (this.guess1.name === this.guess2.name) {
        DisCard1.foundMatch = true;
        DisCard2.foundMatch = true;
        this.guess1 = null;
        this.guess2 = null;
      } else {
        setTimeout(() => {
          this.guess1 = null;
          this.guess2 = null;
        }, 1500);
      }
    },
    getMatchingCards(name) {
      return this.disneyCards.filter((card) => card.name === name);
    },
  },
  computed: {
    matchedThemAll() {
      return this.disneyCards.every((l) => l.foundMatch);
    },
  },
};
</script>

<style>
.background {
  height: 100%;
  background-image: url("../assets/DisneyBackground.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.card-section {
  display: flex;
  flex-direction: row;
  flex-flow: wrap;
  justify-content: center;
}
</style>
