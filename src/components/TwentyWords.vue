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
h3 {
    text-align: center;
    font-size: 28px;
    color: var(--accent);
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid var(--border);
}

button {
    display: block;
    margin: 0 auto 30px;
    padding: 14px 28px;
    background-color: var(--surface);
    color: var(--text-primary);
    border: 1px solid var(--border);
    border-radius: 8px;
    font-size: 16px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s ease;
}

button:hover {
    background-color: var(--border);
    border-color: var(--accent);
    transform: translateY(-2px);
}

.words-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 20px;
}

.word-box {
    background-color: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 25px;
    transition: all 0.2s ease;
}

.word-box:hover {
    border-color: var(--accent);
    transform: translateY(-3px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.word-box p {
    font-size: 20px;
    color: var(--text-primary);
    margin: 0;
    text-align: center;
    line-height: 1.6;
}

.translation {
    color: var(--accent);
    transition: color 0.2s ease;
}

.translation.hidden {
    color: transparent;
    text-shadow: 0 0 8px rgba(79, 195, 247, 0.3);
    user-select: none;
}

@media (max-width: 768px) {
    h3 {
        font-size: 24px;
        margin-bottom: 20px;
        padding-bottom: 12px;
    }
    
    button {
        margin-bottom: 25px;
        padding: 12px 24px;
        font-size: 15px;
    }
    
    .words-container {
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
        gap: 15px;
    }
    
    .word-box {
        padding: 20px;
    }
    
    .word-box p {
        font-size: 18px;
    }
}

@media (max-width: 480px) {
    h3 {
        font-size: 22px;
    }
    
    button {
        width: 100%;
        max-width: 300px;
        padding: 12px 20px;
    }
    
    .words-container {
        grid-template-columns: 1fr;
    }
    
    .word-box {
        padding: 18px;
    }
    
    .word-box p {
        font-size: 17px;
    }
}


</style>