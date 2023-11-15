<script setup>
import { ref, computed } from "vue";


const randomNumber = ref(Math.floor(Math.random() * 100 + 1));
const userValueInput = ref("");
const previousGuesses = ref([]);
const countAttempts = ref(10);

const checkNumber = () => {
    previousGuesses.value.push(userValueInput.value);
    countAttempts.value--;
    userValueInput.value = "";
}

const lastGuess = computed(() => {
    return previousGuesses.value[previousGuesses.value.length - 1];
})

//Deshabilita el input cuando se cumple la condición 
const mustDisableInput = computed(()=>{
    return countAttempts.value===0 || lastGuess.value===randomNumber.value;
})

</script>

<template>
    <div id="wrapper">
        <p>Try and guess a random number between 1 and 100.</p>
        <p>You have {{ countAttempts }} attempts to guess the right number.</p>

        <label for="guessField">Guess a number:</label>
        <input :disabled="mustDisableInput" type="number" id="guessField" v-model="userValueInput">

        <label for="numberAttempts">Number of attempts:</label>
        <input type="number" id="numberAttempts" v-model="countAttempts">

        <button :disabled="!userValueInput" class="button-check" @click="checkNumber">Check Guess</button>

        <div v-show="previousGuesses.length != 0" class="resultParas">
            <p>Previous Guesses: <span class="guesses">{{ previousGuesses }}</span></p>
            <p>Guesses Remaining: <span class="lastResult">{{ countAttempts }}</span></p>
            <p v-if="countAttempts === 0 && lastGuess !== randomNumber">YOU LOST 🤧</p>
            <p style="color: red" v-else-if="lastGuess > randomNumber">Is lower</p>
            <p style="color: green" v-else-if="lastGuess < randomNumber">Is higher</p>
            <p v-else-if="lastGuess === randomNumber">You Won!! Correct number was {{ randomNumber }} </p>
        </div>

        <button class="button-reset" v-show="mustDisableInput" @click="startGame">New Game</button>

    </div>
</template>

<style></style>