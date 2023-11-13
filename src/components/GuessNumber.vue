<script setup>
import { ref } from "vue";

const randomNumber = ref(Math.floor(Math.random() * 100 + 1));
const userValueInput = ref("");
const previousGuesses = ref([]);
const countAttempts = ref(10);
const message = ref("");


const checkNumber = () => {
    const numberUser = + userValueInput.value;

    if(previousGuesses.lenght > countAttempts){
        message.value = "Game over!";
        return;
    }

    previousGuesses.value.push(numberUser);

    if (numberUser > randomNumber.value) {
        message.value = `Too High! Try again.`;
    } else if (numberUser < randomNumber.value) {
        message.value = `Too low! Try again.`;
    } else {
        message.value = `Correct number!`;
    }

    if(countAttempts.value > 0){
        countAttempts.value--;
    } else {
        message.value = `No more attempts!`;
    }
    
    userValueInput.value = "";
}

</script>

<template>
    <p>Try and guess a random number between 1 and 100.</p>
    <p>You have {{countAttempts}} attempts to guess the right number.</p>
    <div id="wrapper">
        <label for="guessField">Guess a number</label>
        <input type="number" id="guessField" v-model="userValueInput">
        <label for="numberAttempts">Number of attempts</label>
        <input type="number" id="numberAttempts" v-model="countAttempts">
        <button class="button-check" @click="checkNumber">Check Guess</button>

        <div class="resultParas">
            <p>Previous Guesses: <span class="guesses">{{ previousGuesses }}</span></p>
            <p>Guesses Remaining: <span class="lastResult">{{ countAttempts }}</span></p>
            <p class="lowOrHi">{{ message }}</p>
        </div>
    </div>
</template>

<style></style>