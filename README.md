# Sergio Fit - Carabanchel 🏋️‍♀️⏱️

Aplicación Web Progresiva (PWA) de alta precisión para entrenamientos en circuito, intervalos y clases dirigidas de Pilates, Zumba y Funcional.

Diseñada para funcionar **100% offline** directamente desde cualquier teléfono móvil o tablet (iOS / Android) o navegador de escritorio.

---

## 🚀 Características Principales

- ⏱️ **Timer de Intervalos Profesional**:
  - Cuenta atrás radial continua a 60 FPS con `requestAnimationFrame`.
  - Transiciones de color ambiental (*Verde Esmeralda* en Trabajo, *Ámbar Dorado* en Descanso, *Rojo Rubí* en últimos 3 segundos).
  - Efecto de latido (*heartbeat zoom pulse*) en cada segundo de la fase de esfuerzo.
  - Dock inferior estilo titanio aeroespacial:
    - **Izquierda**: Tarjeta de Estación/Ejercicio actual con barra segmentada.
    - **Centro**: Botón táctil gigante Play/Pausa de 112px con respuesta inmediata.
    - **Derecha**: Tarjeta de Ronda actual con micro-LEDs de progreso.

- 📋 **Dos Modos de Entrenamiento**:
  1. **Modo Guiado**:
     - Catálogo biomecánico de 125 ejercicios categorizados para Pilates y Zumba.
     - Ilustraciones vectoriales dinámicas en SVG (stickmen flotantes transparentes sin bordes ni cajas).
     - Material claramente indicado en etiqueta superior independiente (*Mancuernas 2kg, Banda Decathlon, Aro Pilates, KB, Esterilla, Peso Corporal*).
  2. **Modo Solo Temporizador**:
     - Temporizador libre y limpio para cuando no se desean ejercicios predefinidos.
     - Tú decides los ejercicios en vivo mientras la app gestiona el número de estaciones por serie, las rondas y los descansos.

- 🔔 **Audio Sintetizado sin Dependencias (Web Audio API)**:
  - Campana de boxeo y gong armónico al inicio de ronda.
  - Tonos sutiles de aviso para los últimos 3 segundos.
  - Funciona con la pantalla encendida mediante Wake Lock API.

- 📱 **Instalable como App Móvil (PWA)**:
  - Manifiesto `manifest.json` y Service Worker `sw.js` integrados.
  - Abre el enlace en Safari o Chrome en tu teléfono y pulsa *"Añadir a la pantalla de inicio"*.

---

## 🛠️ Estructura del Proyecto

- `index.html` - Aplicación completa (HTML5, Tailwind CSS, SVG dinámico y lógica en JavaScript).
- `sw.js` - Service Worker para caché offline instantánea.
- `manifest.json` - Configuración de instalación PWA.
- `dumbbell_data.json` - Base de datos de ejercicios de mancuernas.
- `ARQUITECTURA.md` - Guía técnica de la arquitectura de software.
- `MEJORAS.md` - Bitácora de evoluciones y notas de diseño.
