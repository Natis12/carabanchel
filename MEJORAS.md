# Sergio Fit — Plan de mejora e Historial de Cambios

**Público objetivo**: Mujeres de 40 a 60 años con nivel inicial de condición física.  
**Entorno**: Clases funcionales en sala/gimnasio con o sin cobertura (100% offline).  
**Criterios biomecánicos**: Cero saltos de impacto, protección lumbar, cervical y de suelo pélvico, sin presses pesados por encima de la cabeza (mancuernas de 2 kg máx).

---

## 1. Estado de los Errores (17/17 Resueltos)

| # | Error detectado | Impacto | Estado | Solución implementada |
|---|-----------------|---------|--------|----------------------|
| 1 | La ilustración se reiniciaba cada segundo: el GIF (1.8 s) nunca mostraba el paso 2 | Alto | **ARREGLADO** | El SVG no se reinyecta si el ejercicio en pantalla es el mismo. Solo cambia la cuenta atrás. |
| 2 | Al pausar, ir a Ajustes y volver al Timer, se perdía el tiempo del ejercicio | Alto | **ARREGLADO** | `timeLeft` se mantiene intacto en pausa entre cambios de pantalla. |
| 3 | Modo offline fallaba: Tailwind CDN y Google Fonts no estaban cacheados | Crítico | **ARREGLADO** | `sw.js` almacena en caché scripts externos, fuentes e iconos tras la primera apertura con red. |
| 4 | `sw.js` cache-first impedía que las actualizaciones llegaran al dispositivo | Alto | **ARREGLADO** | Implementada estrategia network-first para `index.html` con fallback a caché. |
| 5 | `user-scalable=no` bloqueaba el zoom para personas con presbicia/vista cansada | Medio | **ARREGLADO** | Viewport actualizado permitiendo zoom manual (`maximum-scale=3.0`). |
| 6 | Los ajustes (material, tiempos, rondas) no se persistían al cerrar la app | Medio | **ARREGLADO** | Persistencia automática en `localStorage` por perfil activo (`pilates` / `zumba`). |
| 7 | Temporizador con deriva por contar ticks de `setInterval` | Medio | **ARREGLADO** | Temporizador de alta precisión recalculando tiempo restante con `Date.now()`. |
| 8 | Wake Lock (pantalla encendida) se perdía al minimizar o bloquear el móvil | Medio | **ARREGLADO** | Event listener `visibilitychange` reactiva automáticamente el Wake Lock al volver a la app. |
| 9 | `skipStep(+1)` en la última estación de la última ronda volvía a la estación 1 | Bajo | **ARREGLADO** | Se detecta el final del circuito y se invoca limpiamente la finalización del entrenamiento. |
| 10 | Regenerar el circuito con la clase en marcha dejaba índices inconsistentes | Medio | **ARREGLADO** | Se detiene y reinicia el estado de forma segura al regenerar. |
| 11 | `alert()` nativo al terminar congelaba la interfaz y el audio | Bajo | **ARREGLADO** | Sustituido por modal interactivo `#completionModal` con resumen y opciones de guardado. |
| 12 | Ruteo de Web Audio saltaba el `masterGain` (volumen inconsistente) | Bajo | **ARREGLADO** | Todos los osciladores y beeps pasan por `masterGain`. Sonido único de gong metálico. |
| 13 | Marco falso de iPhone ("18:35" y notch) y `min-h-[820px]` desbordando | Medio | **ARREGLADO** | Eliminado el notch y la barra de estado simulada; diseño flexible y responsivo real. |
| 14 | Tipografías enanas (9-11 px) ilegibles a distancia para 40-60 años | Alto | **ARREGLADO** | Tipografías escaladas (mín. 14-16 px en textos, 72-88 px en cuenta atrás, botones >= 48 px). |
| 15 | Fotos personalizadas de ejercicios se perdían al regenerar | Bajo | **ARREGLADO** | Almacenamiento persistente en `localStorage` asociadas al ID del ejercicio (canvas 240 px). |
| 16 | Icono manifest era un JPG de 3000x3000px declarado como 192/512 | Bajo | **ARREGLADO** | Generados `icon-192.png` y `icon-512.png` optimizados y `apple-touch-icon`. |
| 17 | `exercises_data.json` duplicaba la base de datos | Bajo | **ARREGLADO** | Archivo duplicado eliminado; base de datos única y limpia. |

---

## 2. Funcionalidades Implementadas

- **Selector de Grupo dentro de Ajustes**:
  - Se retiró de la cabecera principal y se integró en la sección superior de **Ajustes**.
  - Permite conmutar instantáneamente entre `🧘 Circuito Pilates` y `💃 Circuito Zumba`. Cada grupo mantiene de forma independiente sus materiales seleccionados, tiempos configurados, circuitos favoritos y su propio conteo de ejercicios y fechas.
- **Guardado voluntario al finalizar la clase**:
  - El entrenamiento **NO** se guarda automáticamente al reiniciar o generar.
  - Al completar todas las estaciones y rondas de la sesión, se despliega el modal de fin de clase ofreciendo:
    - `💾 Guardar Entrenamiento`: Suma +1 en el contador de uso de cada ejercicio del circuito, registra la fecha/hora en el historial del perfil activo y lo archiva.
    - `🔄 No guardar y reiniciar`: Reinicia el circuito para otra sesión sin alterar las estadísticas del grupo.
- **Sonido final único: Gong Metálico**:
  - Se fijó la campana de boxeo / gong metálico resonante de Web Audio API como sonido de fin de ronda y fin de entrenamiento.
  - Se eliminaron las opciones superfluas de cambio de sonido en la interfaz de Ajustes.
- **Botón "📋 Listado de Ejercicios (125)" en Ajustes**:
  - Acceso directo a una ventana modal con el catálogo íntegro de los 125 ejercicios.
  - Buscador en tiempo real por nombre, músculo o material.
  - Filtros rápidos: Todos, Pilates, Zumba, Aeróbicos, Fuerza y por material (Mancuernas, Esterilla, Aro, Banda, KB, Corporal).
  - Indicador dinámico por ejercicio: **veces utilizado y fecha del último uso** según el perfil activo (Pilates / Zumba).
  - Ficha expandible con indicación técnica y versión avanzada para alumnas que quieran más intensidad.
- **Mancuernas de 2 kg y 25 Ejercicios Específicos**:
  - Nuevo material seleccionable: `🏋️‍♀️ Mancuernas 2kg` (código `MANC`).
  - 25 ejercicios nuevos (`m1` a `m25`), distribuidos en 13 aeróbicos y 12 de fuerza controlada.
  - Adaptados rigurosamente: mancuernas de 2 kg, movimientos seguros para hombros (cero press militar pesado sobre la cabeza), sin saltos y con apoyo articular.
  - Ilustraciones animadas paso 1 / paso 2 estilo GIF vectorial integradas.
- **Gestión de Circuitos Favoritos**:
  - Posibilidad de guardar el circuito actual con nombre personalizado para repetirlos en futuras clases.
- **Catálogo total de 125 Ejercicios**:
  - 50 ejercicios base originales (ahora con versión avanzada y consejos de postura).
  - 50 ejercicios funcionales de bajo impacto (pared, silla, aro pilates, banda elástica de 10 kg).
  - 25 ejercicios con mancuernas de 2 kg.
