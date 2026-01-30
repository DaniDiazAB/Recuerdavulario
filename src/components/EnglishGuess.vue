<script setup>
import { watch, ref, inject } from 'vue';

const englishRandomWord = ref("");
const spanishRandomWord = ref("");
const arrayWordsWrong = ref([])
const random = ref();
const arrayWords = inject('arrayWords')
const wrongIndexes = ref([]);


watch(
    arrayWords,
    (newValue) => {
        if (newValue.length > 0) {
            setNewTry()
            console.log(arrayWords);

        }
    },
    { immediate: true }
)

function checkWord(word, index) {
    if (word === spanishRandomWord.value) {
        wrongIndexes.value = [];   // reset al acertar
        setNewTry();
    } else {
        if (!wrongIndexes.value.includes(index)) {
            wrongIndexes.value.push(index);
        }
    }
}

function setNewTry() {
    arrayWordsWrong.value.length = 0;
    getRandom();

    englishRandomWord.value = arrayWords.value[random.value].ingles_palabra
    spanishRandomWord.value = arrayWords.value[random.value].traduccion_palabra

    arrayWordsWrong.value.push(arrayWords.value[random.value].traduccion_palabra)
    for (let i = 0; i < 3; i++) {
        getRandom();
        arrayWordsWrong.value.push(arrayWords.value[random.value].traduccion_palabra);
    }
    shuffle(arrayWordsWrong.value)
}


function shuffle(wordsArray) {
    return wordsArray.sort(() => Math.random() - 0.5);
}

function getRandom() {
    random.value = Math.floor(Math.random() * arrayWords.value.length);
}

</script>


<template>
    <h3>Selecciona la traducción</h3>
    <div id="words">
        <div id="english-word">
            <button>
                {{ englishRandomWord }}
            </button>
        </div>

        <div id="spanish-words">

            <button v-for="(word, index) in arrayWordsWrong" :key="index" @click="checkWord(word, index)"
                :class="{ wrong: wrongIndexes.includes(index) }">
                {{ word }}
            </button>

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

#words {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 40px;
    padding: 30px;
    max-width: 800px;
    margin: 0 auto;
}

#english-word {
    width: 100%;
}

#english-word button {
    width: 100%;
    padding: 40px 20px;
    font-size: 42px;
    font-weight: 600;
    background-color: var(--surface);
    color: white;
    border: 2px solid var(--border);
    border-radius: 12px;
    cursor: default;
    transition: all 0.2s ease;
}

#english-word button:hover {
    border-color: var(--accent);
    background-color: var(--surface);
    transform: none;
}

/* ===========================
   BOTONES ESPAÑOL
   =========================== */

#spanish-words {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
    width: 100%;
}

#spanish-words button {
    padding: 30px 20px;
    font-size: 26px;
    background-color: var(--surface);
    color: var(--text-primary);
    border: 2px solid var(--border);
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.2s ease;
    min-height: 120px;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
}

/* Hover normal */
#spanish-words button:hover {
    border-color: var(--accent);
    background-color: var(--border);
    transform: translateY(-3px);
}

#spanish-words button:active {
    transform: translateY(0);
}

/* ===========================
   ❌ ESTADO ERROR
   =========================== */

#spanish-words button.wrong {
    background-color: #3a0f0f;
    border-color: #ff4d4d;
    color: #ffb3b3;
    transform: none;
    animation: shake 0.35s;
}

/* Anula hover cuando está mal */
#spanish-words button.wrong:hover {
    background-color: #3a0f0f;
    border-color: #ff4d4d;
    transform: none;
}

/* ===========================
   ANIMACIÓN
   =========================== */

@keyframes shake {
    0% {
        transform: translateX(0);
    }

    20% {
        transform: translateX(-4px);
    }

    40% {
        transform: translateX(4px);
    }

    60% {
        transform: translateX(-4px);
    }

    80% {
        transform: translateX(4px);
    }

    100% {
        transform: translateX(0);
    }
}

/* ===========================
   RESPONSIVE
   =========================== */

@media (max-width: 768px) {
    #words {
        padding: 20px;
        gap: 30px;
    }

    #english-word button {
        padding: 30px 15px;
        font-size: 34px;
    }

    #spanish-words {
        grid-template-columns: 1fr;
        gap: 15px;
    }

    #spanish-words button {
        padding: 24px 15px;
        font-size: 22px;
        min-height: 100px;
    }
}

@media (max-width: 480px) {
    #words {
        padding: 15px;
        gap: 25px;
    }

    #english-word button {
        padding: 25px 12px;
        font-size: 28px;
    }

    #spanish-words button {
        padding: 20px 12px;
        font-size: 20px;
        min-height: 90px;
    }
}
</style>