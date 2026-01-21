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

const gameType = ref("link")

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
        <button id="link-words" class="choose-game" @click="changeGame('link')">Enlazar verbos</button>
    </div>


    <SpanishGuess v-if="gameType === 'spanish'" />
    <EnglishGuess v-else-if="gameType === 'english'" />
    <TwentyWords v-else-if="gameType === 'twenty'" />
    <IrregularVerbs v-else-if="gameType === 'verbs'" />
    <WriteWord v-else-if="gameType === 'write'" />
    <FIllIrregularVerb v-else-if="gameType === 'fill'" />
    <LinkWords v-else-if="gameType === 'link'" />
</template>

<style scoped>
.choose-game {
    background-color: var(--card-bg);
    color: var(--primary-color);
    border: 2px solid var(--primary-color);
    padding: 10px 20px;
    border-radius: 8px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.2s, color 0.2s, transform 0.1s, box-shadow 0.2s;
    width: 100%;
    max-width: 250px;
    margin: 5px 0;
    margin-left: 15px;
    box-shadow: 0 2px 5px var(--shadow-color);
}

.choose-game:hover {
    background-color: var(--primary-color);
    color: white;
}

.choose-game:active {
    transform: scale(0.98);
}

#game-selection {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
    width: 100%;
    max-width: 400px;
    margin-bottom: 20px;
}


@media (min-width: 600px) {

    #game-selection {
        flex-direction: row;
        justify-content: center;
        gap: 30px;
    }

    .choose-game {
        max-width: 200px;
        font-size: 18px;
    }
}
</style>
