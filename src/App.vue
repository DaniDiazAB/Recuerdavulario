<script setup>
import EnglishGuess from './components/EnglishGuess.vue';
import SpanishGuess from './components/SpanishGuess.vue';
import TitleComponent from './components/TitleComponent.vue';
import { ref } from 'vue';

const gameType = ref("english")

function changeGame(selectedGameType) {
    gameType.value = selectedGameType
}

</script>

<template>
    <TitleComponent />
    <div class="game-selection">
        <button id="eng-to-spa" class="choose-game" @click="changeGame('english')">Inglés a español</button>
        <button id="spa-to-eng" class="choose-game" @click="changeGame('spanish')">Español a Ingles</button>
    </div>


    <SpanishGuess v-if="gameType === 'spanish'" />
    <EnglishGuess v-else-if="gameType === 'english'" />
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

/* Contenedor si los botones están agrupados (opcional, si los envuelves en un div) */
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
