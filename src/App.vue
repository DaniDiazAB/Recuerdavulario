<script setup>
import { onMounted, provide, ref } from 'vue';

import EnglishGuess from './components/EnglishGuess.vue';
import SpanishGuess from './components/SpanishGuess.vue';
import TitleComponent from './components/TitleComponent.vue';
import TwentyWords from './components/TwentyWords.vue';
import IrregularVerbs from './components/IrregularVerbs.vue';
import WriteWord from './components/WriteWord.vue';
import FIllIrregularVerb from './components/FIllIrregularVerb.vue';
import LinkWords from './components/LinkWords.vue';

const API_URL = 'https://danidiaz.site/recuerdavulario/api/getData.php'
const arrayWords = ref([])

provide('arrayWords', arrayWords)

onMounted(() => {
    setWords();
})

async function setWords() {
    try {
        const response = await fetch(API_URL);
        const data = await response.json();
        arrayWords.value = data;
    } catch (error) {
        console.error("Error:", error);
    }
}

const gameType = ref("english")

function changeGame(selectedGameType) {
    gameType.value = selectedGameType
}

</script>

<template>
    <TitleComponent />
    <div class="game-selection">
        <button id="eng-to-spa" class="choose-game" @click="changeGame('english')">Inglés a español</button>
        <button id="spa-to-eng" class="choose-game" @click="changeGame('spanish')">Español a inglés</button>
        <button id="twenty-words" class="choose-game" @click="changeGame('twenty')">Las 20 de hoy</button>
        <button id="write-word" class="choose-game" @click="changeGame('write')">Escribe la palabra</button>
        <button id="irregular-verbs" class="choose-game" @click="changeGame('verbs')">Verbos Irregulares</button>
        <button id="write-word" class="choose-game" @click="changeGame('fill')">Rellenar el verbo</button>
        <button id="link-words" class="choose-game" @click="changeGame('link')">Enlazar palabras</button>
    </div>


    <SpanishGuess v-if="gameType === 'spanish'" />
    <EnglishGuess v-else-if="gameType === 'english'" />
    <TwentyWords v-else-if="gameType === 'twenty'" />
    <IrregularVerbs v-else-if="gameType === 'verbs'" />
    <WriteWord v-else-if="gameType === 'write'" />
    <FIllIrregularVerb v-else-if="gameType === 'fill'" />
    <LinkWords v-else-if="gameType === 'link'" />
</template>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --primary-bg: #0f1115;
    --secondary-bg: #151821;
    --card-bg: #1b1f2a;
    --surface: #222735;
    --border: #2f3547;
    --text-primary: #e6e9ef;
    --text-secondary: #a9afc3;
    --accent: #4fc3f7;
    --accent-hover: #29b6f6;
    --success: #66bb6a;
    --error: #ef5350;
    --radius-sm: 8px;
    --radius-md: 12px;
    --radius-lg: 16px;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, sans-serif;
    background-color: var(--primary-bg);
    color: var(--text-primary);
    min-height: 100vh;
    line-height: 1.6;
}

#app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

.game-selection {
    display: flex;
    gap: 12px;
    padding: 16px;
    max-width: 1400px;
    margin: 0 auto;
    width: 100%;
    background-color: var(--secondary-bg);
    border-bottom: 1px solid var(--border);
}

.choose-game {
    flex: 1;
    min-width: 170px;
    max-width: 220px;
    padding: 14px 22px;
    background-color: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    color: var(--text-primary);
    font-size: 15px;
    font-weight: 500;
    cursor: pointer;
    transition: background-color .2s ease, transform .2s ease, border-color .2s ease;
}

.choose-game:hover {
    background-color: var(--border);
    transform: translateY(-1px);
}

.choose-game.router-link-active,
.choose-game.active {
    background-color: var(--accent);
    border-color: var(--accent);
    color: var(--primary-bg);
    font-weight: 600;
}

button:focus-visible {
    outline: 2px solid var(--accent);
    outline-offset: 2px;
}

.component-container {
    flex: 1;
    padding: 32px 20px;
    max-width: 1200px;
    margin: 0 auto;
    width: 100%;
}

.game-card {
    background-color: var(--card-bg);
    border-radius: var(--radius-md);
    padding: 28px;
    border: 1px solid var(--border);
    box-shadow: 0 10px 30px rgba(0, 0, 0, .25);
}

.input-field {
    width: 100%;
    padding: 15px 16px;
    background-color: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    color: var(--text-primary);
    font-size: 16px;
    transition: border-color .2s ease, background-color .2s ease;
}

.input-field:focus {
    border-color: var(--accent);
    background-color: #262c3d;
    outline: none;
}

.btn-primary,
.btn-secondary {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 15px 30px;
    border-radius: var(--radius-sm);
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: background-color .2s ease, transform .2s ease, border-color .2s ease;
}

.btn-primary {
    background-color: var(--accent);
    color: var(--primary-bg);
    border: none;
}

.btn-primary:hover {
    background-color: var(--accent-hover);
    transform: translateY(-2px);
}

.btn-secondary {
    background-color: var(--surface);
    color: var(--text-primary);
    border: 1px solid var(--border);
}

.btn-secondary:hover {
    background-color: var(--border);
    border-color: var(--accent);
}

.word-display {
    font-size: 32px;
    font-weight: 600;
    text-align: center;
    margin: 24px 0;
    padding: 20px;
    background-color: var(--surface);
    border-radius: var(--radius-md);
    border-left: 4px solid var(--accent);
}

.score-display {
    font-size: 20px;
    font-weight: 600;
    color: var(--accent);
    text-align: center;
    margin-top: 8px;
}

.feedback-correct,
.feedback-incorrect {
    font-size: 18px;
    font-weight: 500;
    text-align: center;
    padding: 10px;
}

.feedback-correct {
    color: var(--success);
}

.feedback-incorrect {
    color: var(--error);
}

.grid-layout {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 20px;
    margin-top: 30px;
}

.verb-form {
    background-color: var(--surface);
    padding: 20px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
}

.verb-form label {
    display: block;
    margin-bottom: 6px;
    color: var(--text-secondary);
    font-weight: 500;
}

.link-words-container {
    display: flex;
    flex-direction: column;
    gap: 14px;
    max-width: 600px;
    margin: 0 auto;
}

.word-pair {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    padding: 14px 16px;
    background-color: var(--surface);
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    transition: border-color .2s ease, background-color .2s ease;
}

.word-pair:hover {
    border-color: var(--accent);
    background-color: #262c3d;
}

@media (max-width: 768px) {
    .game-selection {
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
        scrollbar-width: none;
    }

    .game-selection::-webkit-scrollbar {
        display: none;
    }

    .component-container {
        padding: 24px 16px;
    }

    .game-card {
        padding: 20px;
    }

    .word-display {
        font-size: 26px;
    }

    .grid-layout {
        grid-template-columns: 1fr;
    }

    .word-pair {
        flex-direction: column;
        text-align: center;
    }
}

@media (max-width: 480px) {
    .choose-game {
        min-width: 140px;
        font-size: 13px;
        padding: 10px 14px;
    }

    .btn-primary,
    .btn-secondary {
        width: 100%;
        font-size: 15px;
        padding: 14px 20px;
    }

    .word-display {
        font-size: 22px;
        padding: 14px;
    }

    .input-field {
        font-size: 15px;
        padding: 14px;
    }
}
</style>
