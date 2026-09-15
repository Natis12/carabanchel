# Sergio Fit — Guía Técnica y Arquitectura de la Aplicación

> **Documento de referencia rápida** para mantenimiento, ampliación y modificaciones directas sin necesidad de leer los más de 3.000 líneas de código de `index.html`.

---

## 1. Visión General del Proyecto

- **Propósito**: Aplicación web progresiva (PWA) de entrenamiento funcional por intervalos (circuito de estaciones), orientada y adaptada para mujeres de 40 a 60 años.
- **Funcionamiento**: **100% Offline** (Service Worker con caché completa de fuentes, estilos e ilustraciones).
- **Arquitectura**: **Single-File Architecture** en `index.html` (HTML5, Tailwind CSS vía CDN, Web Audio API y JavaScript Vanilla sin dependencias externas pesadas).

---

## 2. Mapa de Archivos del Directorio

| Archivo | Rol / Función |
| :--- | :--- |
| **`index.html`** | **Núcleo de la aplicación en producción**. Contiene la vista del temporizador, el panel de configuración, los modales, la base de datos de 125 ejercicios y el motor del timer. |
| **`sw.js`** | Service Worker para funcionamiento offline inmediato, almacenamiento en caché y control de ciclo de vida. |
| **`manifest.json`** | Manifiesto PWA para instalación nativa en iOS (Safari "Añadir a pantalla de inicio") y Android. |
| **`modelos_timer.html`** | **Banco de pruebas / Showroom visual**. Aquí se diseñan, comparan y validan nuevas variantes del temporizador antes de transferirlas a `index.html`. |
| **`dumbbell_data.json`** | Catálogo estructurado con SVGs biomecánicos y datos de los ejercicios con mancuernas. |
| **`icon-192.png` / `512.png`** | Iconos oficiales de la PWA. |

---

## 3. Estructura Visual y Pantallas (`index.html`)

La aplicación se divide en dos vistas principales gobernadas por `setMainView(viewName)`:

```
┌─────────────────────────────────────────────────────────────┐
│ CABECERA: [⚡ SERGIO FIT] [OFFLINE]  [☀️/🌙] [⏱️ Timer|⚙️ Ajustes]│
├─────────────────────────────────────────────────────────────┤
│ CONTENEDOR PRINCIPAL (#deviceCard):                         │
│                                                             │
│  [ VISTA 1: #viewTimer ]        [ VISTA 2: #viewConfig ]    │
│  - Barra flotante superior      - Selector de Grupo         │
│    (Audio, ↺, ⏮, ⏭, ⏳)           (Pilates / Zumba)        │
│  - Temporizador circular 60 FPS - Materiales activos        │
│  - Disco interior con fase/dígitos - Series y Tiempos       │
│  - Dibujo animado + Título      - Botón Generar Circuito    │
│  - Dock Inferior V29:           - Listado 125 ejercicios    │
│    [EJERCICIO] [PLAY] [RONDAS]   - Sustituir / Foto propia   │
│                                 - Circuitos Favoritos       │
└─────────────────────────────────────────────────────────────┘
```

---

## 4. Componentes Clave del Temporizador (`#viewTimer`)

### 4.1. Barra Flotante Superior
- **Píldora de controles izquierda**:
  - `toggleMute()`: Alterna audio (`🔊` / `🔇`) e interactúa con el `masterGain` del sintetizador.
  - `resetWorkout()`: Reinicia a la estación 1 y ronda 1 en estado `READY`.
  - `skipStep(-1)` / `skipStep(1)`: Salta de ejercicio hacia atrás o hacia adelante.
- **Píldora derecha (`#m1Total`)**: Muestra en tiempo real la cuenta atrás matemática del tiempo total de la clase (`formatTimeMMSS(computeTotalRemainingSeconds())`).

### 4.2. Círculo Radial a 60 FPS
- **SVG ViewBox `0 0 280 280`**:
  - Radio `r=124`, longitud circunferencial `CIRCLE_CIRCUMFERENCE = 779.12`.
  - Avance continuo calculado mediante `requestAnimationFrame` (`offset = CIRCLE_CIRCUMFERENCE * (1 - fraction)`). Cero saltos discretos de 1 segundo.
- **Pulso de Latido por Segundo**: En cada tick de segundo en fase de Trabajo (`WORK`), se dispara la animación CSS `.zoom-pulse-active` (`scale(1.026)` durante 0.36s) en `#m1CircleWrapper`.
- **Fases y Colores Dinámicos**:
  - `verde` (`WORK`): Fondo radial esmeralda `#064e3b`, acento neón `#10b981`.
  - `amarillo` (`REST_SERIES` / `PREP`): Fondo ámbar `#78350f`, acento `#f59e0b`.
  - `rojo` (`REST_ROUND`): Fondo burdeos `#7f1d1d`, acento `#ef4444`.

### 4.3. Escenario de Ilustración y Título
- **En Trabajo**:
  - Ilustración técnica con animación de dos pasos (`gif-step1` y `gif-step2`) a ritmo desacoplado de 3 segundos (`--gif-duration: 3s`).
  - Badge de material: ej. `MANCUERNAS` en píldora blanca translúcida.
  - Título del ejercicio: Tipografía multilínea atlética retro **Monoton** (`.font-exercise`).
- **En Descanso**:
  - Ilustración del siguiente ejercicio **flotante y sin bordes**, limpiada con `cleanSvgForRest()` para eliminar fondos de tarjeta y etiquetas.
  - Badge: `SIGUIENTE: [MATERIAL]` en color ámbar.

### 4.4. Dock Inferior Titanium Precision (V29)
1. **Columna Izquierda (`EJERCICIO`)**:
   - Recuadro en titanio CNC con bisel diamond-cut dorado (`.recuadro-titanium-ciclos`).
   - Número activo multilínea Modelo D (`#m1CurrentCycle`) centrado matemática y ópticamente.
   - Total de estaciones (`#m1TotalCycles`, ej: `/6`) ubicado abajo junto a la línea base.
   - Micro-barra segmentada dinámica (`#m1ExerciseSegments`) con pastillas doradas activas.
   - Etiqueta exterior centrada debajo: `EJERCICIO`.
2. **Columna Central (Botón Play / Pausa Gigante)**:
   - Diámetro heroico: `w-[112px] h-[112px] sm:w-[120px] sm:h-[120px]`.
   - Acabado concéntrico en titanio táctil (`.titanium-play-outer` y `.titanium-play-inner`).
   - **Completamente limpio sin textos** (`RUNNING` / `PAUSED`).
   - Iconos SVG de 52px (`#m1PlaySvg` y `#m1PauseSvg`) centrados con resplandor neón activo de fase.
3. **Columna Derecha (`RONDAS`)**:
   - Recuadro en titanio CNC con bisel diamond-cut azul zafiro (`.recuadro-titanium-rondas`).
   - Número activo multilínea Modelo D (`#m1CurrentRound`) centrado.
   - Total de rondas (`#m1TotalRounds`, ej: `/3`) en la línea base inferior.
   - Micro-LEDs dinámicos (`#m1RoundLeds`) con diodos azules activos.
   - Etiqueta exterior centrada debajo: `RONDAS`.

---

## 5. Estado Global y Datos (`appStore` & `circuitConfig`)

### 5.1. Variables Principales de Estado en JavaScript
```javascript
// Configuración editable de la clase
let circuitConfig = {
  aerobicCount: 3,     // Ejercicios aeróbicos (Cardio)
  strengthCount: 3,    // Ejercicios de fuerza (Tono/Postura)
  rounds: 3,           // Rondas o series completas
  workTime: 30,        // Segundos de trabajo
  restTime: 10,        // Segundos de descanso entre estaciones
  roundRestTime: 20,   // Segundos de descanso al terminar cada ronda
  prepTime: 10         // Segundos de preparación inicial
};

// Materiales disponibles hoy (marcar/desmarcar)
let activeMaterials = {
  esterilla: true,
  kettlebell: true,
  goma: true,
  aro: true,
  mancuernas: true,
  corporal: true
};

// Estado del Temporizador
let timerPhase = 'READY'; // 'READY' | 'PREP' | 'WORK' | 'REST_SERIES' | 'REST_ROUND'
let currentStationIdx = 0; // Índice (0 a activeStations.length - 1)
let currentRound = 1;      // Ronda actual (1 a circuitConfig.rounds)
let isRunning = false;     // Si el timer está reproduciéndose
let timeLeft = 30;         // Segundos restantes de la fase actual
let phaseEndTime = 0;      // Timestamp Date.now() de fin de fase
let rafId = null;          // Identificador de requestAnimationFrame
```

### 5.2. Persistencia en `localStorage` (`sergio_fit_v4`)
- Guarda grupo seleccionado (`pilates` o `zumba`), tema claro/oscuro, materiales marcados, tiempos personalizados, historial de clases completadas y conteo de uso de cada uno de los 125 ejercicios.

---

## 6. Motor del Temporizador y Audio

### 6.1. Bucle Continuo `requestAnimationFrame` + `Date.now()`
- La sincronización se rige por `phaseEndTime = Date.now() + (timeLeft * 1000)`.
- `animationLoop()` calcula `remainingMs = Math.max(0, phaseEndTime - Date.now())`:
  - Si el fotograma pertenece al mismo segundo, solo actualiza la interpolación angular del círculo SVG.
  - Cuando cambia el segundo entero (`remainingSec !== lastSecondReported`):
    - Actualiza `#m1Digits`.
    - Dispara `triggerTrainingZoomPulse()` si la fase es `WORK`.
    - Ejecuta `playBeep()` en los últimos 3 segundos (3, 2, 1).
    - Actualiza el tiempo total restante en `#m1Total`.
  - Cuando `remainingMs <= 0`, ejecuta `playBoxingBell()` y avanza a la siguiente fase con `advancePhase()`.

### 6.2. Motor de Audio Sintetizado (Cero lag, no corta Spotify)
- Sintetizado 100% nativo mediante la API Web Audio (`AudioContext` conectado a un `masterGain` para control de volumen de 0 a 100%).
- **Campana de Boxeo / Gong**: Combinación polifónica armónica de ondas triangulares y senoidales en 587Hz, 880Hz, 1174Hz y 1760Hz con decaimiento exponencial progresivo.

---

## 7. Base de Datos de Ejercicios (125 Adaptados)

Ubicada en `const fullExerciseDatabase`:
- **`aerobic`**: Ejercicios de bajo impacto cardiovascular (Marcha rítmica, V-steps, patinador suave, desplazamientos laterales, etc.).
- **`strength`**: Ejercicios de fuerza funcional, suelo pélvico, abdomen y postura (Puentes de glúteo, elevaciones laterales, flexiones adaptadas, sentadillas con aro/goma, etc.).
- **Atributos de cada ejercicio**:
  ```json
  {
    "id": "m3",
    "name": "Elevaciones Frontales",
    "type": "FUERZA",
    "materialKey": "mancuernas",
    "material": "Mancuernas 2kg",
    "materialIcon": "MAN",
    "cue": "Espalda recta y codos suaves. Eleva solo hasta la altura del pecho.",
    "advanced": "Mantén 1 segundo la contracción arriba."
  }
  ```

---

## 8. Guía de Modificaciones Frecuentes (Cheat Sheet)

### ¿Cómo cambiar los tiempos por defecto?
Edita `let circuitConfig` en la sección de estado JavaScript (aprox. línea 1920 de `index.html`):
```javascript
let circuitConfig = {
  aerobicCount: 3,
  strengthCount: 3,
  rounds: 3,
  workTime: 30,      // <- Cambiar aquí
  restTime: 10,      // <- Cambiar aquí
  roundRestTime: 20, // <- Cambiar aquí
  prepTime: 10       // <- Cambiar aquí
};
```

### ¿Cómo añadir un nuevo ejercicio a la biblioteca?
Inserta un nuevo objeto en `fullExerciseDatabase.aerobic` o `fullExerciseDatabase.strength`. Asegúrate de asignarle un `id` único y un `materialKey` válido (`esterilla`, `kettlebell`, `goma`, `aro`, `mancuernas` o `corporal`).

### ¿Cómo ajustar los estilos del dock inferior?
Los estilos CNC de titanio se definen en las clases CSS del `<style>`:
- `.recuadro-titanium-rondas`: Bisel y aura azul zafiro.
- `.recuadro-titanium-ciclos`: Bisel y aura oro/ámbar para el módulo de Ejercicio.
- `.titanium-play-outer` / `.titanium-play-inner`: Botón central de reproducción.

### ¿Cómo cambiar las fuentes tipográficas?
Las fuentes están enlazadas en el `<head>`:
- `Monoton`: Utilizada por `.font-exercise` para títulos y números activos del dock.
- `JetBrains Mono`: Utilizada para tiempos, dígitos y contadores numéricos.
- `Plus Jakarta Sans`: Utilizada para el cuerpo de texto general.
