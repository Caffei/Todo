<template>
  <q-page class="q-px-xl q-py-lg">
    <q-btn color="primary" label="Play again" @click="shuffleDeck" />
    <br />
    <span class="text-weight-bold text-subtitle2">Score {{ score }}</span>
    <q-list>
      <q-item-section class="memory">
        <q-item
          clickable
          v-for="(card, index) in cards"
          :key="index"
          @click="face(index)"
          :class="!card.side ? 'card-back' : 'card-front '"
        >
          <q-item-label v-if="card.side" class="card">
            <span class="material-icons"> {{ card.icon }} </span>
          </q-item-label>
        </q-item>
      </q-item-section>
    </q-list>
  </q-page>
</template>


<script>
import { createDOMCompilerError } from "@vue/compiler-dom";

export default {
  data() {
    return {
      quantity: "null",
      inverted: 0,
      prev: null,
      curr: null,
      play: false,
      score: 0,
      cards: [
        { id: 0, icon: "build", side: false },
        { id: 1, icon: "build", side: false },
        { id: 2, icon: "credit_card", side: false },
        { id: 3, icon: "credit_card", side: false },
        { id: 4, icon: "explore", side: false },
        { id: 0, icon: "explore", side: false },
        { id: 6, icon: "star_rate", side: false },
        { id: 7, icon: "star_rate", side: false },
        { id: 8, icon: "code", side: false },
        { id: 9, icon: "code", side: false },
        { id: 10, icon: "print", side: false },
        { id: 11, icon: "print", side: false },
        { id: 12, icon: "code", side: false },
        { id: 13, icon: "code", side: false },
        { id: 14, icon: "touch_app", side: false },
        { id: 15, icon: "touch_app", side: false },
        { id: 16, icon: "view_in_ar", side: false },
        { id: 17, icon: "view_in_ar", side: false },
        { id: 18, icon: "assignment_ind", side: false },
        { id: 19, icon: "assignment_ind", side: false },
      ],
    };
  },
  methods: {
    face(index) {
      if (this.prev != index && this.cards[index].side == false) {
        this.cards[index].side = true;
        this.inverted++;
        this.prev = this.curr;
        this.curr = index;
        if (this.inverted == 2) {
          if (this.cards[this.prev].icon != this.cards[this.curr].icon) {
            this.reverse();
          } else {
            this.score++;
          }

          this.inverted = 0;
          this.prev = null;
          this.curr = null;
        }
      }
    },
    reverse() {
      this.cards[this.prev].side = false;
      this.cards[this.curr].side = false;
    },
    shuffleDeck() {
      for (var i = this.cards.length - 1; i > 0; i--) {
        var j = Math.floor(Math.random() * (i + 1));
        var temp = this.cards[i];
        this.cards[i] = this.cards[j];
        this.cards[j] = temp;
      }
      for (var i = 0; i < this.cards.length; i++) {
        this.cards[i].side = false;

        this.score = 0;
      }
    },
  },
};
</script>

<style>
.memory {
  display: grid;
  grid-template-columns: repeat(5, auto);
  grid-gap: 10px;
}
.card-back {
  background-color: pink;
  height: 275px;
  width: 225px;
  box-shadow: 1px 3px 3px gray;
}
.card-front {
  background-color: lightgray;
  height: 275px;
  width: 225px;
  transition: transform 500ms ease-in-out;
}
.card {
  display: grid;
  padding-left: 50%;
}
.shuffleFast-move {
  transition: transform 0.5s;
}
</style>
