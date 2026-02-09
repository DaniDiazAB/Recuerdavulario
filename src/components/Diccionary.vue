<script setup>
import { inject, watch, ref, computed } from 'vue';

const arrayWords = inject('arrayWords')
const search = ref('')
const words = computed(() => {
    return arrayWords.value
        .slice()
        .sort((a, b) => a.ingles_palabra.localeCompare(b.ingles_palabra));
});
const currentPage = ref(1);
const wordsPage = ref(20);
const filteredWords = computed(() => {
    const searchText = normalize(search.value)
    return words.value.filter(word =>
        normalize(word.ingles_palabra).includes(searchText) ||
        normalize(word.traduccion_palabra).includes(searchText)
    )
})

const paginatedWords = computed(() => {
    const start = (currentPage.value - 1) * wordsPage.value;
    const end = start + wordsPage.value;
    return filteredWords.value.slice(start, end);
});

const totalPages = computed(() => {
    return Math.ceil(filteredWords.value.length / wordsPage.value);
});


watch([filteredWords, wordsPage], () => {
  currentPage.value = 1;
});


function normalize(text = '') {
    return String(text)
        .toLowerCase()
        .normalize('NFD')
        .replace(/[\u0300-\u036f]/g, '')
}

</script>

<template>
    <div class="game-card dictionary-container">
        <div class="header-section">
            <h3 class="section-title">Diccionario</h3>
            <div class="controls-container">
                <input 
                    v-model="search" 
                    placeholder="Buscar palabra..." 
                    class="input-field search-input"
                />
                <div class="pagination-controls">
                    <label for="items-per-page">Resultados:</label>
                    <select id="items-per-page" v-model="wordsPage" class="select-field">
                        <option value="20">20</option>
                        <option value="40">40</option>
                        <option value="60">60</option>
                        <option value="80">80</option>
                        <option value="100">100</option>
                    </select>
                </div>
            </div>
        </div>

        <ul class="word-list">
            <li v-for="word in paginatedWords" :key="word.ingles_palabra" class="word-item">
                <span class="diccionary-word english">{{ word.ingles_palabra }}</span>
                <span class="separator">•</span>
                <span class="diccionary-word spanish">{{ word.traduccion_palabra }}</span>
            </li>
            <li v-if="paginatedWords.length === 0" class="no-results">
                No se encontraron palabras.
            </li>
        </ul>

        <div class="pagination">
            <button 
                class="btn-nav" 
                @click="currentPage--" 
                :disabled="currentPage === 1"
            >
                Anterior
            </button>
            
            <span class="page-info">{{ currentPage }} / {{ totalPages || 1 }}</span>
            
            <button 
                class="btn-nav" 
                @click="currentPage++" 
                :disabled="currentPage === totalPages || totalPages === 0"
            >
                Siguiente
            </button>
        </div>
    </div>
</template>

<style scoped>
.dictionary-container {
    display: flex;
    flex-direction: column;
    min-height: 650px; 
}

.header-section {
    flex: 0 0 auto; 
}

.word-list {
    flex: 1 0 auto; 
    
    list-style: none;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); 
    align-content: start; 
    gap: 12px;
    margin-bottom: 24px;
}

.pagination {
    flex: 0 0 auto;
    margin-top: auto; 
    
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    padding-top: 20px;
    border-top: 1px solid var(--border);
}


.section-title {
    color: var(--text-primary);
    margin-bottom: 24px;
    font-size: 24px;
    text-align: center;
    font-weight: 600;
    border-bottom: 2px solid var(--border);
    padding-bottom: 12px;
}

.controls-container {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin-bottom: 24px;
}

@media (min-width: 600px) {
    .controls-container {
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }
}

.search-input {
    flex: 1;
    min-width: 200px;
}

.pagination-controls {
    display: flex;
    align-items: center;
    gap: 10px;
    color: var(--text-secondary);
    font-size: 14px;
}

.select-field {
    background-color: var(--surface);
    color: var(--text-primary);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 8px 12px;
    outline: none;
    cursor: pointer;
    transition: border-color 0.2s;
}

.select-field:focus {
    border-color: var(--accent);
}

.word-item {
    background-color: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 12px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    transition: all 0.2s ease;
    /* Altura fija para evitar saltos si el contenido varía ligeramente */
    height: 50px; 
}

.word-item:hover {
    border-color: var(--accent);
    transform: translateY(-2px);
    background-color: #262c3d;
}

.diccionary-word {
    font-size: 15px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 45%;
}

.diccionary-word.english {
    font-weight: 600;
    color: var(--accent);
}

.diccionary-word.spanish {
    color: var(--text-secondary);
    text-align: right;
}

.separator {
    color: var(--border);
    font-size: 10px;
    margin: 0 8px;
}

.no-results {
    grid-column: 1 / -1;
    text-align: center;
    color: var(--text-secondary);
    padding: 20px;
    font-style: italic;
}

.btn-nav {
    background-color: var(--surface);
    color: var(--text-primary);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 8px 16px;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.2s ease;
}

.btn-nav:hover:not(:disabled) {
    background-color: var(--accent);
    color: var(--primary-bg);
    border-color: var(--accent);
}

.btn-nav:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    background-color: var(--primary-bg);
}

.page-info {
    color: var(--text-secondary);
    font-variant-numeric: tabular-nums;
    font-weight: 500;
}
</style>