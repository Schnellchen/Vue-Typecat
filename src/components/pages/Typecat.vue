<template>
  <div class="typecat">
    <div class="header">
      <span v-for="item in randomWords" :key="item.word" :class="item.status">{{
        item.word + " "
      }}</span>
    </div>
    <div class="body">
      <input v-model="value" @keydown.enter="checkWord" />
    </div>
    <div class="timer"></div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { words } from "@/config/words";

type WordObjectInterface = {
  word: string;
  status: string;
};

export default Vue.extend({
  name: "Typecat",
  data() {
    const value = "";
    const currentWord = 0;
    const randomWords: Array<WordObjectInterface> = [];
    return { value, currentWord, randomWords };
  },
  methods: {
    checkWord(): void {
      if (this.currentWord === this.randomWords.length) {
        return;
      }

      if (this.value === this.randomWords[this.currentWord].word) {
        this.randomWords[this.currentWord].status = "accepted";
      } else {
        this.randomWords[this.currentWord].status = "declined";
      }
      this.value = "";
      this.currentWord++;
    }
  },
  mounted() {
    this.randomWords = words
      .map((item: string) => ({ word: item, status: "default" }))
      .slice(0, 25);
  }
});
</script>

<style scoped>
.typecat {
  background-color: white;
}
.default {
  color: black;
}
.accepted {
  color: greenyellow;
}
.declined {
  color: red;
}
</style>
