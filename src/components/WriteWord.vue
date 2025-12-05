<script setup>
import { onMounted, ref } from 'vue';

const arrayEnglishWords = ref([]);
const API_URL = 'https://danidiaz.site/recuerdavulario/api/getData.php'

const englishWord = ref("")
const spanishWord = ref("")
const inputClass = ref("guess-word");
const tryWord = ref("")

onMounted(() => {
    loadWords();
})

async function loadWords() {
    try {
        const response = await fetch(API_URL);
        const data = await response.json();
        arrayEnglishWords.value = data;
        setEnglishWordGuess();
    } catch (error) {
        console.error("Error:", error);
    }
}

function setRandomEnglishWord() {
    return Math.floor(Math.random() * arrayEnglishWords.value.length);
}

function setEnglishWordGuess() {
    const randomWord = setRandomEnglishWord();
    spanishWord.value = arrayEnglishWords.value[randomWord].traduccion_palabra
    englishWord.value = arrayEnglishWords.value[randomWord].ingles_palabra
}

function checkWord() {

    if (englishWord.value.toLocaleLowerCase() === tryWord.value.toLocaleLowerCase()) {
        setEnglishWordGuess()
        tryWord.value = ''
        inputClass.value = "guess-word";

    } else {
        inputClass.value = "guess-word-wrong";
    }

}

function playerSurrendered() {
    tryWord.value = englishWord.value
}

</script>

<template>

    <h2>Escribe la traducción</h2>

    <div class="div-guess">
        <p class="guess-word">{{ spanishWord }}</p>
        <input :class="inputClass" v-model="tryWord" @keyup.enter="checkWord" placeholder="Escribe la traducción"></input>
    </div>
    <div class="div-btn">
        <button class="btn-check" @click="checkWord()">Comprobar</button>
        <button class="btn-surrender" @click="playerSurrendered()">Ver solución</button>
        <button class="btn-surrender" @click="setEnglishWordGuess()">Saltar palabra</button>
    </div>


</template>

<style scoped>


h2 {
    font-size: 24px;
    color: var(--text-color, #e0e0e0);
    text-align: center;
    margin-top: 30px;
    margin-bottom: 20px;
}

.div-guess {
    width: 100%;
    max-width: 320px;
    margin: 0 auto;  
    display: flex;
    flex-direction: column;
    align-items: center;
}

p.guess-word {
    font-size: 32px;
    font-weight: bold;
    color: var(--primary-color, #8ab4f8);
    text-align: center;
    margin: 0 0 20px 0;
    text-shadow: 0 0 5px var(--shadow-color, rgba(0, 0, 0, 0.4));
}


input {
    background-color: var(--card-bg, #1e1e1e);
    color: var(--text-color, #e0e0e0);
    border: 2px solid var(--primary-color, #8ab4f8);
    width: 100%;
    padding: 12px 15px;
    border-radius: 10px;
    font-size: 18px;
    text-align: center; 
    box-shadow: 0 2px 8px var(--shadow-color, rgba(0, 0, 0, 0.4));
    transition: all 0.2s ease;
    box-sizing: border-box;
    outline: none;
}

input:focus {
    border-color: var(--primary-color, #8ab4f8);
    box-shadow: 0 0 0 3px rgba(138, 180, 248, 0.5);
}

.guess-word-wrong {
    border-color: #e74c3c !important;
    color: #e74c3c !important; 
    box-shadow: 0 0 0 3px rgba(231, 76, 60, 0.3) !important;
    animation: shake 0.4s ease-in-out; 
}


.div-btn {
    display: flex;
    flex-wrap: wrap; 
    justify-content: space-between;
    gap: 12px; 
    width: 100%;
    max-width: 320px;    margin: 20px auto 0 auto;
}


.btn-check {
    width: 100%; 
    background-color: var(--primary-color, #8ab4f8);
    color: white;
    border: none;
    padding: 12px;
    border-radius: 10px;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 4px 10px var(--shadow-color, rgba(0, 0, 0, 0.4));
    transition: transform 0.1s, background-color 0.2s;
}

.btn-check:hover {
    background-color: var(--hover-color, #6a95e0);
}

.btn-surrender {
    flex: 1;
    background-color: transparent;
    color: var(--text-color, #e0e0e0);
    border: 2px solid var(--text-color, #e0e0e0);
    padding: 10px 5px;
    border-radius: 8px;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.2s;
    white-space: nowrap; 
}

.btn-surrender:hover {
    border-color: var(--primary-color, #8ab4f8);
    color: var(--primary-color, #8ab4f8);
    background-color: var(--bg-color, #121212);
}

button:active {
    transform: scale(0.96);
}

@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-5px); }
    75% { transform: translateX(5px); }
}


@media (min-width: 600px) {
    h2 { font-size: 30px; }
    p.guess-word { font-size: 40px; }
    
    .div-guess, .div-btn { max-width: 400px; }
    .btn-surrender { font-size: 16px; }
}
</style>