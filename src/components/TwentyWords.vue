<script setup>
import { onMounted, inject, ref } from 'vue';

const arrayWords = inject('arrayWords')
const randomIndexList = ref([]);
const showTranslation = ref(true); 

onMounted(async () => {
    randomIndexList.value = setRandomNumbers(arrayWords.value.length);
});

// mediante el tamaño del array, se consiguen 20 posiciones aleatorias
function setRandomNumbers(arraySize){
    const today = new Date().toISOString().split('T')[0];

    let seedValue = 0;
    for (let i = 0; i < today.length; i++) {
        seedValue += today.charCodeAt(i);
    }

    function seededRandom() {
        seedValue = (seedValue * 1664525 + 1013904223) % 4294967296;
        return seedValue / 4294967296;
    }

    const indexes = Array.from({ length: arraySize }, (_, i) => i);
    const shuffled = indexes.slice().sort(() => seededRandom() - 0.5);
    return shuffled.slice(0, 20);
}

function hideTrad(){
    showTranslation.value = !showTranslation.value;
}

</script>

<template>
  <h3>Las 20 palabras del día </h3>
  <button @click="hideTrad">Esconder la traducción</button>
  <div v-if="arrayWords.length && randomIndexList.length" class="words-container">
    <div 
      v-for="(index, i) in randomIndexList" 
      :key="i"
      class="word-box"
    >
      <p><strong>{{ arrayWords[index]?.ingles_palabra }}</strong> - <strong 
          :class="{ 'hidden': !showTranslation }"
          class="translation"
        >
          {{ arrayWords[index]?.traduccion_palabra }}
        </strong></p>
    </div>
  </div>

  <p v-else>Cargando...</p>
</template>

<style scoped>


.word-box:hover {
  transform: scale(1.03);
  box-shadow: 0 4px 15px var(--shadow-color, rgba(0, 0, 0, 0.6));
}

h3 {
  color: var(--primary-color, #8ab4f8);
  text-align: center;
  margin-bottom: 20px;
  text-shadow: 0 0 5px var(--shadow-color, rgba(0, 0, 0, 0.4));
}

div[v-if] {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.words-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.word-box {
  background: var(--card-bg, #1e1e1e); 
  color: var(--text-color, #e0e0e0); 
  padding: 12px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 6px var(--shadow-color, rgba(0, 0, 0, 0.4));
  border-left: 4px solid var(--primary-color, #8ab4f8);
}

.translation.hidden {
  color: transparent !important; 
  text-shadow: 0 0 8px var(--text-color, #e0e0e0); 
  background-color: transparent !important;
}

button {
    background-color: var(--card-bg, #1e1e1e); 
    color: var(--primary-color, #8ab4f8);
    border: 2px solid var(--primary-color, #8ab4f8);
    padding: 10px 20px;
    border-radius: 8px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.2s, color 0.2s, transform 0.1s, box-shadow 0.2s;
    margin: 10px auto 30px auto; 
    display: block;
    max-width: 300px;
}

button:hover {
    background-color: var(--primary-color, #8ab4f8);
    color: white;
}

button:active {
    transform: scale(0.98);
}

</style>