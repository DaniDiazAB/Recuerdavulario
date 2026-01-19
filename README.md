# Recueldavulario

Recueldavulario es una aplicación web desarrollada con **Vue 3** cuyo objetivo es ayudarte a practicar y memorizar vocabulario, centrándose especialmente en **vocavulario B2, C1 y C2** mediante un sistema de juegos interactivos.

La base de datos (que más adelante estará disponible para su descarga) no está pensada para personas que quieran empezar con el inglés, ya que apenas hay palabras básicas del inglés y no hay explicación de tiempos verbales, aunque no se descarta que en el futuro se implemente. De todas formas, cualquier persona puede coger este proyecto y usar su propia base de datos.

---

## 🚀 Características

* 🎮 Juego de adivinanza de verbos en inglés
* 🔄 Comparación de pasado simple y participio
* 📡 Consumo de datos desde una API centralizada
* ♻️ Estado compartido entre componentes
* ⚡ Construido con Vue 3 y Composition API
* 🧩 Componentes reutilizables y desacoplados

---

## 🛠️ Tecnologías utilizadas

* **Vue 3**
* **Composition API** (`<script setup>`)
* **JavaScript (ES6+)**
* **Vite** (entorno de desarrollo)
* **API REST** para obtención de verbos

---

## 📂 Estructura del proyecto

```
src/
├── components/
│   ├── EnglishGuess.vue
│   ├── SpanishGuess.vue
│   └── TitleComponent.vue
│   └── Demás componentes
├── App.vue
└── main.js
```

* `App.vue`: carga inicial de datos desde la API y distribución del estado.
* `components/`: componentes del juego y la interfaz.

---

## 📦 Instalación y uso

Clona el repositorio:

```bash
git clone https://github.com/tu-usuario/recueldavulario.git
```

Accede al proyecto:

```bash
cd recueldavulario
```

Instala las dependencias:

```bash
npm install
```

Inicia el servidor de desarrollo:

```bash
npm run dev
```

---

## 📈 Mejoras futuras

* Nuevos juegos (relacionar palabras, "examen"...).
* Mejoras en el código y CSS.
* Mejoras varias en los juegos.

---

## 📄 Licencia

Autorizo cualquier modificación y uso de este Software.

---

## ✨ Autor

Desarrollado por Daniel Díaz Honrubia

