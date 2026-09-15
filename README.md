# 📚 Recuerdavulario

**Recuerdavulario** es una aplicación web hecha con **Vue 3** para practicar y memorizar vocabulario de inglés, centrada especialmente en niveles **B2, C1 y C2**, a través de una serie de juegos interactivos (adivinar traducciones, verbos irregulares, escribir la palabra correcta, enlazar parejas, diccionario, etc.).

No está pensada para empezar desde cero con el inglés (no incluye vocabulario básico ni explicaciones de gramática), pero cualquiera puede clonar el proyecto y conectarlo a su propia base de datos de palabras.

---

## 🎯 Idea del proyecto

El objetivo es convertir el repaso de vocabulario en algo activo en vez de pasivo: en lugar de leer listas de palabras, el usuario juega contra sí mismo (adivinando traducciones, rellenando verbos, enlazando parejas...) para forzar la memorización.

Las palabras se sirven desde una API propia (PHP + MySQL), y el frontend en Vue consume esos datos y los reparte entre los distintos componentes de juego.

---

## 🚀 Características

- 🎮 Juego de adivinanza de vocabulario (inglés ↔ español)
- 🔄 Comparación de pasado simple y participio de verbos irregulares
- ✍️ Modo "escribe la palabra"
- 🔗 Modo "enlazar palabras"
- 📖 Vista de diccionario
- 📡 Datos servidos desde una API centralizada
- ⚡ Construido con Vue 3 (Composition API) y Vite

---

## 🛠️ Tecnologías utilizadas

- **Vue 3** + **Composition API** (`<script setup>`)
- **JavaScript (ES6+)**
- **Vite** como entorno de desarrollo
- **PHP + MySQL** para la API que sirve el vocabulario

---

## 📂 Estructura del proyecto

```
src/
├── components/
│   ├── EnglishGuess.vue
│   ├── SpanishGuess.vue
│   ├── TwentyWords.vue
│   ├── IrregularVerbs.vue
│   ├── WriteWord.vue
│   ├── FIllIrregularVerb.vue
│   ├── LinkWords.vue
│   ├── Diccionary.vue
│   └── TitleComponent.vue
├── App.vue
└── main.js
public/
└── api/
    └── getData.php
```

---

## 💻 Descargar el proyecto para modificarlo

1. **Clona el repositorio:**

   ```bash
   git clone https://github.com/tu-usuario/recuerdavulario.git
   cd recuerdavulario
   ```

2. **Instala las dependencias** (necesitas [Node.js](https://nodejs.org/) instalado):

   ```bash
   npm install
   ```

3. **Configura la API:**

   El frontend consume el vocabulario desde una API PHP (`public/api/getData.php`), que necesita conectarse a una base de datos MySQL. Si vas a usar tu propia base de datos:

   - Edita `public/api/getData.php` con tus propias credenciales de conexión.
   - ⚠️ **No subas nunca credenciales reales al repositorio.** Usa variables de entorno o un archivo de configuración fuera del control de versiones (añádelo a `.gitignore`).
   - Actualiza la constante `API_URL` en `src/App.vue` para que apunte a tu propia API.

4. **Arranca el servidor de desarrollo:**

   ```bash
   npm run dev
   ```

   Por defecto se abrirá en `http://localhost:5173`.

5. **Genera la build de producción** cuando quieras desplegar:

   ```bash
   npm run build
   ```

   Esto genera una carpeta `dist/` lista para subir a cualquier hosting estático.

---

## ☁️ Desplegar en la nube

Este proyecto tiene dos partes que hay que desplegar por separado: el **frontend** (Vue, estático) y el **backend** (API en PHP + base de datos MySQL).

### Frontend (Vue) — opciones gratuitas y sencillas

- **GitHub Pages**
  1. Ejecuta `npm run build` para generar la carpeta `dist/`.
  2. Sube el contenido de `dist/` a la rama `gh-pages` de tu repositorio (puedes usar la acción [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages) para automatizarlo con GitHub Actions).
  3. Activa GitHub Pages en la configuración del repositorio, apuntando a esa rama.

- **Vercel / Netlify**
  1. Conecta tu repositorio de GitHub directamente desde el panel de Vercel o Netlify.
  2. Configura el comando de build como `npm run build` y el directorio de salida como `dist`.
  3. Cada `push` a la rama principal desplegará automáticamente una nueva versión.

### Backend (API en PHP + MySQL)

Como el proyecto usa PHP y MySQL, necesitas un hosting que soporte ambos. Algunas opciones:

- Un hosting compartido tradicional con soporte PHP/MySQL (tipo cPanel).
- Servicios como **Hostinger**, **000webhost** o similares para proyectos pequeños.
- Si prefieres todo en un mismo proveedor moderno, plataformas como **Railway** o **Render** permiten desplegar PHP junto a una base de datos MySQL gestionada.

Pasos generales:

1. Sube `public/api/getData.php` (y cualquier otro script de la API) a tu servidor PHP.
2. Crea la base de datos MySQL y la tabla de vocabulario.
3. Configura las credenciales de conexión **como variables de entorno o en un archivo fuera del repositorio**, nunca en texto plano dentro del código versionado.
4. Actualiza la constante `API_URL` en `src/App.vue` (antes de hacer el build del frontend) para que apunte a la URL pública de tu API.

---

## 🔐 Nota de seguridad

El archivo `public/api/getData.php` contiene la lógica de conexión a la base de datos. Si vas a usar este proyecto como base para el tuyo:

- No dejes credenciales de acceso a la base de datos escritas directamente en el código.
- Usa un usuario de MySQL de solo lectura (`SELECT`) para esta API, en vez de un usuario con permisos totales.
- Revisa la configuración de CORS si vas a exponer la API públicamente.

---

## 📈 Mejoras futuras

- Nuevos juegos (relacionar palabras, modo "examen"...)
- Repetición espaciada (SRS) para priorizar palabras que más cuestan
- Guardado de progreso (localStorage o backend de usuarios)
- Estadísticas de aciertos/fallos
- Audio/pronunciación de las palabras
- Soporte offline (PWA)

---

## 📄 Licencia

Se autoriza cualquier modificación y uso de este software.

---

## ✨ Autor

Desarrollado por **Daniel Díaz Honrubia**
