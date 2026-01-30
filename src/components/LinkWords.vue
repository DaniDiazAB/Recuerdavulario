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
    <h3>Enlaza las palabras</h3>
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

h3 {
    text-align: center;
    font-size: 28px;
    color: var(--accent);
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid var(--border);
}

.game-board {
    display: flex;
    gap: 40px;
    max-width: 1200px;
    margin: 0 auto;
    padding: 30px;
    align-items: flex-start;
}

.column {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.title {
    text-align: center;
    font-size: 24px;
    color: var(--accent);
    margin-bottom: 10px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.card {
    padding: 25px 20px;
    background-color: var(--surface);
    border: 2px solid var(--border);
    border-radius: 10px;
    color: var(--text-primary);
    font-size: 20px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s ease;
    user-select: none;
    min-height: 90px;
    display: flex;
    align-items: center;
    justify-content: center;
    word-break: break-word;
    overflow-wrap: break-word;
}

.card:hover {
    border-color: var(--accent);
    transform: translateY(-3px);
}

.card.is-selected {
    border-color: var(--accent);
    background-color: rgba(79, 195, 247, 0.1);
    color: var(--accent);
    font-weight: 600;
}

.card.is-matched {
    border-color: var(--success);
    background-color: rgba(102, 187, 106, 0.1);
    color: var(--success);
    cursor: default;
    transform: none;
}

.card.is-matched:hover {
    border-color: var(--success);
    transform: none;
}

.card.is-error {
    border-color: var(--error);
    background-color: rgba(244, 67, 54, 0.1);
    color: var(--error);
    animation: shake 0.3s ease;
}

@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-5px); }
    75% { transform: translateX(5px); }
}

@media (max-width: 768px) {
    .game-board {
        flex-direction: column;
        gap: 30px;
        padding: 20px;
    }
    
    .column {
        width: 100%;
    }
    
    .title {
        font-size: 22px;
        height: 45px;
    }
    
    .card {
        padding: 20px 15px;
        font-size: 18px;
        min-height: 80px;
    }
}

@media (max-width: 480px) {
    .game-board {
        padding: 15px;
        gap: 25px;
    }
    
    .title {
        font-size: 20px;
        height: 40px;
    }
    
    .card {
        padding: 18px 12px;
        font-size: 17px;
        min-height: 75px;
    }
}

</style>
