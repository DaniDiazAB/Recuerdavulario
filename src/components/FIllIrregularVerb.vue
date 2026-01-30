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
    <h3>Escribe el pasado y el participio del verbo</h3>
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

h3 {
    text-align: center;
    font-size: 28px;
    color: var(--accent);
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid var(--border);
}

div {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 25px;
    max-width: 500px;
    margin: 0 auto;
    padding: 40px;
    background-color: var(--card-bg);
    border-radius: 12px;
    border: 1px solid var(--border);
}

.irregular-verb {
    font-size: 36px;
    font-weight: 600;
    color: white;
    text-align: center;
    margin: 0;
}

.irregular-verb:nth-child(4) {
    color: var(--text-secondary);
    font-size: 28px;
    margin-top: 10px;
}

input[type="text"] {
    width: 100%;
    padding: 20px;
    font-size: 20px;
    background-color: var(--surface);
    border: 2px solid var(--border);
    border-radius: 8px;
    color: var(--text-primary);
    text-align: center;
    transition: all 0.2s ease;
}

input[type="text"]:focus {
    border-color: var(--accent);
    outline: none;
}

input[type="text"].correct {
    border-color: var(--success);
    background-color: rgba(102, 187, 106, 0.1);
}

input[type="text"].wrong {
    border-color: var(--error);
    background-color: rgba(244, 67, 54, 0.1);
}

input[type="button"] {
    width: 100%;
    padding: 18px;
    font-size: 18px;
    font-weight: 600;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s ease;
}

input[type="button"]:first-of-type {
    background-color: var(--accent);
    color: var(--primary-bg);
    margin-top: 10px;
}

input[type="button"]:first-of-type:hover {
    background-color: var(--accent-hover);
    transform: translateY(-2px);
}

input[type="button"]:last-of-type {
    background-color: var(--surface);
    color: var(--text-primary);
    border: 1px solid var(--border);
}

input[type="button"]:last-of-type:hover {
    background-color: var(--border);
    border-color: var(--accent);
    transform: translateY(-2px);
}

@media (max-width: 768px) {
    div {
        padding: 30px 20px;
        gap: 20px;
    }
    
    .irregular-verb {
        font-size: 32px;
    }
    
    .irregular-verb:nth-child(4) {
        font-size: 24px;
    }
    
    input[type="text"] {
        padding: 18px;
        font-size: 18px;
    }
    
    input[type="button"] {
        padding: 16px;
        font-size: 17px;
    }
}

@media (max-width: 480px) {
    div {
        padding: 25px 15px;
        gap: 18px;
    }
    
    .irregular-verb {
        font-size: 28px;
    }
    
    .irregular-verb:nth-child(4) {
        font-size: 22px;
    }
    
    input[type="text"] {
        padding: 16px;
        font-size: 17px;
    }
    
    input[type="button"] {
        padding: 15px;
        font-size: 16px;
    }
}

</style>