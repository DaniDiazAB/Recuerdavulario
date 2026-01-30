<script setup>
import { onMounted, inject, ref } from 'vue';

const arrayEnglishWords = inject('arrayWords')
const englishWord = ref("")
const spanishWord = ref("")
const inputClass = ref("guess-word")
const tryWord = ref("")

onMounted(() => {
    loadWords()
})

function loadWords() {
    setNextWord()
}

function setRandomEnglishWord() {
    return Math.floor(Math.random() * arrayEnglishWords.value.length)
}

function setNextWord() {
    const randomWord = setRandomEnglishWord()
    spanishWord.value = arrayEnglishWords.value[randomWord].traduccion_palabra
    englishWord.value = arrayEnglishWords.value[randomWord].ingles_palabra
    tryWord.value = ''
    inputClass.value = 'guess-word'
}

function checkWord() {
    if (
        englishWord.value.toLowerCase() === tryWord.value.toLowerCase()
    ) {
        setNextWord()
    } else {
        inputClass.value = 'guess-word-wrong'
    }
}

function playerSurrendered() {
    tryWord.value = englishWord.value
}
</script>


<template>

    <h3>Escribe la traducción</h3>

    <div class="div-guess">
        <p class="guess-word">{{ spanishWord }}</p>
        <input :class="inputClass" v-model="tryWord" @keyup.enter="checkWord"
            placeholder="Escribe la traducción"></input>
    </div>
    <div class="div-btn">
        <button class="btn-check" @click="checkWord()">Comprobar</button>
        <button class="btn-surrender" @click="playerSurrendered()">Ver solución</button>
        <button class="btn-surrender" @click="setNextWord()">Saltar palabra</button>

    </div>


</template>

<style scoped>
h3 {
    text-align: center;
    font-size: 28px;
    color: var(--accent);
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid var(--border);
}

h2 {
    text-align: center;
    font-size: 32px;
    color: var(--accent);
    margin-bottom: 40px;
    font-weight: 600;
}

.div-guess {
    background-color: var(--surface);
    border: 2px solid var(--border);
    border-radius: 12px;
    padding: 40px;
    max-width: 600px;
    margin: 0 auto 30px;
    text-align: center;
}

.guess-word {
    font-size: 38px;
    font-weight: 600;
    color: white;
    margin-bottom: 30px;
    min-height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
}

input {
    width: 100%;
    padding: 20px;
    font-size: 22px;
    background-color: var(--card-bg);
    border: 2px solid var(--border);
    border-radius: 8px;
    color: var(--text-primary);
    text-align: center;
    transition: all 0.2s ease;
}

input:focus {
    border-color: var(--accent);
    outline: none;
    box-shadow: 0 0 0 3px rgba(79, 195, 247, 0.1);
}

input.correct {
    border-color: var(--success);
    background-color: rgba(102, 187, 106, 0.1);
}

input.incorrect {
    border-color: var(--error);
    background-color: rgba(244, 67, 54, 0.1);
}

.div-btn {
    display: flex;
    justify-content: center;
    gap: 20px;
    max-width: 600px;
    margin: 0 auto;
    flex-wrap: wrap;
}

.btn-check {
    background-color: var(--accent);
    color: var(--primary-bg);
    padding: 18px 36px;
    border: none;
    border-radius: 8px;
    font-size: 18px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    flex: 1;
    min-width: 180px;
}

.btn-check:hover {
    background-color: var(--accent-hover);
    transform: translateY(-2px);
}

.btn-surrender {
    background-color: var(--surface);
    color: var(--text-primary);
    padding: 18px 36px;
    border: 1px solid var(--border);
    border-radius: 8px;
    font-size: 18px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s ease;
    flex: 1;
    min-width: 180px;
}

.btn-surrender:hover {
    background-color: var(--border);
    border-color: var(--accent);
    transform: translateY(-2px);
}

@media (max-width: 768px) {
    h2 {
        font-size: 28px;
        margin-bottom: 30px;
    }

    .div-guess {
        padding: 30px 20px;
        margin-bottom: 25px;
    }

    .guess-word {
        font-size: 32px;
        margin-bottom: 25px;
        min-height: 50px;
    }

    input {
        padding: 18px;
        font-size: 20px;
    }

    .div-btn {
        gap: 15px;
    }

    .btn-check,
    .btn-surrender {
        padding: 16px 28px;
        font-size: 17px;
        min-width: 160px;
    }
}

@media (max-width: 480px) {
    h2 {
        font-size: 24px;
        margin-bottom: 25px;
    }

    .div-guess {
        padding: 25px 15px;
        margin-bottom: 20px;
    }

    .guess-word {
        font-size: 28px;
        margin-bottom: 20px;
    }

    input {
        padding: 16px;
        font-size: 18px;
    }

    .div-btn {
        flex-direction: column;
        align-items: stretch;
        gap: 12px;
    }

    .btn-check,
    .btn-surrender {
        width: 100%;
        min-width: auto;
        padding: 16px 20px;
    }
}
</style>