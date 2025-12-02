<script setup>
import { onMounted, ref } from 'vue';

const englishRandomWord = ref("");
const spanishRandomWord = ref("");
const arrayWordsWrong = ref([])
const random = ref();
const arrayWords = ref([])
const API_URL = 'https://danidiaz.site/recuerdavulario/api/getData.php'

onMounted(() => {
    setWords();
})

function setNewTry() {
    getRandom();

    englishRandomWord.value = arrayWords.value[random.value].ingles_palabra
    spanishRandomWord.value = arrayWords.value[random.value].traduccion_palabra

    arrayWordsWrong.value.push(arrayWords.value[random.value].ingles_palabra)
    for (let i = 0; i < 3; i++) {
        getRandom();
        arrayWordsWrong.value.push(arrayWords.value[random.value].ingles_palabra);
    }
    shuffle(arrayWordsWrong.value)
}

async function setWords() {
    try {
        const response = await fetch(API_URL);
        const data = await response.json();
        arrayWords.value = data;
        arrayWordsWrong.value.length = 0;
        setNewTry(); 
    } catch (error) {
        console.error("Error:", error);
    }
}

function shuffle(wordsArray) {
    return wordsArray.sort(() => Math.random() - 0.5);
}

function getRandom() {
    random.value = Math.floor(Math.random() * arrayWords.value.length);
}

function checkWord(word) {
    if (word === englishRandomWord.value) {
        setWords()
    } else {
        alert("Fallo");
    }
}

</script>

<template>
    <div id="words">
        <div id="english-word">
            <button>
                {{ spanishRandomWord }}
            </button>
        </div>

        <div id="spanish-words">
            <button @click="checkWord(arrayWordsWrong[0])">
                {{ arrayWordsWrong[0] }}
            </button>

            <button @click="checkWord(arrayWordsWrong[1])">
                {{ arrayWordsWrong[1] }}

            </button>

            <button @click="checkWord(arrayWordsWrong[2])">
                {{ arrayWordsWrong[2] }}

            </button>

            <button @click="checkWord(arrayWordsWrong[3])">
                {{ arrayWordsWrong[3] }}
            </button>

        </div>
    </div>

</template>

<style>
/* * 1. Definición de Variables CSS para Dark Mode 
 * Usamos @media (prefers-color-scheme: dark) para cambiar los colores.
 */

:root {
  /* Modo Claro (Default) */
  --bg-color: #f4f4f9; /* Fondo muy claro */
  --card-bg: #ffffff;  /* Fondo de las tarjetas/botones */
  --text-color: #1e1e1e; /* Color del texto principal */
  --primary-color: #4a90e2; /* Azul principal */
  --hover-color: #357bd9;  /* Azul oscuro para hover */
  --shadow-color: rgba(0, 0, 0, 0.1);
}

@media (prefers-color-scheme: dark) {
  /* Modo Oscuro */
  :root {
    --bg-color: #121212; /* Fondo muy oscuro */
    --card-bg: #1e1e1e;  /* Fondo de las tarjetas/botones en oscuro */
    --text-color: #e0e0e0; /* Color del texto claro */
    --primary-color: #8ab4f8; /* Azul más claro para contraste */
    --hover-color: #6a95e0;  /* Azul oscuro para hover */
    --shadow-color: rgba(0, 0, 0, 0.4);
  }
}

/* * 2. Estilos Generales y Contenedor Principal
 */

body {
    background-color: var(--bg-color); /* Aplica el fondo del modo oscuro/claro */
    transition: background-color 0.3s; /* Transición suave para el modo oscuro/claro */
    color: var(--text-color);
    font-family: 'Avenir', 'Helvetica', Arial, sans-serif;
    margin: 0;
}

#words {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 40px; /* Aumentado ligeramente para mejor espaciado */
    padding: 20px;
    min-height: 100vh; /* Ocupa al menos toda la altura de la vista */
    box-sizing: border-box;
}

/* * 3. Estilo de la Palabra en Inglés (English Word)
 */

#english-word {
    width: 100%;
    max-width: 400px; /* Limita el ancho en pantallas grandes */
    text-align: center;
}

#english-word button {
    background: var(--primary-color);
    color: var(--text-color); /* Usa el color de texto del modo */
    border: none;
    width: 100%;
    padding: 20px 25px;
    font-size: 24px;
    font-weight: bold;
    border-radius: 12px;
    cursor: default;
    box-shadow: 0 4px 15px var(--shadow-color);
    transition: all 0.3s ease;
    /* Asegura que el color del texto sea visible en el primary-color */
    color: white; 
}

/* * 4. Estilos de las Opciones en Español (Spanish Words)
 */

#spanish-words {
    display: grid;
    /* Por defecto, en móvil, usamos 1 columna */
    grid-template-columns: 1fr; 
    width: 100%;
    max-width: 400px;
    gap: 15px;
}

#spanish-words button {
    background: var(--card-bg);
    border: 2px solid var(--primary-color);
    color: var(--text-color);
    padding: 15px 25px;
    width: 100%;
    border-radius: 10px;
    font-size: 18px;
    cursor: pointer;
    transition: background-color 0.2s, color 0.2s, transform 0.1s;
    box-shadow: 0 2px 8px var(--shadow-color);
    font-weight: 500;
}

/* Efectos de Interacción */
#spanish-words button:hover {
    background: var(--hover-color);
    color: white;
    border-color: var(--hover-color);
}

#spanish-words button:active {
    transform: scale(0.98);
    box-shadow: 0 1px 5px var(--shadow-color);
}


/* * 5. Adaptación a Escritorio (Desktop/Tablet) 
 * Usamos Media Query para cambiar a 2 columnas cuando hay más espacio.
 */

@media (min-width: 600px) {
    #words {
        padding: 60px;
        gap: 50px;
    }

    #english-word button {
        font-size: 28px;
        padding: 25px 50px;
    }

    #spanish-words {
        /* En pantallas más grandes, usamos 2 columnas */
        grid-template-columns: repeat(2, 1fr);
        max-width: 600px;
        gap: 20px;
    }

    #spanish-words button {
        font-size: 20px;
    }
}
</style>