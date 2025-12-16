<script setup>
import { ref } from 'vue';

const irregularVerbs = [
    {
        infinitive: "be",
        past: "was / were",
        participle: "been",
        spanish: "ser / estar"
    },
    {
        infinitive: "beat",
        past: "beat",
        participle: "beaten",
        spanish: "golpear / vencer"
    },
    {
        infinitive: "become",
        past: "became",
        participle: "become",
        spanish: "llegar a ser"
    },
    {
        infinitive: "begin",
        past: "began",
        participle: "begun",
        spanish: "empezar"
    },
    {
        infinitive: "bet",
        past: "bet",
        participle: "bet",
        spanish: "apostar"
    },
    {
        infinitive: "bite",
        past: "bit",
        participle: "bitten",
        spanish: "morder"
    },
    {
        infinitive: "bleed",
        past: "bled",
        participle: "bled",
        spanish: "sangrar"
    },
    {
        infinitive: "blow",
        past: "blew",
        participle: "blown",
        spanish: "soplar"
    },
    {
        infinitive: "break",
        past: "broke",
        participle: "broken",
        spanish: "romper"
    },
    {
        infinitive: "bring",
        past: "brought",
        participle: "brought",
        spanish: "traer"
    },
    {
        infinitive: "build",
        past: "built",
        participle: "built",
        spanish: "construir"
    },
    {
        infinitive: "burn",
        past: "burnt / burned",
        participle: "burnt / burned",
        spanish: "quemar"
    },
    {
        infinitive: "buy",
        past: "bought",
        participle: "bought",
        spanish: "comprar"
    },
    {
        infinitive: "catch",
        past: "caught",
        participle: "caught",
        spanish: "atrapar"
    },
    {
        infinitive: "choose",
        past: "chose",
        participle: "chosen",
        spanish: "elegir"
    },
    {
        infinitive: "come",
        past: "came",
        participle: "come",
        spanish: "venir"
    },
    {
        infinitive: "cost",
        past: "cost",
        participle: "cost",
        spanish: "costar"
    },
    {
        infinitive: "cut",
        past: "cut",
        participle: "cut",
        spanish: "cortar"
    },
    {
        infinitive: "deal",
        past: "dealt",
        participle: "dealt",
        spanish: "tratar / repartir"
    },
    {
        infinitive: "dig",
        past: "dug",
        participle: "dug",
        spanish: "cavar"
    },
    {
        infinitive: "do",
        past: "did",
        participle: "done",
        spanish: "hacer"
    },
    {
        infinitive: "draw",
        past: "drew",
        participle: "drawn",
        spanish: "dibujar"
    },
    {
        infinitive: "dream",
        past: "dreamt / dreamed",
        participle: "dreamt / dreamed",
        spanish: "soñar"
    },
    {
        infinitive: "drink",
        past: "drank",
        participle: "drunk",
        spanish: "beber"
    },
    {
        infinitive: "drive",
        past: "drove",
        participle: "driven",
        spanish: "conducir"
    },
    {
        infinitive: "eat",
        past: "ate",
        participle: "eaten",
        spanish: "comer"
    },
    {
        infinitive: "fall",
        past: "fell",
        participle: "fallen",
        spanish: "caer"
    },
    {
        infinitive: "feed",
        past: "fed",
        participle: "fed",
        spanish: "alimentar"
    },
    {
        infinitive: "feel",
        past: "felt",
        participle: "felt",
        spanish: "sentir"
    },
    {
        infinitive: "fight",
        past: "fought",
        participle: "fought",
        spanish: "pelear"
    },
    {
        infinitive: "find",
        past: "found",
        participle: "found",
        spanish: "encontrar"
    },
    {
        infinitive: "fly",
        past: "flew",
        participle: "flown",
        spanish: "volar"
    },
    {
        infinitive: "forget",
        past: "forgot",
        participle: "forgotten",
        spanish: "olvidar"
    },
    {
        infinitive: "forgive",
        past: "forgave",
        participle: "forgiven",
        spanish: "perdonar"
    },
    {
        infinitive: "freeze",
        past: "froze",
        participle: "frozen",
        spanish: "congelar"
    },
    {
        infinitive: "get",
        past: "got",
        participle: "got / gotten",
        spanish: "conseguir / obtener"
    },
    {
        infinitive: "give",
        past: "gave",
        participle: "given",
        spanish: "dar"
    },
    {
        infinitive: "go",
        past: "went",
        participle: "gone",
        spanish: "ir"
    },
    {
        infinitive: "grow",
        past: "grew",
        participle: "grown",
        spanish: "crecer"
    },
    {
        infinitive: "hang",
        past: "hung",
        participle: "hung",
        spanish: "colgar"
    },
    {
        infinitive: "have",
        past: "had",
        participle: "had",
        spanish: "tener / haber"
    },
    {
        infinitive: "hear",
        past: "heard",
        participle: "heard",
        spanish: "oír"
    },
    {
        infinitive: "hide",
        past: "hid",
        participle: "hidden",
        spanish: "esconder"
    },
    {
        infinitive: "hit",
        past: "hit",
        participle: "hit",
        spanish: "golpear"
    },
    {
        infinitive: "hold",
        past: "held",
        participle: "held",
        spanish: "sostener"
    },
    {
        infinitive: "hurt",
        past: "hurt",
        participle: "hurt",
        spanish: "herir / doler"
    },
    {
        infinitive: "keep",
        past: "kept",
        participle: "kept",
        spanish: "guardar / mantener"
    },
    {
        infinitive: "know",
        past: "knew",
        participle: "known",
        spanish: "saber / conocer"
    },
    {
        infinitive: "lead",
        past: "led",
        participle: "led",
        spanish: "liderar"
    },
    {
        infinitive: "learn",
        past: "learnt / learned",
        participle: "learnt / learned",
        spanish: "aprender"
    },
    {
        infinitive: "leave",
        past: "left",
        participle: "left",
        spanish: "dejar / irse"
    },
    {
        infinitive: "lend",
        past: "lent",
        participle: "lent",
        spanish: "prestar"
    },
    {
        infinitive: "let",
        past: "let",
        participle: "let",
        spanish: "permitir / dejar"
    },
    {
        infinitive: "lie",
        past: "lay",
        participle: "lain",
        spanish: "tumbarse / echarse"
    },
    {
        infinitive: "light",
        past: "lit",
        participle: "lit",
        spanish: "encender"
    },
    {
        infinitive: "lose",
        past: "lost",
        participle: "lost",
        spanish: "perder"
    },
    {
        infinitive: "make",
        past: "made",
        participle: "made",
        spanish: "hacer / fabricar"
    },
    {
        infinitive: "mean",
        past: "meant",
        participle: "meant",
        spanish: "significar"
    },
    {
        infinitive: "meet",
        past: "met",
        participle: "met",
        spanish: "conocer / reunirse"
    },
    {
        infinitive: "pay",
        past: "paid",
        participle: "paid",
        spanish: "pagar"
    },
    {
        infinitive: "put",
        past: "put",
        participle: "put",
        spanish: "poner"
    },
    {
        infinitive: "read",
        past: "read (red)",
        participle: "read (red)",
        spanish: "leer"
    },
    {
        infinitive: "ride",
        past: "rode",
        participle: "ridden",
        spanish: "montar"
    },
    {
        infinitive: "ring",
        past: "rang",
        participle: "rung",
        spanish: "sonar / llamar"
    },
    {
        infinitive: "rise",
        past: "rose",
        participle: "risen",
        spanish: "levantarse / subir"
    },
    {
        infinitive: "run",
        past: "ran",
        participle: "run",
        spanish: "correr"
    },
    {
        infinitive: "say",
        past: "said",
        participle: "said",
        spanish: "decir"
    },
    {
        infinitive: "see",
        past: "saw",
        participle: "seen",
        spanish: "ver"
    },
    {
        infinitive: "sell",
        past: "sold",
        participle: "sold",
        spanish: "vender"
    },
    {
        infinitive: "send",
        past: "sent",
        participle: "sent",
        spanish: "enviar"
    },
    {
        infinitive: "set",
        past: "set",
        participle: "set",
        spanish: "fijar / poner"
    },
    {
        infinitive: "shake",
        past: "shook",
        participle: "shaken",
        spanish: "agitar / sacudir"
    },
    {
        infinitive: "shine",
        past: "shone",
        participle: "shone",
        spanish: "brillar"
    },
    {
        infinitive: "shoot",
        past: "shot",
        participle: "shot",
        spanish: "disparar"
    },
    {
        infinitive: "show",
        past: "showed",
        participle: "shown",
        spanish: "mostrar"
    },
    {
        infinitive: "shut",
        past: "shut",
        participle: "shut",
        spanish: "cerrar"
    },
    {
        infinitive: "sing",
        past: "sang",
        participle: "sung",
        spanish: "cantar"
    },
    {
        infinitive: "sink",
        past: "sank",
        participle: "sunk",
        spanish: "hundir"
    },
    {
        infinitive: "sit",
        past: "sat",
        participle: "sat",
        spanish: "sentarse"
    },
    {
        infinitive: "sleep",
        past: "slept",
        participle: "slept",
        spanish: "dormir"
    },
    {
        infinitive: "slide",
        past: "slid",
        participle: "slid",
        spanish: "deslizar"
    },
    {
        infinitive: "smell",
        past: "smelt / smelled",
        participle: "smelt / smelled",
        spanish: "oler"
    },
    {
        infinitive: "speak",
        past: "spoke",
        participle: "spoken",
        spanish: "hablar"
    },
    {
        infinitive: "spell",
        past: "spelt / spelled",
        participle: "spelt / spelled",
        spanish: "deletrear"
    },
    {
        infinitive: "spend",
        past: "spent",
        participle: "spent",
        spanish: "gastar"
    },
    {
        infinitive: "spill",
        past: "spilt / spilled",
        participle: "spilt / spilled",
        spanish: "derramar"
    },
    {
        infinitive: "spoil",
        past: "spoilt / spoiled",
        participle: "spoilt / spoiled",
        spanish: "estropear / mimar"
    },
    {
        infinitive: "stand",
        past: "stood",
        participle: "stood",
        spanish: "estar de pie"
    },
    {
        infinitive: "steal",
        past: "stole",
        participle: "stolen",
        spanish: "robar"
    },
    {
        infinitive: "stick",
        past: "stuck",
        participle: "stuck",
        spanish: "pegar (adherir)"
    },
    {
        infinitive: "swim",
        past: "swam",
        participle: "swum",
        spanish: "nadar"
    },
    {
        infinitive: "take",
        past: "took",
        participle: "taken",
        spanish: "tomar / llevar"
    },
    {
        infinitive: "teach",
        past: "taught",
        participle: "taught",
        spanish: "enseñar"
    },
    {
        infinitive: "tear",
        past: "tore",
        participle: "torn",
        spanish: "rasgar"
    },
    {
        infinitive: "tell",
        past: "told",
        participle: "told",
        spanish: "contar / decir"
    },
    {
        infinitive: "think",
        past: "thought",
        participle: "thought",
        spanish: "pensar"
    },
    {
        infinitive: "throw",
        past: "threw",
        participle: "thrown",
        spanish: "lanzar / tirar"
    },
    {
        infinitive: "understand",
        past: "understood",
        participle: "understood",
        spanish: "entender"
    },
    {
        infinitive: "wake",
        past: "woke",
        participle: "woken",
        spanish: "despertar"
    },
    {
        infinitive: "wear",
        past: "wore",
        participle: "worn",
        spanish: "llevar puesto"
    },
    {
        infinitive: "win",
        past: "won",
        participle: "won",
        spanish: "ganar"
    },
    {
        infinitive: "write",
        past: "wrote",
        participle: "written",
        spanish: "escribir"
    }
];

const guessPastVerb = ref("")
const guessParticileVerb = ref("")
const randomVerb = ref();

const isPastCorrect = ref(null); 
const isParticipleCorrect = ref(null);


function randomIndex() {
    randomVerb.value = irregularVerbs[Math.floor(Math.random() * irregularVerbs.length)];
     isPastCorrect.value = null;
     isParticipleCorrect.value = null;
}

randomIndex();


function checkWord() {
  const pastCorrect = guessPastVerb.value === randomVerb.value.past;
  const participleCorrect = guessParticileVerb.value === randomVerb.value.participle;

  isPastCorrect.value = pastCorrect;
  isParticipleCorrect.value = participleCorrect;

  if (pastCorrect && participleCorrect) {
    guessPastVerb.value = "";
    guessParticileVerb.value = "";
    randomIndex();
  }
}

function giveSolution() {
    guessPastVerb.value = randomVerb.value.past
    guessParticileVerb.value = randomVerb.value.participle
}

</script>

<template>
    <div>
        <p class="irregular-verb">{{ randomVerb.infinitive }}</p>
        <input type="text" v-model="guessPastVerb" placeholder="Pasado" :class="{
            wrong: isPastCorrect === false,
            correct: isPastCorrect === true
        }"></input>
        <input type="text" v-model="guessParticileVerb" placeholder="Participio":class="{
            wrong: isParticipleCorrect === false,
            correct: isParticipleCorrect === true
        }"></input>
        <p class="irregular-verb">{{ randomVerb.spanish }}</p>
        <input type="button" value="Comprobar" @click="checkWord()"></input>
        <input type="button" value="Solución" @click="giveSolution()"></input>
    </div>


</template>

<style scoped>
/* * 1. Configuración del Contenedor Principal
 * Mantenemos el diseño compacto y centrado (max-width: 320px)
 */
div {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    max-width: 320px;
    margin: 30px auto;
    gap: 15px; /* Espacio vertical entre elementos */
}

/* * 2. Tipografía de los Verbos
 */

/* Verbo Infinitivo (Principal) */
p.irregular-verb:first-of-type {
    font-size: 36px;
    font-weight: bold;
    color: var(--primary-color, #8ab4f8);
    margin: 0;
    text-shadow: 0 0 5px var(--shadow-color, rgba(0, 0, 0, 0.4));
    text-transform: lowercase;
}

/* Traducción al Español (Secundario) */
p.irregular-verb:nth-of-type(2) {
    font-size: 20px;
    color: var(--text-color, #e0e0e0);
    margin: 5px 0 15px 0;
    font-style: italic;
    opacity: 0.9;
}

/* * 3. Estilos de los Inputs de Texto (Past & Participle)
 */
input[type="text"] {
    background-color: var(--card-bg, #1e1e1e);
    color: var(--text-color, #e0e0e0);
    border: 2px solid var(--primary-color, #8ab4f8);
    width: 100%;
    padding: 12px 15px;
    border-radius: 10px;
    font-size: 18px;
    text-align: center;
    box-shadow: 0 2px 8px var(--shadow-color, rgba(0, 0, 0, 0.4));
    transition: all 0.2s ease;
    box-sizing: border-box;
    outline: none;
}

input[type="text"]:focus {
    box-shadow: 0 0 0 3px rgba(138, 180, 248, 0.5);
}

/* ✅ Estado CORRECTO (Verde) */
input[type="text"].correct {
    border-color: #2ecc71 !important;
    color: #2ecc71 !important;
    box-shadow: 0 0 0 3px rgba(46, 204, 113, 0.3) !important;
}

/* ❌ Estado INCORRECTO (Rojo + Animación) */
input[type="text"].wrong {
    border-color: #e74c3c !important;
    color: #e74c3c !important;
    box-shadow: 0 0 0 3px rgba(231, 76, 60, 0.3) !important;
    animation: shake 0.4s ease-in-out;
}

/* * 4. Estilos de los Botones (input type="button")
 */
input[type="button"] {
    width: 100%;
    padding: 12px;
    border-radius: 10px;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.1s, background-color 0.2s;
    border: none;
    -webkit-appearance: none; /* Reset para móviles iOS */
}

/* Botón "Comprobar" (Primary) */
input[value="Comprobar"] {
    background-color: var(--primary-color, #8ab4f8);
    color: white;
    box-shadow: 0 4px 10px var(--shadow-color, rgba(0, 0, 0, 0.4));
    margin-top: 10px; /* Separación extra antes de los botones */
}

input[value="Comprobar"]:hover {
    background-color: var(--hover-color, #6a95e0);
}

/* Botón "Solución" (Secondary) */
input[value="Solución"] {
    background-color: transparent;
    color: var(--text-color, #e0e0e0);
    border: 2px solid var(--text-color, #e0e0e0);
    font-size: 16px;
    padding: 10px;
}

input[value="Solución"]:hover {
    background-color: var(--secondary-bg, #282828);
    color: var(--primary-color, #8ab4f8);
    border-color: var(--primary-color, #8ab4f8);
}

input[type="button"]:active {
    transform: scale(0.96);
}

/* * 5. Animación de Error
 */
@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-5px); }
    75% { transform: translateX(5px); }
}

/* * 6. Ajustes Desktop
 */
@media (min-width: 600px) {
    div { max-width: 400px; }
    p.irregular-verb:first-of-type { font-size: 42px; }
}
</style>