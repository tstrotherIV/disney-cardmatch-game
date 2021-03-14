<template>
  <div :class="{ flipcard: flippedClass }" @click="cardClicked">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img
          src="../assets/DisneyCard.png"
          alt="Disney Playing Card"
          height="350px"
        />
      </div>
      <div class="flip-card-back">
        <img
          :src="require('@/assets/' + card.image)"
          :alt="card.name"
          :title="card.name"
          height="350px"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["card", "guess1", "guess2", "cardSelected"],
  data() {
    return {
      cardFlipped: this.cardSelected,
    };
  },
  methods: {
    cardClicked() {
      if (!this.guess2) {
        this.cardFlipped = true;
      }
      this.$emit("card-selected", this.card);
    },
  },
  computed: {
    flippedClass() {
      return (
        this.card.foundMatch ||
        this.card === this.guess1 ||
        this.card === this.guess2
      );
    },
  },
};
</script>

<style>
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 350px;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
}

/* This container is needed to position the front and back side */
.flip-card-inner {
  position: relative;
  width: 300px;
  height: 350px;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flipcard:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flipcard .flip-card-inner {
  transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  background-color: rgba(187, 187, 187, 0);
  color: black;
}

/* Style the back side */
.flip-card-back {
  color: white;
  transform: rotateY(180deg);
}
</style>
