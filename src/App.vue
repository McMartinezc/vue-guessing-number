<script setup>
import GuessNumber from "./components/GuessNumber.vue";
import { ref } from 'vue';

const isPlaying = ref(false)

const startGame = () => {
  console.log("Game Starts")
  isPlaying.value = true;
}

</script>

<template>
  <main>
    <h2>Number guessing game</h2>

    <section v-if="isPlaying">
     <GuessNumber />
    </section>
    <section v-else>
      <button @click="startGame">Start Game</button>
    </section>
  </main>
</template>

<style>
.button-check {
  background-color: rgb(128, 70, 128);
}
</style>
