<script setup>
import { watch, ref, inject } from 'vue';

const arrayWords = inject('arrayWords');

const leftColumn = ref([]);  
const rightColumn = ref([]); 
const selectedLeft = ref(null);
const selectedRight = ref(null);
const solvedIds = ref([]);   

const shuffle = (array) => {
    return array.sort(() => Math.random() - 0.5);
};

const startGame = (rawData) => {
    if (!rawData || rawData.length === 0) return;

    const shuffledAll = shuffle([...rawData]);

    const selected10 = shuffledAll.slice(0, 10);

    const gameData = selected10.map((item, index) => {
        return {
            id: index, 
            es: item.traduccion_palabra,
            en: item.ingles_palabra
        };
    });

    leftColumn.value = [...gameData];
    rightColumn.value = shuffle([...gameData]); 
    
};

watch(arrayWords, (newValue) => {
    if (newValue && newValue.length > 0) {
        startGame(newValue);
    }
}, { immediate: true });

const handleLeftClick = (item) => {
    if (solvedIds.value.includes(item.id)) return; 
    selectedLeft.value = item;
    checkMatch();
};

const handleRightClick = (item) => {
    if (solvedIds.value.includes(item.id)) return;
    selectedRight.value = item;
    checkMatch();
};

const checkMatch = () => {
    if (selectedLeft.value && selectedRight.value) {
        if (selectedLeft.value.id === selectedRight.value.id) {
            solvedIds.value.push(selectedLeft.value.id);
            resetSelection();
        } else {
            setTimeout(() => {
                resetSelection();
            }, 500);
        }
    }
};

const resetSelection = () => {
    selectedLeft.value = null;
    selectedRight.value = null;
};

</script>

<template>
    <div class="game-board">
        <div class="column">
            <h3 class="title">Español</h3>
            <div 
                v-for="word in leftColumn" 
                :key="word.id"
                class="card"
                :class="{
                    'is-selected': selectedLeft && selectedLeft.id === word.id,
                    'is-matched': solvedIds.includes(word.id),
                    'is-error': selectedLeft && selectedRight && selectedLeft.id === word.id && selectedLeft.id !== selectedRight.id
                }"
                @click="handleLeftClick(word)"
            >
                {{ word.es }}
            </div>
        </div>

        <div class="column">
            <h3 class="title">Inglés</h3>
            <div 
                v-for="word in rightColumn" 
                :key="word.id"
                class="card"
                :class="{
                    'is-selected': selectedRight && selectedRight.id === word.id,
                    'is-matched': solvedIds.includes(word.id),
                    'is-error': selectedLeft && selectedRight && selectedRight.id === word.id && selectedLeft.id !== selectedRight.id
                }"
                @click="handleRightClick(word)"
            >
                {{ word.en }}
            </div>
        </div>
    </div>
</template>

<style>
/* =====================================================
 * 1. Variables CSS (heredadas del diseño general)
 * ===================================================== */

:root {
  --bg-color: #f4f4f9;
  --card-bg: #ffffff;
  --text-color: #1e1e1e;
  --primary-color: #4a90e2;
  --hover-color: #357bd9;
  --success-color: #4caf50;
  --error-color: #e74c3c;
  --shadow-color: rgba(0, 0, 0, 0.1);
}

@media (prefers-color-scheme: dark) {
  :root {
    --bg-color: #121212;
    --card-bg: #1e1e1e;
    --text-color: #e0e0e0;
    --primary-color: #8ab4f8;
    --hover-color: #6a95e0;
    --success-color: #66bb6a;
    --error-color: #ef5350;
    --shadow-color: rgba(0, 0, 0, 0.4);
  }
}

/* =====================================================
 * 2. Contenedor principal del juego
 * ===================================================== */

.game-board {
  display: flex;
  gap: 30px;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
}

/* En móvil, columnas una debajo de la otra */
@media (max-width: 599px) {
  .game-board {
    flex-direction: column;
  }
}

/* =====================================================
 * 3. Columnas (Español / Inglés)
 * ===================================================== */

.column {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.title {
  text-align: center;
  font-size: 22px;
  font-weight: bold;
  color: var(--text-color);
  margin-bottom: 10px;
}

/* =====================================================
 * 4. Tarjetas (palabras)
 * ===================================================== */

.card {
  background: var(--card-bg);
  border: 2px solid var(--primary-color);
  border-radius: 12px;
  padding: 15px 20px;
  font-size: 18px;
  text-align: center;
  cursor: pointer;
  user-select: none;
  box-shadow: 0 2px 8px var(--shadow-color);
  transition: 
    background-color 0.2s ease,
    color 0.2s ease,
    transform 0.1s ease,
    box-shadow 0.2s ease;
}

/* Hover */
.card:hover {
  background: var(--hover-color);
  color: white;
  border-color: var(--hover-color);
}

/* Click */
.card:active {
  transform: scale(0.97);
  box-shadow: 0 1px 5px var(--shadow-color);
}

/* =====================================================
 * 5. Estados del juego
 * ===================================================== */

/* Seleccionada */
.card.is-selected {
  background: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
}

/* Correcta (emparejada) */
.card.is-matched {
  background: var(--success-color);
  border-color: var(--success-color);
  color: white;
  cursor: default;
  opacity: 0.9;
}

/* Error (selección incorrecta) */
.card.is-error {
  background: var(--error-color);
  border-color: var(--error-color);
  color: white;
  animation: shake 0.3s;
}

/* =====================================================
 * 6. Animación de error
 * ===================================================== */

@keyframes shake {
  0% { transform: translateX(0); }
  25% { transform: translateX(-4px); }
  50% { transform: translateX(4px); }
  75% { transform: translateX(-4px); }
  100% { transform: translateX(0); }
}

/* =====================================================
 * 7. Ajustes en pantallas grandes
 * ===================================================== */

@media (min-width: 600px) {
  .title {
    font-size: 24px;
  }

  .card {
    font-size: 20px;
    padding: 18px 25px;
  }
}
</style>
