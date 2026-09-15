# ESPECIFICACIÓN BIOMECÁNICA MAESTRA Y GUÍA DE DISEÑO VECTORIAL SVG
## Aplicación Sergio Fit — Entrenamiento Funcional y Pilates (Población Diana: 40 - 60 Años)

> **Documento Técnico Oficial de Kinesiología y Biomecánica Aplicada**  
> **Destinatario directo**: Subagente de Diseño Gráfico e Ilustración SVG  
> **Objetivo**: Estandarización visual, corrección anatómica y definición fotograma a fotograma de los **75 ejercicios** (25 Aeróbicos `a1-a25`, 25 Fuerza `s1-s25`, 25 Mancuernas `m1-m25`).

---

## 1. RESUMEN EJECUTIVO Y AUDITORÍA CRÍTICA DE LA BASE ACTUAL

### 1.1. Diagnóstico de la Base de Datos Actual
Tras auditar exhaustivamente el archivo `dumbbell_data.json` y los bloques `fullExerciseDatabase` y `EXERCISE_SVGS` en `index.html`, se han detectado deficiencias de diseño críticas que comprometen la comprensión y la seguridad de las usuarias:

1. **Clonación Masiva en Ejercicios con Mancuernas (`m1` - `m25`)**:
   - **20 de los 25 ejercicios** con mancuernas comparten **exactamente el mismo código SVG genérico de un muñeco de frente flexionando ligeramente los brazos**.
   - Ejercicios con demandas biomecánicas radicalmente opuestas muestran la misma figura:
     - `m15` (*Remo Dorsal inclinado a 45º*) se muestra como una persona de pie erguida.
     - `m17` (*Peso Muerto Rumano con bisagra de cadera*) se muestra como una persona erguida.
     - `m18` (*Patada de Tríceps con extensión sagital*) se muestra como un curl frontal.
     - `m5` (*Talones al Glúteo*) y `m8` (*Patinador*) se muestran en bipedestación neutra sin flexión ni cruce de piernas.
2. **Error Grave de Asignación de Ejercicio**:
   - `m20` (*Zancada Estática / Lunge*) muestra el dibujo de una **Sentadilla bilateral**. La zancada exige obligatoriamente un plano sagital con tijera de piernas y flexión de ambas rodillas a 90º. Mostrarla como sentadilla es un error de prescripción motriz severo.
3. **Plano Anatómico Inadecuado (Confusión Coronal vs Sagital)**:
   - Para movimientos con flexión/extensión del raquis y de la cadera (sentadillas, bisagras, remos, peso muerto, patadas traseras, zancadas), la **vista coronal (frente) anula la percepción de la columna neutra y del ángulo de cadera**, provocando que el usuario encorve la zona lumbar. **Debe emplearse Vista Sagital (Perfil estricto)**.
   - Para ejercicios de abducción, pasos laterales o aperturas pectorales, el plano coronal (Frente) es el correcto.
4. **Duplicidad en Trabajo en Suelo**:
   - `m25` (*Aperturas de Pecho en esterilla*) tiene el mismo SVG que `m24` (*Floor Press*), mostrando un empuje vertical en lugar de una apertura en arco semicircular.
   - `a7` (*Talones al glúteo*) en vista frontal dibuja una rodilla acortada ilegible que parece una deformidad de pierna; en vista de perfil es evidente e intuitivo.

---

## 2. ESTÁNDARES BIOMECÁNICOS Y ERGONÓMICOS PARA ADULTOS (40-60 AÑOS)

Las usuarias de este rango de edad presentan particularidades fisiológicas y articulares que el dibujo debe reflejar con máxima pulcritud para evitar lesiones:

| Región Anatómica | Riesgo Frecuente en 40-60 Años | Criterio Biomecánico Obligatorio en el Dibujo |
| :--- | :--- | :--- |
| **Columna Lumbar (L1-S1)** | Hernias discales, pinzamiento ciático por flexión con carga o hiperextensión. | **Columna Neutra**. Jamás dibujar chepa (cifosis dorsal excesiva) ni hiperlordosis. En bisagras y remos, línea recta continua cabeza-coxis. |
| **Articulación Patelofemoral** | Condromalacia, desgaste de cartílago por sobrecarga en flexión profunda (>90º). | **Ángulo de rodilla nunca menor a 90º**. La rodilla nunca sobrepasa la punta del pie de forma acusada; la cadera viaja atrás hacia los talones. |
| **Hombro y Manguito Rotador** | Síndrome subacromial, tendinitis supraespinoso por elevaciones en abducción pura a 90º. | **Plano Escapular**. Las elevaciones de brazos se realizan a **30º por delante del plano coronal**, con codos ligeramente flexionados ("codos blandos"). |
| **Columna Cervical** | Rectificación cervical, sobrecarga del trapecio superior al encoger hombros. | **Mirada alineada con el esternón**. Cuello largo, hombros deprimidos y escápulas conectadas lejos de las orejas. |
| **Suelo Pélvico y Faja Abdominal** | Incontinencia de esfuerzo, prolapsos, diástasis. | Activación del transverso abdominal mediante respiración coordinada (marcada con vectores de exhalación en el punto de contracción). |

---

## 3. ESPECIFICACIÓN DEL SISTEMA VECTORIAL SVG (GUÍA DE IMPLEMENTACIÓN)

Todos los gráficos deben crearse dentro del estándar unificado de la aplicación:

- **ViewBox**: `0 0 100 100` (con `fill="none"` y bordes redondeados).
- **Estructura Interna**:
  - Contenedor Fotograma 1: `<g class="gif-step1">` (Posición Inicial / Fase Excéntrica).
  - Contenedor Fotograma 2: `<g class="gif-step2">` (Contracción Máxima / Rango Objetivo).
  - Retorno cíclico gobernado por el motor CSS `.gif-step1` y `.gif-step2` (1.8s a 3.0s por ciclo).
- **Paleta Cromática Oficial**:
  - Figura Humana (Huesos / Segmentos): Trazo `#f8fafc` (blanco tiza), `stroke-width="4.5"` a `5`, `stroke-linecap="round"`.
  - Cabeza: Círculo `#f8fafc`, radio `r="6"`.
  - Mancuernas (`MANC`): Cuerpo `#0284c7` (azul cobalto), discos/extremos `#38bdf8` (azul cian brillante), `r="2.8"`.
  - Goma Elástica / Banda Decathlon (`BANDA`): Trazo `#10b981` (esmeralda activo), `stroke-width="3"` a `4.5`, puntos de anclaje `#047857`.
  - Aro de Pilates (`ARO`): Elipse/anillo `#06b6d4` (cian neón), `stroke-width="3"`, almohadillas laterales `#0891b2`.
  - Kettlebell (`KB`): Esfera `#10b981`, asa curva `#047857`, `stroke-width="2.5"`.
  - Esterilla (`EST`): Rectángulo base `#8b5cf6` (púrpura suave), `rx="2"`, `fill="#8b5cf6"`.
  - Flechas e Indicadores Cinemáticos: Trazo `#f59e0b` (ámbar vibrante) o `#10b981` (verde tracción), `stroke-width="2"`, `stroke-linecap="round"`.

---

## 4. AUDITORÍA Y ESPECIFICACIÓN: 25 EJERCICIOS AERÓBICOS (`a1` - `a25`)

### [a1] Marcha en el Sitio con Braceo Rítmico
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Activación cardiorrespiratoria de bajo impacto articular, reeducación del patrón cruzado locomotor.
- **Diagnóstico SVG Actual**: Frontal. Válido pero muy estático, la elevación de rodilla no tiene suficiente dinamismo.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL (Ligeramente oblicuo 15º)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, pie izquierdo firmemente apoyado en suelo (`cx=44, cy=90`).
  - Pie derecho apoyado en metatarso, rodilla derecha con flexión incipiente (15º).
  - Brazo izquierdo al frente flexionado a 90º a nivel del ombligo; brazo derecho relajado atrás.
- **Fotograma 2 (Acción / Elevación)**:
  - Rodilla derecha elevada a 75º-80º respecto a la cadera (`cx=58, cy=68`).
  - Codo izquierdo avanza a la altura del esternón coordinado con rodilla contraria.
  - Brazo derecho extendido hacia atrás para contrarrestar.
  - Flecha ámbar curva ascendente en la rodilla derecha indicando ritmo ágil.
- **Pautas de Seguridad (40-60 años)**: Apoyo suave sobre metatarso amortiguando la caída, sin zapatazo; evitar subir rodilla más de 90º para no sobrecargar psoas.

---

### [a2] Paso Lateral con Tracción al Pecho
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Apertura torácica, trabajo de deltoides posterior y coordinación rítmica frontal.
- **Diagnóstico SVG Actual**: Frontal. Banda dibujada muy delgada, poco claro el vector de abducción escapular.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos al ancho de caderas (`cx=46, cy=90` y `cx=54, cy=90`).
  - Manos a la anchura del pecho sujetando la banda floja a la altura de las clavículas (`d="M40 44 L60 44"`).
- **Fotograma 2 (Acción)**:
  - Pierna derecha se separa lateralmente en abducción amplia (`cx=78, cy=90`), mini-flexión de rodillas amortiguadora.
  - Brazos se separan horizontalmente estirando la goma elástica `#10b981` al doble de su longitud contra el esternón (`d="M22 38 L78 38"`).
  - Flechas ámbar bilaterales de apertura lateral en las manos.
- **Pautas de Seguridad**: Hombros bajos lejos de orejas, no permitir que la tensión de la goma tire bruscamente de los brazos al volver.

---

### [a3] Toque de Rodillas Alternas con Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Flexión de cadera asistida, estabilidad monopodal dinámica y propiocepción.
- **Diagnóstico SVG Actual**: Frontal. El aro se superpone de forma confusa con la rodilla.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación neutra, aro sostenido horizontalmente con ambas manos a la altura de la cintura (`ellipse cx="50" cy="52" rx="10" ry="5"`).
  - Pies paralelos al ancho de hombros.
- **Fotograma 2 (Acción)**:
  - Rodilla izquierda se flexiona y eleva al centro hacia el eje medio (`cx=50, cy=60`).
  - El aro desciende ligeramente para hacer contacto suave sobre el muslo/rodilla elevada.
  - Tronco completamente vertical sin inclinarse hacia delante a buscar el aro.
  - Flecha ámbar vertical indicando ascenso controlado de rodilla.
- **Pautas de Seguridad**: Mantener pelvis neutra, no arquear zona lumbar para ganar altura en la rodilla.

---

### [a4] Escalador Suave en Suelo
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Resistencia cardiovascular en cadena cerrada, estabilización lumbopélvica anti-extensión.
- **Diagnóstico SVG Actual**: Sagital suelo. La cadera está dibujada demasiado alta en pico.
- **Plano Óptimo**: **PERFIL (SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - Posición de plancha alta sobre esterilla (`rect x="10" y="80" width="80" height="5"`).
  - Manos bajo hombros, brazos extendidos (`x=68, y=50 L68 80`).
  - Tronco, cadera y piernas extendidas formando una rampa descendente neutra a 15º.
- **Fotograma 2 (Acción)**:
  - Pierna derecha avanza flexionando rodilla hacia el esternón a 90º (`L45 52 L56 64 L50 76`).
  - Pie derecho suspendido en el aire sin tocar el suelo; pie izquierdo firme en apoyo.
  - Columna lumbar perfectamente inalterada (sin botar ni combarse).
  - Flecha verde de avance fluido en rodilla derecha.
- **Pautas de Seguridad**: Ritmo continuo sin rebote; no hiperextender cuello (mirada al borde anterior de la colchoneta).

---

### [a5] Balanceo Ruso Suave a Dos Manos (Kettlebell Swing Adaptado)
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Potencia extensora de glúteos e isquiosurales, frecuencia cardíaca sin impacto rotuliano.
- **Diagnóstico SVG Actual**: Sagital. Bueno en concepto, pero la trayectoria pendular debe ser inequívoca.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio / Bisagra atrás)**:
  - Cadera empujada atrás en bisagra (flexión de cadera 70º, rodillas suaves 20º de flexión, tibias verticales).
  - Tronco recto inclinado a 45º. Kettlebell colgando entre los muslos (`cx=42, cy=72`).
- **Fotograma 2 (Extensión y Flotación)**:
  - Extensión enérgica de cadera (glúteos bloqueados, pelvis neutra, cuerpo en vertical).
  - La kettlebell flota por inercia hacia el frente a la altura exacta del pecho/ombligo (`cx=78, cy=42`), brazos relajados como cuerdas.
  - Arco punteado ámbar que ilustra la trayectoria pendular desde atrás hacia delante.
- **Pautas de Seguridad**: No levantar la pesa con los hombros ni brazos; jamás hiperextender columna lumbar al ponerse de pie.

---

### [a6] Step Touch Lateral con Tracción de Goma
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Trabajo aductor/abductor con ritmo musical, retracción escapular coordinada.
- **Diagnóstico SVG Actual**: Frontal. Falta amplitud en la pisada lateral.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos al centro (`cx=45, cy=90` y `50, 90`), banda con tensión base entre ambas manos a la anchura de hombros.
- **Fotograma 2 (Acción)**:
  - Paso lateral abierto hacia la derecha (`cx=68, cy=90`), rodilla derecha amortiguada.
  - Tracción bilateral de codos hacia los costados separando la banda con el pecho erguido.
  - Flecha lateral doble reflejando apertura simultánea de base y tren superior.
- **Pautas de Seguridad**: Apoyo plantar completo en el paso lateral para evitar torceduras de tobillo.

---

### [a7] Talones al Glúteo con Braceo Suave
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Estiramiento dinámico de cuádriceps, bombeo venoso de pantorrilla y flexión isquiotibial.
- **Diagnóstico SVG Actual**: **Frontal muy deficiente**. Al mirar de frente, la pierna que va atrás se solapa y no se entiende el ejercicio.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Figura de perfil erguida, pierna izquierda de apoyo recta y firme (`L50 56 L44 90`).
  - Brazos relajados a los lados o en balanceo sagital.
- **Fotograma 2 (Acción)**:
  - Talón derecho se flexiona hacia el glúteo alcanzando un ángulo de 90º-110º de flexión de rodilla (`L50 56 L50 74 L38 72`).
  - El muslo permanece casi vertical alineado con el tronco (la rodilla no viaja hacia delante).
  - Codo contrario flexiona enérgicamente hacia atrás simulando braceo activo.
  - Flecha curva ámbar ascendente desde el talón hacia el isquion.
- **Pautas de Seguridad**: No flexionar la cadera delantera ni inclinar el tronco adelante al subir el talón.

---

### [a8] Rotación Dinámica de Tronco con Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Movilidad torácica rotacional, activación de oblicuos y estabilización de la pelvis.
- **Diagnóstico SVG Actual**: Frontal. Bueno, requiere marcar la fijación pélvica.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies al ancho de hombros clavados al frente. Aro sostenido al frente con brazos semicurvos girado a la izquierda (`cx=38, cy=45`).
- **Fotograma 2 (Acción)**:
  - Giro controlado del bloque torácico hacia la derecha (`cx=62, cy=45`).
  - Caderas y rodillas permanecen apuntando rígidamente hacia el frente (cero torsión en rodillas).
  - Arco punteado ámbar entre izquierda y derecha a la altura del esternón.
- **Pautas de Seguridad**: Rotación torácica pura; no torsionar las rodillas para evitar estrés meniscal.

---

### [a9] Puente Dinámico Rápido (Glute Bridge Pulse)
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Activación cardiovascular en suelo mediante cadencia rítmica de extensores de cadera.
- **Diagnóstico SVG Actual**: Suelo decúbito supino. Correcto, pero debe definirse la fase de bajada y subida.
- **Plano Óptimo**: **PERFIL (SAGITAL) / DECÚBITO SUPINO**.
- **Fotograma 1 (Inicio)**:
  - Tumbada boca arriba en esterilla, escápulas apoyadas, rodillas flexionadas a 90º con pies planos en el suelo (`cx=74, cy=80`).
  - Glúteo apoyado o rozando la esterilla (`L28 78 L54 78`).
- **Fotograma 2 (Acción / Impulso)**:
  - Elevación de pelvis hasta formar una línea recta perfecta hombro-cadera-rodilla (`L28 78 L52 56 L72 80`).
  - Apriete simultáneo de glúteos y activación del core.
  - Flecha verde vertical `#10b981` debajo del sacro indicando empuje de cadera al techo.
- **Pautas de Seguridad**: Evitar arquear la zona lumbar en la cumbre; empujar a través de los talones.

---

### [a10] Paso Frontal en V con Saludo de Brazos (V-Step)
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Patrón aeróbico clásico, coordinación espacial y activación sin impacto.
- **Diagnóstico SVG Actual**: Frontal. Genérico.
- **Plano Óptimo**: **FRENTE / PERSPECTIVA AXONOMÉTRICA SUAVE**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos en el vértice de la V (`cx=46, cy=90` y `54, 90`), brazos al pecho o en costados.
- **Fotograma 2 (Acción)**:
  - Piernas abiertas en paso diagonal adelante formando una base ancha (`cx=34, cy=88` y `66, 88`).
  - Brazos se elevan abriéndose en forma de "V" a 45º sobre la cabeza.
  - Flechas de apertura diagonal en pies y brazos.
- **Pautas de Seguridad**: Apoyar toda la planta del pie al dar el paso diagonal adelante.

---

### [a11] Shadow Boxing con Banda Tras la Espalda
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Potencia de tren superior, estabilización anterior del core y resistencia muscular.
- **Diagnóstico SVG Actual**: 3/4. Buena base, requiere clarificar el paso del bucle tras la espalda.
- **Plano Óptimo**: **3/4 OBLICUO FRONTAL**.
- **Fotograma 1 (Inicio)**:
  - Posición de guardia de boxeo, codos pegados a costillas, banda pasando por las axilas y escápulas.
- **Fotograma 2 (Acción)**:
  - Extensión recta controlada del brazo adelantado (Jab) proyectando el puño contra la goma (`L46 36 L76 36`).
  - Brazo contrario permanece protegiendo la barbilla.
  - Línea de tensión elástica estirada `#10b981` y flecha horizontal de impacto suave.
- **Pautas de Seguridad**: Nunca bloquear el codo en hiperextensión brusca; mantener hombros descendidos.

---

### [a12] Desplazamiento Lateral al Pecho con Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Desplazamiento lateral de cadencia ágil y tono postural de cintura escapular.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación en el margen izquierdo (`cx=40, cy=56`), sujetando el aro con palmas firmes al pecho.
- **Fotograma 2 (Acción)**:
  - Doble paso ágil hacia la derecha (`cx=60, cy=56`), manteniendo flexión atlética de rodillas.
  - Flecha ámbar bidireccional horizontal señalando el vaivén lateral.
- **Pautas de Seguridad**: Mantener el centro de gravedad bajo y rodillas sin colapsar hacia dentro (evitar valgo dinámico).

---

### [a13] Marcha en Cuadrupedia Suave (Bear Crawl Hold Dinámico)
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Activación del núcleo profundo, estabilización escapulohumeral y cadencia coordinativa.
- **Diagnóstico SVG Actual**: Sagital suelo. La rodilla apenas se percibe despegada.
- **Plano Óptimo**: **PERFIL (SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - En cuadrupedia perfecta sobre esterilla: muñecas bajo hombros, rodillas bajo caderas a 90º apoyadas en suelo (`cy=78`).
  - Espalda plana como una mesa.
- **Fotograma 2 (Acción)**:
  - Despegue de rodillas de 3 a 5 cm del suelo sosteniendo el peso en metatarsos y manos.
  - Elevación alternativa de una rodilla 2 cm más sin alterar el raquis lumbosacro.
  - Flecha verde ascendente milimétrica bajo la rodilla levantada.
- **Pautas de Seguridad**: No arquear la lumbar ni dejar caer la cabeza; empujar activamente el suelo con las manos.

---

### [a14] Traslado Dinámico a Dos Manos con Kettlebell
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Carga frontal estabilizadora (Goblet hold) combinada con pasos laterales.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Sujeción de la kettlebell por los cuernos pegada al esternón (`cx=42, cy=56`), pies en ancho de cadera.
- **Fotograma 2 (Acción)**:
  - Paso lateral dinámico abriendo a un lado (`cx=58, cy=56`), absorbiendo el impacto con flexión de cadera y rodillas.
  - Flecha ámbar horizontal entre ambas posiciones del torso.
- **Pautas de Seguridad**: Mantener los codos cerrados hacia las costillas protegiendo la articulación del hombro.

---

### [a15] Jumping Jacks sin Salto (Low-Impact Jacks)
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Aumento de pulso cardíaco sin impacto reactivo en suelo pélvico ni articulaciones.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación neutra, pies juntos en eje central, brazos relajados a lo largo del cuerpo (`cx=50`).
- **Fotograma 2 (Acción)**:
  - Pierna derecha se desplaza lateralmente tocando con metatarso el suelo a 45º (`cx=72, cy=90`).
  - Brazos se elevan simultáneamente en arco circular lateral por encima de la cabeza (`d="M50 34 L32 20 M50 34 L68 20"`).
  - Flecha lateral en el pie derecho y flechas en arco en las manos.
- **Pautas de Seguridad**: Codos y rodillas ligeramente flexionados; no chocar las manos violentamente arriba.

---

### [a16] Tracción Frontal en Tijera con Banda
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Coordinación anteroposterior, trabajo cruzado de espalda y zancada dinámica.
- **Diagnóstico SVG Actual**: **Frontal confuso**. No se aprecia la separación sagital de los pies.
- **Plano Óptimo**: **PERFIL (SAGITAL) O 3/4 SAGITAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos de perfil, banda sujetada al frente a nivel de hombros.
- **Fotograma 2 (Acción)**:
  - Paso frontal en tijera (un pie delante, otro detrás), brazos traccionan abriendo la banda horizontalmente contra el esternón.
  - Tensión máxima visible en la banda `#10b981`.
- **Pautas de Seguridad**: Mantener el torso erguido en la vertical sin volcar el peso sobre la rodilla delantera.

---

### [a17] Patinador Suave sin Salto (Skater Step)
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Activación del glúteo medio, equilibrio lateral y agilidad funcional.
- **Diagnóstico SVG Actual**: Frontal plano sin dinamismo de cruce posterior.
- **Plano Óptimo**: **FRENTE / PERSPECTIVA FRONTAL DINÁMICA**.
- **Fotograma 1 (Inicio)**:
  - Apoyo sobre pierna izquierda flexionada a 30º, torso ligeramente inclinado con columna recta, brazos equilibrando a la izquierda.
- **Fotograma 2 (Acción)**:
  - Desplazamiento suave a la derecha: pierna izquierda cruza en diagonal por detrás rozando la punta del pie en el suelo.
  - Brazos oscilan rítmicamente hacia la derecha.
  - Flechas cruzadas en la base de sustentación.
- **Pautas de Seguridad**: Mantener la rodilla de apoyo siempre alineada con el 2º dedo del pie (sin colapso interno).

---

### [a18] Elevación de Rodilla con Compresión de Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Contracción simultánea de recto anterior, psoas y pectorales/dorsales.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación erguida, aro sostenido a la altura del esternón entre ambas palmas abiertas.
- **Fotograma 2 (Acción)**:
  - Subida de rodilla derecha a 80º mientras se comprimen las almohadillas laterales del aro haciéndolo ovalar (`rx="7"` en vez de `9`).
  - Flechas ámbar enfrentadas de compresión sobre el aro.
- **Pautas de Seguridad**: No flexionar la columna para acercar el aro a la pierna; hombros abajo.

---

### [a19] Bicicleta Suave en Esterilla (Espalda Apoyada)
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Movilidad de cadera y rodilla con apoyo total del raquis lumbar.
- **Diagnóstico SVG Actual**: Suelo lateral. El movimiento circular del pedaleo debe ser evidente.
- **Plano Óptimo**: **PERFIL (SAGITAL) / DECÚBITO SUPINO**.
- **Fotograma 1 (Inicio)**:
  - Boca arriba, cabeza apoyada en esterilla, manos al suelo o tras la nuca sin traccionar el cuello.
  - Una pierna flexionada a 90º hacia el pecho y la otra semi-extendida a 45º.
- **Fotograma 2 (Acción)**:
  - Inversión fluida de piernas trazando un pedaleo circular continuo.
  - Línea circular de pedaleo en verde esmeralda `#10b981`.
- **Pautas de Seguridad**: Zona lumbar 100% adherida a la colchoneta; no descender los pies por debajo de 45º para no arquear la espalda.

---

### [a20] Step Adelante con Balanceo de Kettlebell
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Estabilización de marcha con carga inercial suave.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **PERFIL (SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - De pie de perfil, kettlebell en reposo con brazos extendidos hacia abajo.
- **Fotograma 2 (Acción)**:
  - Paso corto adelante apoyando talón-punta mientras la pesa se balancea fluidamente hacia el frente hasta la altura del ombligo.
  - Curva de péndulo en flecha discontinua ámbar.
- **Pautas de Seguridad**: Guiar el balanceo con la cadera y glúteo; no levantar la pesa por encima del pecho.

---

### [a21] Braceo de Boxeo Estático
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Cadencia cardiorrespiratoria de brazos y cintura escapular con base fija.
- **Diagnóstico SVG Actual**: Frontal. Válido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Guardia de boxeo al mentón, puño izquierdo proyectado al frente (`cx=28, cy=36`), puño derecho protegiendo costillas.
- **Fotograma 2 (Acción)**:
  - Retracción del brazo izquierdo e impacto suave frontal con el puño derecho (`cx=72, cy=36`).
  - Marcador circular ámbar en el puño que avanza.
- **Pautas de Seguridad**: Mantener flexión residual de 5º en codos para preservar ligamentos del olécranon.

---

### [a22] Remo Dinámico con Paso Atrás
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Cadena posterior dinámica, sincronización de miembro superior e inferior.
- **Diagnóstico SVG Actual**: Sagital / oblicuo.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - De perfil, banda anclada al frente; brazos extendidos adelante con tensión suave, pies juntos.
- **Fotograma 2 (Acción)**:
  - Pierna atrasada da un paso largo apoyando metatarso; simultáneamente tracción profunda de codos hacia las costillas pegados al cuerpo.
  - Tensión evidente de la banda estirándose hacia el torso (`#10b981`).
- **Pautas de Seguridad**: Tronco en rampa vertical erguida; no arquear lumbares al tirar de los codos atrás.

---

### [a23] Elevación de Talones Rítmica con Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Retorno venoso en sóleos/gemelos y estabilidad de la musculatura intrínseca del pie.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies planos al suelo, aro sostenido con ambas manos frente al pecho.
- **Fotograma 2 (Acción)**:
  - Elevación completa sobre metatarsos (talones despegados 5-8 cm del suelo).
  - Aro elevado por encima de la cabeza con brazos en arco suave.
  - Flechas ascendentes bajo ambos talones (`#f59e0b`).
- **Pautas de Seguridad**: Apoyar de forma equilibrada sobre el 1º y 2º metatarsiano evitando que el tobillo se tuerza hacia fuera.

---

### [a24] Gato-Vaca Dinámico en Cuadrupedia
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Movilidad rítmica segmentaria de la columna vertebral y descompresión discal.
- **Diagnóstico SVG Actual**: Sagital suelo.
- **Plano Óptimo**: **PERFIL (SAGITAL) / SUELO**.
- **Fotograma 1 (Fase Gato / Flexión)**:
  - En 4 apoyos sobre esterilla, columna completamente curvada hacia el techo en "C", cabeza relajada con barbilla al esternón, pelvis en retroversión.
  - Flecha ámbar apuntando hacia arriba en el centro de la espalda (`cy=30`).
- **Fotograma 2 (Fase Vaca / Extensión Neutra Asistida)**:
  - Columna desciende suavemente a neutro con ligera extensión torácica, esternón se proyecta al frente, mirada diagonal al suelo.
  - Flecha verde apuntando hacia el suelo (`cy=62`).
- **Pautas de Seguridad**: En población de 40-60 años no forzar una hiperlordosis lumbar extrema en la fase de vaca; enfatizar la movilidad dorsal.

---

### [a25] Bisagra de Cadera Rítmica con Kettlebell
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Reeducación del patrón de bisagra (Hip Hinge) frente al agachamiento de rodilla.
- **Diagnóstico SVG Actual**: Sagital.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Extensión / Inicio)**:
  - Bipedestación neutra erguida, kettlebell sujetada con ambas manos a nivel púbico.
- **Fotograma 2 (Bisagra atrás)**:
  - Cadera se desplaza horizontalmente hacia atrás, rodillas con flexión mínima fija (15º), torso inclinado a 45º con columna rígida neutra.
  - La pesa viaja rozando los muslos hasta la parte superior de las tibias.
  - Flecha horizontal hacia atrás a la altura del glúteo.
- **Pautas de Seguridad**: La flexión nace 100% de la cadera; cero flexión en el raquis lumbar.

---

## 5. AUDITORÍA Y ESPECIFICACIÓN: 25 EJERCICIOS DE FUERZA (`s1` - `s25`)

### [s1] Sentadilla Asistida a Silla o Banco
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Fuerza funcional de cuádriceps, glúteos y preservación de la independencia motriz.
- **Diagnóstico SVG Actual**: Perfil con banco. Bien orientado pero el ángulo articular debe ser estrictamente 90º.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido delante de una silla/banco situado atrás (`rect x="62" y="66" width="20" height="24"`).
  - Pies al ancho de hombros, brazos extendidos al frente para contrapeso (`x=32, y=44`).
- **Fotograma 2 (Acción / Roce)**:
  - Cadera se desplaza atrás y abajo rozando el asiento sin descargar el peso corporal.
  - Muslos paralelos al suelo (ángulo femorotibial a 90º exactos), rodillas nunca sobrepasan la vertical de la punta del pie.
  - Línea punteada de control entre glúteo y banco (`#f59e0b`).
- **Pautas de Seguridad**: Empujar el suelo a través de los talones para levantarse; pecho alto y orgulloso.

---

### [s2] Remo Dorsal Doble con Banda Pisada
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Fortalecimiento de dorsal ancho, romboides, trapecio medio y corrección de postura hipercifótica.
- **Diagnóstico SVG Actual**: Sagital. Correcto en concepto, pero requiere detallar el pegado de codos a costillas.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Torso inclinado a 45º con bisagra de cadera sólida. Banda pisada con ambos pies (`ellipse cx="51" cy="92"`).
  - Brazos extendidos hacia abajo tensando la goma elástica (`#10b981`).
- **Fotograma 2 (Acción / Tracción)**:
  - Codos traccionan pegados a las costillas sobrepasando la línea del tronco hacia atrás (`L44 54`).
  - Retracción escapular activa (juntar omóplatos sin elevar hombros a las orejas).
  - Flechas ámbar apuntando en diagonal ascendente-posterior.
- **Pautas de Seguridad**: Mantener el cuello neutro alineado con la espalda (no mirar al techo).

---

### [s3] Compresión de Aro entre Rodillas (Suelo Pélvico y Aductores)
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Co-activación de aductores mayores, transverso del abdomen y musculatura del suelo pélvico.
- **Diagnóstico SVG Actual**: Frontal. Válido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - De pie o sentada, aro colocado horizontalmente justo por encima de las rodillas (`ellipse cx="50" cy="72" rx="10" ry="8"`).
  - Pies alineados con caderas.
- **Fotograma 2 (Acción / Apriete)**:
  - Aducción isométrica de muslos comprimiendo el aro (`rx="6" ry="8"`).
  - Flechas ámbar de compresión bilateral medial hacia el centro.
  - Exhalación forzada vaciando abdomen.
- **Pautas de Seguridad**: Evitar que los pies giren en pronación hacia dentro al apretar; presión progresiva sin sacudidas.

---

### [s4] Puente de Glúteo con Apriete Isométrico
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Hipertrofia y tono del glúteo mayor, descompresión de flexores de cadera acortados.
- **Diagnóstico SVG Actual**: Sagital suelo.
- **Plano Óptimo**: **PERFIL (SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - Tumbada supina sobre esterilla, rodillas flexionadas a 90º, talones apoyados firmes, pelvis en suelo.
- **Fotograma 2 (Acción / Contracción)**:
  - Elevación de pelvis hasta bloquear cadera en línea recta rodilla-pelvis-hombro.
  - Círculo de activación verde esmeralda `#10b981` en glúteos indicando 2 segundos de pausa arriba.
- **Pautas de Seguridad**: No arquear la columna lumbar al subir; la fuerza proviene del empuje de talones y contracción de glúteos.

---

### [s5] Peso Muerto Rumano a Dos Manos con Kettlebell
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Fortalecimiento de la cadena posterior excéntrica (isquiotibiales, glúteos, erectores espinales).
- **Diagnóstico SVG Actual**: Sagital.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, kettlebell sostenida por el asa delante de los muslos con hombros deprimidos.
- **Fotograma 2 (Acción / Descenso)**:
  - Bisagra de cadera profunda hacia atrás, rodillas "suaves" (microflexión fija de 15º).
  - La kettlebell desciende vertical rozando las espinillas hasta la altura de la rótula/media tibia.
  - Columna 100% plana y neutra paralela a 35º del suelo.
- **Pautas de Seguridad**: Detener el descenso en cuanto la cadera deje de viajar hacia atrás para evitar redondear la espalda baja.

---

### [s6] Apertura de Escápulas (Band Pull-Apart)
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Corrección postural del síndrome cruzado superior, fortalecimiento de deltoides posterior y romboides.
- **Diagnóstico SVG Actual**: Frontal. Válido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - De pie, brazos extendidos al frente al ancho de hombros sujetando la banda elástica horizontal a nivel de las axilas.
- **Fotograma 2 (Acción)**:
  - Separación horizontal de brazos abriendo en cruz hasta que la banda toque suavemente el esternón (`d="M22 36 L78 36"`).
  - Tensión máxima visible y puntos terminales esmeralda.
- **Pautas de Seguridad**: Prohibido arquear la espalda lumbar hacia atrás para ayudar a la apertura; mantener costillas cerradas.

---

### [s7] Prensa Pectoral con Aro de Pilates
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Tono de pectoral mayor, tríceps y estabilizadores anteriores del hombro.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Aro sostenido entre las palmas abiertas a la altura del esternón, codos abiertos en ángulo de 45º hacia abajo (`rx="10"`).
- **Fotograma 2 (Acción)**:
  - Compresión isométrica potente de las palmas aplastando el aro hacia el centro (`rx="6.5"`).
  - Flechas ámbar de compresión interna centrípeta.
- **Pautas de Seguridad**: Mantener los hombros abajo y lejos de las orejas (evitar encogimiento del trapecio).

---

### [s8] Bird-Dog (Perro de Caza) en Esterilla
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Estabilidad del core en patrón cruzado anti-rotación (McGill Big 3).
- **Diagnóstico SVG Actual**: Sagital suelo.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - Posición de cuadrupedia neutra (4 apoyos simétricos en colchoneta).
- **Fotograma 2 (Acción / Extensión)**:
  - Extensión simultánea del brazo derecho al frente y la pierna izquierda atrás hasta formar una línea horizontal perfecta (`d="M14 50 L88 48"`).
  - Línea punteada verde de alineación horizontal talón-glúteo-espalda-mano.
- **Pautas de Seguridad**: No elevar la pierna por encima de la cadera para evitar hiperextensión lumbar; cadera cuadrada mirando al suelo.

---

### [s9] Paseo del Granjero Asimétrico (Suitcase Carry)
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Fuerza anti-flexión lateral del tronco (cuadrado lumbar, oblicuos) y agarre.
- **Diagnóstico SVG Actual**: Frontal. Válido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Kettlebell sostenida en la mano derecha a un lado del muslo (`cx=36, cy=68`).
  - Hombros perfectamente nivelados y horizontales (cero inclinación hacia el lado del peso).
- **Fotograma 2 (Acción)**:
  - Marcha firme paso a paso manteniendo el torso 100% vertical como un bloque indeformable.
  - Marcador de nivelación horizontal en hombros.
- **Pautas de Seguridad**: Si el tronco se inclina hacia el lado de la pesa, reducir el peso de inmediato.

---

### [s10] Sentadilla Isométrica en Pared (Wall Sit)
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Fuerza isométrica de cuádriceps y estabilidad lumbopélvica sin estrés sobre columna.
- **Diagnóstico SVG Actual**: Sagital contra muro.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Espalda apoyada en la pared vertical (`line x1="30" y1="10" x2="30" y2="95"`), de pie.
- **Fotograma 2 (Acción / Isometría)**:
  - Descenso del tronco resbalando por la pared hasta que los muslos queden horizontales a 90º respecto a las tibias.
  - Rodillas alineadas sobre tobillos formando un ángulo recto perfecto (`M36 68 L56 68 L56 92`).
  - Círculo de tensión verde en la articulación de la rodilla.
- **Pautas de Seguridad**: Nunca permitir que los pies queden por detrás de las rodillas (aumentaría la presión patelar).

---

### [s11] Buenos Días con Banda Elástica (Good Mornings)
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Cadena posterior y aprendizaje del torque de cadera con resistencia elástica variable.
- **Diagnóstico SVG Actual**: Sagital.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Banda pisada con ambos pies, el bucle superior pasa por detrás de los trapecios (no sobre vértebras cervicales). De pie erguido.
- **Fotograma 2 (Acción / Inclinación)**:
  - Bisagra pura de cadera hacia atrás; torso inclinado a 45º manteniendo curvatura lumbar neutra y tensión de la goma elástica `#10b981`.
  - Arco punteado ámbar de flexión de cadera.
- **Pautas de Seguridad**: El bucle descansa en la parte carnosa de los trapecios; cuello largo sin flexión cervical.

---

### [s12] Compresión de Aro en Decúbito Lateral
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Fuerza y tono aislado del glúteo medio, estabilizador clave de la marcha.
- **Diagnóstico SVG Actual**: Decúbito lateral.
- **Plano Óptimo**: **PERFIL / SUELO DECÚBITO LATERAL**.
- **Fotograma 1 (Inicio)**:
  - Tumbada de lado, piernas semi-extendidas, aro colocado entre los tobillos o pantorrillas (`ellipse cx="74" cy="67"`).
- **Fotograma 2 (Acción / Aducción)**:
  - Presión descendente de la pierna superior aplastando el aro de Pilates (`ellipse ry="5.5"`).
  - Flecha descendente indicadora de fuerza vertical sobre la almohadilla.
- **Pautas de Seguridad**: Mantener la pelvis vertical y perpendicular al suelo sin que caiga hacia atrás.

---

### [s13] Patada de Glúteo en Cuadrupedia (Donkey Kicks)
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Activación aislada de fibras superiores del glúteo mayor sin compromiso lumbar.
- **Diagnóstico SVG Actual**: Sagital suelo.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - Posición de 4 apoyos sobre esterilla, rodillas flexionadas a 90º.
- **Fotograma 2 (Acción / Extensión)**:
  - Elevación de la pierna derecha manteniendo la rodilla doblada a 90º, empujando la planta del pie plano hacia el techo (`d="L24 44 L24 32"`).
  - El muslo alcanza la altura de la horizontal del cuerpo.
  - Flecha vertical esmeralda de empuje hacia arriba.
- **Pautas de Seguridad**: Detener la pierna en cuanto la espalda intente arquearse (cero anteversión de pelvis).

---

### [s14] Sentadilla Sumo Colgante con Kettlebell
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Reclutamiento de aductores, glúteo mayor y cuádriceps con menor inclinación del tronco.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies bien separados (1.5 veces el ancho de hombros), puntas orientadas hacia fuera a 40º-45º.
  - Kettlebell colgando en el centro con brazos extendidos relajados.
- **Fotograma 2 (Acción / Descenso vertical)**:
  - Descenso del torso casi vertical hasta que los muslos alcancen los 45º-60º respecto al suelo.
  - Rodillas viajan activamente hacia fuera en la misma dirección que las puntas de los pies.
  - La kettlebell desciende libremente en el eje vertical central.
- **Pautas de Seguridad**: Vigilar que las rodillas no colapsen hacia dentro al iniciar el ascenso.

---

### [s15] Curl de Bíceps con Banda Pisada
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Fuerza de flexores del codo (bíceps braquial, braquial anterior) con tensión progresiva.
- **Diagnóstico SVG Actual**: Frontal. Válido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - De pie, banda pisada con ambos pies al centro, brazos extendidos a los costados con codos pegados al cuerpo.
- **Fotograma 2 (Acción / Flexión)**:
  - Flexión de codos a 90º-110º subiendo las manos hacia los hombros sin balancear el torso.
  - Bandas elásticas estiradas al máximo `#10b981`.
- **Pautas de Seguridad**: Codos clavados a los costados; prohibido inclinar la espalda atrás para hacer palanca.

---

### [s16] Aducción de Muslos Sentada con Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Acondicionamiento de aductores y estabilización de la sínfisis púbica en descarga.
- **Diagnóstico SVG Actual**: Frontal sentado.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL (Ligeramente en perspectiva)**.
- **Fotograma 1 (Inicio)**:
  - Sentada en silla o banco erguida, aro colocado entre las caras internas de los muslos (`ellipse rx="10"`).
- **Fotograma 2 (Acción / Compresión)**:
  - Cierre potente de muslos aplastando el aro (`ellipse rx="6"`).
  - Pausa de 3 segundos con flechas ámbar de compresión medial.
- **Pautas de Seguridad**: Espalda completamente erguida, hombros relajados sin tensar cuello.

---

### [s17] Plancha Frontal con Apoyo de Rodillas
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Resistencia isométrica de la faja abdominal (anti-extensión) adaptada para proteger raquis lumbar.
- **Diagnóstico SVG Actual**: Sagital suelo con rodillas.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - Antebrazos y rodillas apoyados en esterilla, tronco relajado antes de conectar.
- **Fotograma 2 (Acción / Bloqueo en Tabla)**:
  - Cuerpo elevado formando una línea diagonal impecable desde las rodillas hasta los hombros (`d="M64 56 L34 68 L28 78"`).
  - Glúteos contraídos, ombligo succionado hacia la columna, codos empujando el suelo (anti-colapso escapular).
  - Rectángulo indicador verde de tensión abdominal firme.
- **Pautas de Seguridad**: Jamás dejar caer la pelvis hacia el suelo (evitaría hiperlordosis lesiva).

---

### [s18] Zancada Estática Asistida con Manos Libres (Split Squat)
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Fuerza unilateral de cuádriceps, glúteo y equilibrio locomotor.
- **Diagnóstico SVG Actual**: Perfil estático.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Posición en tijera fija: pierna delantera adelantada y pierna trasera con talón despegado del suelo. Tronco vertical.
- **Fotograma 2 (Acción / Descenso 90º/90º)**:
  - Descenso vertical del torso: ambas rodillas se flexionan simultáneamente a 90º exactos (`L36 68 L36 90` y `L62 78 L62 90`).
  - La rodilla delantera permanece sobre el tobillo; la trasera desciende hacia el suelo sin impactar.
  - Flecha ámbar de descenso vertical en el centro de gravedad.
- **Pautas de Seguridad**: El torso baja recto en la vertical, no hacia delante; mantener la distancia de zancada amplia.

---

### [s19] Tracción al Pecho y Elevación con Kettlebell (Remo al Mentón / High Pull)
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Tono de trapecio superior, medio y deltoides con tracción vertical suave.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, kettlebell sostenida por el asa a dos manos a nivel púbico (`cx=50, cy=68`).
- **Fotograma 2 (Acción)**:
  - Tracción vertical de la pesa hasta el esternón/pecho; los codos suben siempre por encima de las manos apuntando hacia fuera (`cx=50, cy=46`).
  - Flecha vertical ámbar de recorrido ascendente.
- **Pautas de Seguridad**: La kettlebell nunca supera la altura del esternón para no provocar pinzamiento subacromial.

---

### [s20] Extensión de Tríceps Vertical con Banda
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Tono de tríceps braquial en aislamiento sin sobrecarga articular.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Mano izquierda ancla la banda firmemente sobre la clavícula contraria. Mano derecha sujeta la banda a la altura del pecho con codo flexionado a 90º.
- **Fotograma 2 (Acción / Extensión)**:
  - Brazo derecho extiende el antebrazo verticalmente hacia el suelo hasta el bloqueo controlado del codo (`L56 68`).
  - Banda estirada y flecha descendente ámbar.
- **Pautas de Seguridad**: El codo que empuja no debe separarse del costado.

---

### [s21] Rotación Externa de Hombro con Aro
- **Material**: Aro de Pilates (`aro`).
- **Objetivo**: Refuerzo de manguito rotador (infraespinoso y redondo menor) y estabilización humeral.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Codos flexionados a 90º pegados rígidamente a las costillas; antebrazos paralelos sujetando el aro por dentro (`rx="8"`).
- **Fotograma 2 (Acción / Apertura)**:
  - Separación de manos hacia fuera girando sobre el eje del húmero contra la resistencia del aro (`rx="11"`).
  - Flechas ámbar divergentes hacia fuera en los antebrazos.
- **Pautas de Seguridad**: Los codos jamás se despegan de los flancos corporales.

---

### [s22] Activación del Abdomen Transverso en Esterilla
- **Material**: Esterilla (`esterilla`).
- **Objetivo**: Reeducación del transverso, estabilización pélvica y aplanamiento de la faja abdominal.
- **Diagnóstico SVG Actual**: Sagital suelo.
- **Plano Óptimo**: **PERFIL (SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio)**:
  - Tumbada boca arriba con rodillas dobladas, curvatura lumbar neutra con pequeño hueco natural bajo la espalda.
- **Fotograma 2 (Acción / Imprint)**:
  - Retroversión pélvica suave e impronta de toda la zona lumbar contra la colchoneta expulsando el aire.
  - Círculo verde de activación en el ombligo que "se pega al suelo".
- **Pautas de Seguridad**: Movimiento guiado por la respiración; no contener el aire (evitar maniobra de Valsalva).

---

### [s23] Elevación de Talones con Kettlebell
- **Material**: Kettlebell Pesada (`kettlebell`).
- **Objetivo**: Fuerza de gastrocnemios y sóleo con sobrecarga axial vertical.
- **Diagnóstico SVG Actual**: Frontal.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, kettlebell sujetada a dos manos al frente, pies planos apoyados.
- **Fotograma 2 (Acción / Elevación)**:
  - Máxima elevación de talones sobre las puntas de los pies con pausa isométrica de 1 segundo arriba.
  - Flechas ámbar de empuje vertical bajo los talones.
- **Pautas de Seguridad**: Mantener rodillas extendidas pero sin hiperextender hacia atrás (no bloquear rodilla en genu recurvatum).

---

### [s24] Flexiones Asistidas con Rodillas en Esterilla
- **Material**: Peso Corporal (`corporal`).
- **Objetivo**: Fuerza de empuje horizontal (pectoral, tríceps, serrato anterior) con brazo de palanca reducido.
- **Diagnóstico SVG Actual**: Sagital suelo.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL) / SUELO**.
- **Fotograma 1 (Inicio / Arriba)**:
  - Apoyo de manos y rodillas en esterilla. Manos bajo los hombros, cuerpo en línea diagonal de rodillas a coronilla.
- **Fotograma 2 (Acción / Descenso)**:
  - Flexión de codos a 45º respecto al torso (codos en flecha, nunca en "T" a 90º) descendiendo el pecho a 10 cm del suelo.
  - Columna y cuello completamente alineados en bloque.
- **Pautas de Seguridad**: No dejar caer la cabeza ni arquear la zona lumbar hacia el suelo.

---

### [s25] Abducción de Cadera de Pie con Minibanda
- **Material**: Goma Elástica (`goma`).
- **Objetivo**: Fuerza del glúteo medio y estabilizadores pélvicos en bipedestación con resistencia en tobillos.
- **Diagnóstico SVG Actual**: Frontal. Válido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Banda elástica alrededor de los tobillos (`path d="M46 82 L54 82"`). Pies al ancho de hombros.
- **Fotograma 2 (Acción / Abducción)**:
  - Separación lateral controlada de la pierna derecha manteniendo el pie recto hacia el frente (`d="M46 82 L70 80"`).
  - Tensión máxima en la banda elástica y flecha lateral ámbar.
- **Pautas de Seguridad**: El tronco permanece erguido vertical sin ladearse hacia el lado contrario para compensar.

---

## 6. AUDITORÍA Y ESPECIFICACIÓN: 25 EJERCICIOS DE MANCUERNAS (`m1` - `m25`)

> [!CRITICAL]
> **REDISEÑO PRIORITARIO INMEDIATO**:  
> Esta sección corrige la anomalía más grave detectada en la app: **los SVGs genéricos duplicados**. Cada ejercicio dispone ahora de su anatomía funcional propia, sus ángulos precisos y su plano óptimo irremplazable.

---

### [m1] Marcha en el Sitio con Curl de Bíceps
- **Tipo**: Aeróbico (`pz`).
- **Material**: Mancuernas 1.5 - 2 kg (`mancuernas`).
- **Objetivo**: Coordinación locomotora con carga periférica y tonificación de flexores de codo.
- **Diagnóstico SVG Actual**: Frontal genérico repetido.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación con pie izquierdo plano y rodilla derecha iniciando subida suave.
  - Brazos extendidos a los lados con mancuernas en agarre neutro/supino (`cx=42, cy=58` y `cx=58, cy=58`).
- **Fotograma 2 (Acción)**:
  - Rodilla derecha elevada a 75º.
  - Flexión simultánea de ambos codos llevando las mancuernas a la altura de los hombros/esternón (`cx=34, cy=42` y `cx=66, cy=42`).
  - Flechas ámbar verticales de curl en ambos antebrazos.
- **Pautas de Seguridad**: Mantener codos fijos a los lados del torso; no utilizar inercia de la espalda para elevar las pesas.

---

### [m2] Paso Lateral con Empuje Frontal (Punch / Press Frontal)
- **Tipo**: Aeróbico (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Cardio dinámico con deltoides anterior y estabilización rotuliana lateral.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos al centro, mancuernas recogidas pegadas a las clavículas con codos flexionados cerrados.
- **Fotograma 2 (Acción)**:
  - Paso lateral amplio hacia la derecha (`cx=74, cy=90`), mini-sentadilla de amortiguación.
  - Ambos brazos empujan simultáneamente las mancuernas al frente a la altura exacta del pecho (`cx=38, cy=40` y `cx=62, cy=40`).
  - Flechas horizontales de empuje al frente.
- **Pautas de Seguridad**: No extender las mancuernas por encima de los hombros; no bloquear bruscamente los codos.

---

### [m3] Boxeo Suave con Mancuernas (Alternating Punches)
- **Tipo**: Aeróbico (`z`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Frecuencia cardíaca continua, tono de deltoides y rotación suave de tronco.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL (Ligeramente en guardia)**.
- **Fotograma 1 (Inicio)**:
  - Pies en anchura de hombros con rodillas desbloqueadas.
  - Puño izquierdo adelantado en directo suave con mancuerna horizontal (`cx=30, cy=38`), puño derecho en guardia pegado a la mandíbula (`cx=58, cy=42`).
- **Fotograma 2 (Acción)**:
  - Inversión fluida: brazo izquierdo recoge a la guardia y brazo derecho proyecta puñetazo recto controlado (`cx=70, cy=38`).
  - Marcador de impacto ámbar en la mancuerna que avanza.
- **Pautas de Seguridad**: Usar mancuernas ligeras (1-1.5 kg máximo); amortiguar el final del golpe con los músculos dorsales.

---

### [m4] Step Touch con Elevación Frontal Baja
- **Tipo**: Aeróbico (`z`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Ritmo aeróbico y deltoides anterior sin compromiso subacromial.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos, mancuernas descansando sobre la cara anterior de los muslos (`cx=44, cy=58` y `cx=56, cy=58`).
- **Fotograma 2 (Acción)**:
  - Paso lateral a la derecha (`cx=68, cy=90`), pies separados.
  - Elevación simultánea de mancuernas al frente únicamente hasta la altura del ombligo/esternón (máximo 45º de flexión de hombro), con codos ligeramente flexionados.
  - Flechas ascendentes cortas en los puños.
- **Pautas de Seguridad**: Jamás elevar las mancuernas por encima del nivel del pecho para no irritar el manguito rotador.

---

### [m5] Talones al Glúteo con Remo Sagital
- **Tipo**: Aeróbico (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Activación de isquiosurales coordinada con retracción escapular y dorsal.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Totalmente incorrecto**.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Figura de perfil: pierna de apoyo recta, brazos estirados al frente sosteniendo las mancuernas (`x=65, y=50`).
- **Fotograma 2 (Acción)**:
  - Pierna derecha flexiona rodilla a 90º llevando el talón directo al glúteo (`L50 56 L50 74 L38 72`).
  - Simultáneamente, ambos codos traccionan enérgicamente hacia atrás pegados a las costillas (`L50 36 L36 46`).
  - Mancuernas quedan alojadas junto a las costillas flotantes.
  - Flecha curva en talón y flecha horizontal hacia atrás en codo.
- **Pautas de Seguridad**: No arquear la columna lumbar al traccionar los codos atrás; mantener el pecho erguido.

---

### [m6] Paso en V con Apertura de Brazos (V-Step Fly)
- **Tipo**: Aeróbico (`z`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Coordinación de pasos con deltoides posterior y pectoral menor.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos en el vértice posterior, mancuernas unidas delante del ombligo con codos flexionados a 90º (`cx=46` y `cx=54`).
- **Fotograma 2 (Acción)**:
  - Pies avanzan en diagonal abriendo la base (`cx=34, cy=88` y `cx=66, cy=88`).
  - Brazos se abren hacia los lados en forma de "W" a 45º manteniendo codos flexionados.
  - Flechas divergentes de apertura en extremidades superiores.
- **Pautas de Seguridad**: No llevar los codos por detrás del plano del cuerpo para proteger la cápsula anterior del hombro.

---

### [m7] Marcha con Transporte de Maletas (Suitcase March)
- **Tipo**: Aeróbico / Postural (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Estabilidad espinal en carga vertical y fortalecimiento de trapecios/antebrazos.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación con hombros nivelados simétricamente, brazos rectos a los lados sujetando las mancuernas como dos maletas pesadas (`cx=38, cy=60` y `cx=62, cy=60`).
  - Pie izquierdo plano.
- **Fotograma 2 (Acción)**:
  - Marcha firme elevando la rodilla derecha a 70º (`cx=56, cy=68`).
  - El tronco y las mancuernas permanecen **rigurosamente estables y nivelados**, sin balanceo ni inclinación lateral.
  - Indicadores de aplomo horizontal en la línea de las clavículas.
- **Pautas de Seguridad**: Mantener abdomen activo para que la pelvis no caiga (signo de Trendelenburg).

---

### [m8] Patinador Suave con Balanceo Pendular de Brazos
- **Tipo**: Aeróbico (`z`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Estabilidad lateral, desaceleración con carga y coordinación rítmica.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PERSPECTIVA FRONTAL**.
- **Fotograma 1 (Inicio)**:
  - Apoyo sobre pierna izquierda semi-flexionada, pierna derecha cruzada por detrás en el aire, mancuernas balanceadas hacia la izquierda del cuerpo (`cx=32, cy=52`).
- **Fotograma 2 (Acción)**:
  - Salto/paso suave a la derecha: apoyo sobre pierna derecha, pierna izquierda cruza por detrás, mancuernas oscilan en péndulo controlado hacia la derecha (`cx=68, cy=52`).
  - Flecha en arco pendular que conecta ambas posiciones.
- **Pautas de Seguridad**: El balanceo de las mancuernas es un péndulo pasivo de inercia; no forzar con los hombros.

---

### [m9] Toque de Talón al Frente con Press al Pecho
- **Tipo**: Aeróbico (`z`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Disociación motriz de miembros inferiores y empuje horizontal de tren superior.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **PERFIL (SAGITAL) O 3/4**.
- **Fotograma 1 (Inicio)**:
  - De perfil/semiprofil, pies juntos, mancuernas recogidas al esternón pegadas al cuerpo (`x=50, y=42`).
- **Fotograma 2 (Acción)**:
  - Pierna derecha se adelanta apoyando firmemente el talón con la punta al techo (`x=68, y=90`).
  - Ambos brazos empujan las mancuernas en horizontal al frente a la altura del pecho (`x=72, y=42`).
  - Flechas de proyección frontal.
- **Pautas de Seguridad**: No flexionar la columna lumbar al sacar el talón al frente.

---

### [m10] Sentadilla Corta con Impulso al Pecho
- **Tipo**: Aeróbico (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Trabajo cardiovascular de triple extensión (tobillo-rodilla-cadera).
- **Diagnóstico SVG Actual**: Sentadilla frontal estática genérica.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Mini-sentadilla)**:
  - Figura de perfil en flexión suave de cadera y rodilla (media sentadilla a 45º), mancuernas pegadas al pecho (`x=50, y=42`).
- **Fotograma 2 (Extensión a puntillas)**:
  - Extensión enérgica del cuerpo elevándose sobre las puntas de los pies (flexión plantar).
  - Mancuernas se mantienen pegadas al esternón para seguridad de la palanca.
  - Flechas ascendentes en talones y cabeza (`#f59e0b`).
- **Pautas de Seguridad**: La sentadilla es corta y controlada; no permitir que las rodillas se adelanten a los dedos.

---

### [m11] Paso Atrás Alterno con Apertura en "W"
- **Tipo**: Aeróbico / Postural (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Estiramiento de cadena anterior, activación de romboides y zancada dinámica suave.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies juntos al centro, mancuernas a la altura de la cintura con codos flexionados.
- **Fotograma 2 (Acción)**:
  - Pie derecho da un paso atrás apoyando el metatarso.
  - Brazos se abren lateralmente formando una "W" perfecta: codos pegados a costillas y mancuernas separadas hacia los hombros externos (`cx=28, cy=38` y `cx=72, cy=38`).
  - Flechas de retracción escapular externa.
- **Pautas de Seguridad**: Mantener el pecho abierto y esternón elevado sin arquear las lumbares.

---

### [m12] Desplazamiento Lateral con Guardia Cerrada
- **Tipo**: Aeróbico (`z`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Agilidad en el plano frontal, tono isométrico de bíceps y hombros.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Bipedestación en el lado izquierdo del tapiz, mancuernas sostenidas en guardia rígida delante del mentón/pecho (`cx=46, cy=36` y `cx=54, cy=36`).
- **Fotograma 2 (Acción)**:
  - Dos pasos laterales rápidos hacia la derecha (`cx=68`), manteniendo la guardia cerrada inmutable.
  - Flecha horizontal doble indicando el traslado de la base.
- **Pautas de Seguridad**: Mantener las rodillas en flexión constante para amortiguar el impacto lateral.

---

### [m13] Marcha Rápida con Braceo Alterno Corto
- **Tipo**: Aeróbico (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Cadencia rápida de paso y braceo con carga para acelerar gasto calórico.
- **Diagnóstico SVG Actual**: Idéntico a `m1`. **Incorrecto**.
- **Plano Óptimo**: **PERFIL (SAGITAL) O 3/4 SAGITAL**.
- **Fotograma 1 (Inicio)**:
  - De perfil: codos flexionados a 90º fijos. Brazo derecho adelante a la altura del pecho (`x=64, y=40`), brazo izquierdo atrás (`x=36, y=52`).
  - Pierna izquierda en apoyo y pierna derecha subiendo rodilla.
- **Fotograma 2 (Acción)**:
  - Inversión rápida y rítmica: brazo izquierdo adelante con mancuerna, brazo derecho atrás. Rodilla contraria elevada.
  - Flechas opuestas ámbar en ambos brazos.
- **Pautas de Seguridad**: Braceo corto y controlado; no lanzar las mancuernas de forma descontrolada para no dañar los hombros.

---

### [m14] Sentadilla a Silla al Pecho con Mancuernas (Goblet Squat a Banco)
- **Tipo**: Fuerza (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Fuerza funcional de extensión de piernas con carga anterior (Goblet).
- **Diagnóstico SVG Actual**: Sentadilla frontal genérica. **Debe ser de perfil con silla visible**.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido de perfil, silla dibujada detrás (`rect x="64" y="66" width="18" height="24"`).
  - Mancuernas sostenidas verticalmente pegadas contra el esternón (`x=46, y=40`).
- **Fotograma 2 (Acción / Descenso)**:
  - Flexión de cadera empujando los glúteos atrás hasta rozar la silla (`x=58, y=66`).
  - Muslos horizontales a 90º, tibias casi verticales, rodillas sin sobrepasar las puntas.
  - Mancuernas firmes en el pecho sin separarse.
  - Flecha diagonal descendente-posterior hacia el asiento.
- **Pautas de Seguridad**: Mantener el torso con inclinación natural alineada con las tibias; no sentarse a descansar en la silla.

---

### [m15] Remo Dorsal con Codos Pegados a Dos Manos
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Hipertrofia de dorsal ancho, redondo mayor y estabilizadores espinales en flexión de tronco.
- **Diagnóstico SVG Actual**: **De pie erguido frontal (clon de `m1`). Disparate biomecánico**.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Torso inclinado a 45º respecto a la horizontal, columna vertebral recta y neutra desde el sacro a la cabeza (`d="M38 34 L58 50"`).
  - Brazos colgados perpendiculares al suelo con mancuernas bajo los hombros (`x=48, y=68`).
- **Fotograma 2 (Acción / Tracción)**:
  - Codos traccionan hacia atrás y hacia el techo pegados a los costados (`d="M48 38 L36 46 L46 52"`).
  - Mancuernas suben rozando las costillas flotantes.
  - Escápulas conectadas firmemente atrás. Flecha ascendente ámbar en el codo.
- **Pautas de Seguridad**: Rodillas en ligera flexión de 20º para dar holgura a los isquiotibiales y evitar que la espalda baja se redondee.

---

### [m16] Elevaciones Laterales en Plano Escapular (Scaption)
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Tonificación del deltoides medio y supraespinoso sin pinzamiento acromial.
- **Diagnóstico SVG Actual**: Clon de `m1`. **Incorrecto**.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL (Con brazos a 30º adelantados)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, mancuernas a los lados de los muslos con palmas enfrentadas hacia dentro.
- **Fotograma 2 (Acción / Elevación a 30º)**:
  - Brazos se elevan lateralmente en un ángulo de **30º hacia delante del plano frontal** (plano escapular natural).
  - Los codos quedan ligeramente flexionados y las manos suben **únicamente hasta la altura de las axilas** (máx. 70º-80º de abducción).
  - Pulgares ligeramente más altos que los meñiques (evita rotación interna forzada).
  - Flechas curvas ámbar ascendentes.
- **Pautas de Seguridad**: Prohibido superar la horizontal de los hombros; no balancear el cuerpo para arrancar el movimiento.

---

### [m17] Peso Muerto Rumano Asistido con Mancuernas
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Cadena posterior (isquiosurales, glúteo mayor y musculatura paravertebral).
- **Diagnóstico SVG Actual**: **Clon de `m1` (de pie erguido sin bisagra). Inadmisible**.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - De pie de perfil, hombros atrás y abajo, mancuernas pegadas al frente de los muslos (`x=48, y=56`).
- **Fotograma 2 (Acción / Bisagra atrás)**:
  - La cadera viaja hacia atrás en flexión mientras el tronco se inclina recto hacia delante a 45º (`d="M34 34 L56 48"`).
  - Las mancuernas descienden rozando la parte delantera de los muslos hasta quedar justo por debajo de las rodillas (`x=50, y=72`).
  - Rodillas mantienen una microflexión constante de 15º (tibias verticales).
  - Flecha horizontal hacia atrás en el glúteo y vertical descendente en las mancuernas.
- **Pautas de Seguridad**: Las mancuernas nunca se separan de las piernas (reduce el brazo de palanca lumbar a cero).

---

### [m18] Patada de Tríceps a Dos Manos (Triceps Kickback)
- **Tipo**: Fuerza (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Aislamiento del tríceps braquial en extensión terminal de codo contra la gravedad.
- **Diagnóstico SVG Actual**: **Clon de `m1` (muñeco de frente flexionando brazos como un curl). Totalmente opuesto a la realidad**.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Tronco inclinado hacia delante a 45º con espalda neutra y rodillas flexionadas.
  - Codos flexionados a 90º y **elevados al nivel del tronco, pegados a los costados** (`x=46, y=42`). Mancuerna colgando bajo el pecho.
- **Fotograma 2 (Acción / Extensión atrás)**:
  - El codo permanece **completamente congelado en el espacio** mientras el antebrazo se extiende hacia atrás hasta quedar paralelo al tronco (`L46 42 L68 40`).
  - Mancuerna situada detrás de la cadera en el punto más alto.
  - Flecha en arco ascendente-posterior en el antebrazo.
- **Pautas de Seguridad**: Prohibido balancear el brazo como un péndulo; solo se mueve la articulación del codo.

---

### [m19] Curl de Bíceps Martillo Controlado (Hammer Curl)
- **Tipo**: Fuerza (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Fuerza de braquiorradial y bíceps braquial con articulación radiocubital en neutro.
- **Diagnóstico SVG Actual**: Clon de `m1`.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL (o 3/4)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, mancuernas a los lados de los muslos con palmas enfrentadas (agarre neutro o de martillo) (`cx=40, cy=58` y `cx=60, cy=58`).
- **Fotograma 2 (Acción / Flexión vertical)**:
  - Flexión de ambos codos subiendo las mancuernas verticalmente hacia los hombros con las palmas mirándose en todo momento (`cx=36, cy=38` y `cx=64, cy=38`).
  - Codos fijados a las costillas. Flechas de flexión vertical.
- **Pautas de Seguridad**: Mantener muñecas firmes en línea recta con el antebrazo (sin flexión ni extensión de muñeca).

---

### [m20] Zancada Estática con Mancuernas (Static Lunge / Split Squat)
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Fuerza unilateral de cuádriceps y glúteo con sobrecarga en brazos.
- **Diagnóstico SVG Actual**: **Dibujado como una sentadilla bilateral frontal. Error biomecánico crítico**.
- **Plano Óptimo**: **PERFIL ESTRICTO (PLANO SAGITAL)**.
- **Fotograma 1 (Inicio)**:
  - Posición en tijera de perfil: pie derecho adelantado, pie izquierdo atrasado apoyando metatarso con talón alto.
  - Brazos estirados a los lados sujetando las mancuernas hacia abajo como maletas (`x=48, y=56`).
- **Fotograma 2 (Acción / Descenso 90º/90º)**:
  - Descenso vertical del cuerpo: ambas rodillas se flexionan a 90º (`d="M48 62 L36 68 L36 90 M48 62 L64 76 L64 90"`).
  - La rodilla delantera sobre el talón; la rodilla trasera se sitúa a 5 cm del suelo bajo la cadera.
  - Mancuernas descienden verticales junto a las caderas.
  - Flecha descendente vertical.
- **Pautas de Seguridad**: El torso desciende vertical como un ascensor, sin inclinarse hacia delante.

---

### [m21] Pájaros para Deltoides Posterior y Escápulas (Rear Delt Fly)
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Tonificación de deltoides posterior, trapecio medio e inferior para combatir hombros adelantados.
- **Diagnóstico SVG Actual**: Clon de `m1`. **Incorrecto**.
- **Plano Óptimo**: **PERFIL INCLINADO O 3/4 OBLICUO POSTERIOR**.
- **Fotograma 1 (Inicio)**:
  - Tronco inclinado a 45º con espalda recta, mancuernas colgando juntas debajo del pecho con codos ligeramente flexionados (`cx=48, cy=66`).
- **Fotograma 2 (Acción / Vuelo lateral)**:
  - Los brazos se abren en semicírculo hacia los lados hasta alcanzar la horizontal de los hombros (`cx=28, cy=46` y `cx=72, cy=46`), manteniendo la flexión de codos constante.
  - Escápulas juntas con fuerza en el centro de la espalda.
  - Flechas curvas de apertura lateral ascendente.
- **Pautas de Seguridad**: Carga muy ligera (1 kg); no usar impulso del torso para levantar los brazos.

---

### [m22] Sentadilla Sumo Central con Mancuernas Unidas
- **Tipo**: Fuerza (`pz`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Aductores, cuádriceps y suelo pélvico con centro de gravedad bajo y tronco erguido.
- **Diagnóstico SVG Actual**: Sentadilla estrecha genérica.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL**.
- **Fotograma 1 (Inicio)**:
  - Pies bien separados (más anchos que hombros), puntas giradas hacia fuera a 45º (`cx=30, cy=90` y `cx=70, cy=90`).
  - Las dos mancuernas sujetadas juntas en el centro colgando verticales entre los muslos.
- **Fotograma 2 (Acción / Descenso)**:
  - Descenso vertical de pelvis manteniendo las rodillas abiertas hacia fuera alineadas con los dedos de los pies.
  - Las mancuernas descienden por la línea media central hasta la altura de las rodillas.
  - Torso muy erguido.
- **Pautas de Seguridad**: Las rodillas nunca deben colapsar hacia el interior al subir.

---

### [m23] Elevación de Talones con Mancuernas para Gemelos
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas (`mancuernas`).
- **Objetivo**: Fuerza y bombeo venoso de gastrocnemios y sóleo con sobrecarga lateral.
- **Diagnóstico SVG Actual**: Clon de `m1`.
- **Plano Óptimo**: **FRENTE / PLANO CORONAL (o PERFIL)**.
- **Fotograma 1 (Inicio)**:
  - De pie erguido, pies paralelos al ancho de caderas, mancuernas sostenidas a los lados de los muslos.
- **Fotograma 2 (Acción / Subida)**:
  - Elevación completa de los talones sobre los metatarsos despegando del suelo 6-8 cm (`M44 88 M56 88`).
  - Pausa isométrica de 1 segundo arriba.
  - Flechas ámbar verticales ascendentes en talones.
- **Pautas de Seguridad**: Mantener el peso repartido sobre la base del dedo gordo para evitar torceduras externas.

---

### [m24] Press de Pecho en Esterilla con Mancuernas (Floor Press)
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas y Esterilla (`mancuernas`).
- **Objetivo**: Fuerza de empuje pectoral y tríceps con límite mecánico de seguridad para el hombro (el suelo evita hiperextensión).
- **Diagnóstico SVG Actual**: Sagital suelo. Aceptable en concepto, debe perfeccionarse la posición de codos a 45º.
- **Plano Óptimo**: **PERFIL (SAGITAL) / SUELO**.
- **Fotograma 1 (Descenso / Inicio)**:
  - Tumbada boca arriba en esterilla (`rect x="8" y="80" width="84" height="5"`), rodillas flexionadas con pies en suelo.
  - Codos apoyados suavemente en el suelo a 45º respecto al cuerpo, mancuernas sobre los codos (`x=36, y=62`).
- **Fotograma 2 (Acción / Empuje)**:
  - Empuje vertical de las mancuernas hacia el techo hasta la extensión controlada de los codos sobre el pecho (`x=36, y=48`).
  - Mancuernas alineadas verticalmente con el esternón.
  - Flechas verticales de empuje hacia arriba.
- **Pautas de Seguridad**: El contacto de los codos con el suelo protege el hombro; no rebotar los codos con fuerza sobre la colchoneta.

---

### [m25] Apertura de Pecho en Esterilla (Dumbbell Floor Flyes)
- **Tipo**: Fuerza (`p`).
- **Material**: Mancuernas y Esterilla (`mancuernas`).
- **Objetivo**: Estiramiento y fuerza del pectoral mayor en abducción horizontal protegida por el suelo.
- **Diagnóstico SVG Actual**: **Copia exacta del Floor Press (`m24`). Muestra un empuje recto en vez de una apertura semicircular**.
- **Plano Óptimo**: **VISTA FRONTAL / CENITAL EN DECÚBITO SUPINO (o 3/4 suelo)**.
- **Fotograma 1 (Inicio / Brazos Arriba)**:
  - Tumbada boca arriba, brazos extendidos sobre el esternón con codos ligeramente doblados (en arco de abrazo), palmas mirándose enfrentadas (`cx=46, cy=50` y `cx=54, cy=50`).
- **Fotograma 2 (Acción / Apertura en Arco)**:
  - Los brazos se abren hacia los lados en un semicírculo hasta que el dorso de los brazos y los codos tocan suavemente la esterilla (`cx=24, cy=64` y `cx=76, cy=64`).
  - El suelo actúa como tope natural impidiendo que el hombro caiga en hiperextensión lesiva.
  - Arcos ámbar divergentes mostrando la trayectoria circular de apertura.
- **Pautas de Seguridad**: Mantener el ángulo de flexión del codo (aprox. 20º) fijo durante todo el movimiento; no estirar los brazos al 100%.

---

## 7. MATRIZ RESUMEN DE PLANOS VISUALES Y PRIORIDADES DE ACCIÓN

Esta tabla sirve como hoja de ruta técnica inmediata para el diseñador SVG:

| ID | Ejercicio | Material | Plano Visual Óptimo | Estado Actual | Prioridad Rediseño |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **a1** | Marcha en el Sitio con Braceo | Corporal | FRENTE (Coronal) | Aceptable | Baja |
| **a2** | Paso Lateral con Tracción al Pecho | Goma | FRENTE (Coronal) | Aceptable | Baja |
| **a3** | Toque de Rodillas Alternas | Aro | FRENTE (Coronal) | Aceptable | Baja |
| **a4** | Escalador Suave | Esterilla | PERFIL (Sagital suelo) | Mejorable | Media |
| **a5** | Balanceo Ruso Suave | Kettlebell | PERFIL (Sagital) | Bueno | Baja |
| **a6** | Step Touch con Tracción | Goma | FRENTE (Coronal) | Aceptable | Baja |
| **a7** | Talones al Glúteo con Braceo | Corporal | **PERFIL (Sagital)** | **Confuso (Frontal)** | **ALTA** |
| **a8** | Rotación Dinámica de Tronco | Aro | FRENTE (Coronal) | Bueno | Baja |
| **a9** | Puente Dinámico Rápido | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **a10** | Paso Frontal en V (V-Step) | Corporal | FRENTE (Coronal) | Aceptable | Baja |
| **a11** | Shadow Boxing con Goma | Goma | 3/4 OBLICUO | Aceptable | Baja |
| **a12** | Desplazamiento Lateral al Pecho | Aro | FRENTE (Coronal) | Aceptable | Baja |
| **a13** | Marcha en Cuadrupedia | Esterilla | PERFIL (Sagital suelo) | Mejorable | Media |
| **a14** | Traslado Dinámico a Dos Manos | Kettlebell | FRENTE (Coronal) | Aceptable | Baja |
| **a15** | Jumping Jacks sin Salto | Corporal | FRENTE (Coronal) | Aceptable | Baja |
| **a16** | Tracción Frontal en Tijera | Goma | **PERFIL (Sagital)** | **Confuso (Frontal)** | **ALTA** |
| **a17** | Patinador Suave sin Salto | Corporal | FRENTE (Coronal) | Aceptable | Media |
| **a18** | Elevación Rodilla con Compresión | Aro | FRENTE (Coronal) | Aceptable | Baja |
| **a19** | Bicicleta Suave | Esterilla | PERFIL (Sagital suelo) | Aceptable | Media |
| **a20** | Step Adelante con Balanceo | Kettlebell | PERFIL (Sagital) | Aceptable | Media |
| **a21** | Braceo de Boxeo Estático | Corporal | FRENTE (Coronal) | Aceptable | Baja |
| **a22** | Remo Dinámico Paso Atrás | Goma | PERFIL (Sagital) | Bueno | Baja |
| **a23** | Elevación de Talones Rítmica | Aro | FRENTE (Coronal) | Aceptable | Baja |
| **a24** | Gato-Vaca Dinámico | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **a25** | Bisagra de Cadera Rítmica | Kettlebell | PERFIL (Sagital) | Bueno | Baja |
| **s1** | Sentadilla a Silla Asistida | Corporal | PERFIL (Sagital) | Bueno | Baja |
| **s2** | Remo Dorsal Doble | Goma | PERFIL (Sagital) | Bueno | Baja |
| **s3** | Compresión entre Rodillas | Aro | FRENTE (Coronal) | Bueno | Baja |
| **s4** | Puente de Glúteo | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **s5** | Peso Muerto Rumano | Kettlebell | PERFIL (Sagital) | Bueno | Baja |
| **s6** | Apertura de Escápulas | Goma | FRENTE (Coronal) | Bueno | Baja |
| **s7** | Prensa Pectoral con Aro | Aro | FRENTE (Coronal) | Bueno | Baja |
| **s8** | Bird-Dog | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **s9** | Paseo del Granjero | Kettlebell | FRENTE (Coronal) | Bueno | Baja |
| **s10** | Sentadilla en Pared (Wall Sit) | Corporal | PERFIL (Sagital) | Bueno | Baja |
| **s11** | Buenos Días con Goma | Goma | PERFIL (Sagital) | Bueno | Baja |
| **s12** | Compresión Decúbito Lateral | Aro | PERFIL (Suelo lateral) | Bueno | Baja |
| **s13** | Patada de Glúteo Cuadrupedia | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **s14** | Sentadilla Sumo Colgante | Kettlebell | FRENTE (Coronal) | Bueno | Baja |
| **s15** | Curl de Bíceps con Goma | Goma | FRENTE (Coronal) | Bueno | Baja |
| **s16** | Aducción de Muslos Sentada | Aro | FRENTE (Coronal) | Bueno | Baja |
| **s17** | Plancha con Rodillas | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **s18** | Zancada Estática Asistida | Corporal | PERFIL (Sagital) | Bueno | Baja |
| **s19** | Tracción al Pecho y Elevación | Kettlebell | FRENTE (Coronal) | Bueno | Baja |
| **s20** | Extensión Tríceps Vertical | Goma | FRENTE (Coronal) | Bueno | Baja |
| **s21** | Rotación Externa de Hombro | Aro | FRENTE (Coronal) | Bueno | Baja |
| **s22** | Abdomen Transverso | Esterilla | PERFIL (Sagital suelo) | Bueno | Baja |
| **s23** | Elevación de Talones | Kettlebell | FRENTE (Coronal) | Bueno | Baja |
| **s24** | Flexiones con Rodillas | Corporal | PERFIL (Sagital suelo) | Bueno | Baja |
| **s25** | Abducción de Cadera con Goma | Goma | FRENTE (Coronal) | Bueno | Baja |
| **m1** | Marcha con Curl Bíceps | Mancuernas | FRENTE (Coronal) | Genérico | Media |
| **m2** | Paso Lateral Empuje Frontal | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m3** | Boxeo Suave | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m4** | Step Touch Elevación Frontal | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m5** | Talones al Glúteo con Remo | Mancuernas | **PERFIL (Sagital)** | **Clon m1 (Inútil)** | **URGENTE** |
| **m6** | Paso en V con Apertura | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m7** | Marcha Maletas | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m8** | Patinador con Balanceo | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m9** | Toque Talón Press Pecho | Mancuernas | PERFIL (Sagital) | **Clon m1** | **URGENTE** |
| **m10** | Sentadilla Corta a Pecho | Mancuernas | **PERFIL (Sagital)** | Frontal genérico | **ALTA** |
| **m11** | Paso Atrás Apertura W | Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m12** | Desplazamiento Lateral Guardia| Mancuernas | FRENTE (Coronal) | **Clon m1** | **URGENTE** |
| **m13** | Marcha Braceo Corto | Mancuernas | **PERFIL (Sagital)** | **Clon m1** | **URGENTE** |
| **m14** | Sentadilla a Silla al Pecho | Mancuernas | **PERFIL (Sagital)** | Frontal genérico | **URGENTE** |
| **m15** | Remo Dorsal Codos Pegados | Mancuernas | **PERFIL (Sagital)** | **Clon m1 (Grave)** | **URGENTE** |
| **m16** | Elevaciones Plano Escapular | Mancuernas | FRENTE (Coronal 30º) | **Clon m1** | **URGENTE** |
| **m17** | Peso Muerto Rumano Asistido | Mancuernas | **PERFIL (Sagital)** | **Clon m1 (Grave)** | **URGENTE** |
| **m18** | Patada de Tríceps a 2 Manos | Mancuernas | **PERFIL (Sagital)** | **Clon m1 (Opuesto)**| **URGENTE** |
| **m19** | Curl de Bíceps Martillo | Mancuernas | FRENTE (Coronal) | **Clon m1** | **ALTA** |
| **m20** | Zancada Estática | Mancuernas | **PERFIL (Sagital)** | **Sentadilla (Error)**| **CRÍTICA** |
| **m21** | Pájaros Deltoides Posterior | Mancuernas | **PERFIL / 3/4 OBLICUO** | **Clon m1** | **URGENTE** |
| **m22** | Sentadilla Sumo Central | Mancuernas | FRENTE (Coronal) | Sentadilla genérica | **ALTA** |
| **m23** | Elevación Talones Gemelos | Mancuernas | FRENTE (Coronal) | **Clon m1** | **ALTA** |
| **m24** | Press Pecho Esterilla (Floor) | Mancuernas | PERFIL (Sagital suelo) | Aceptable | Media |
| **m25** | Apertura Pecho Esterilla | Mancuernas | **DECÚBITO SUPINO CENITAL**| **Clon m24 (Press)** | **URGENTE** |

---

## 8. RECOMENDACIONES TÉCNICAS PARA EL SUBAGENTE DE CÓDIGO/DISEÑO

1. **Prioridad Absoluta de Ejecución**:
   - Reemplazar en primer lugar los SVGs de `m14`, `m15`, `m17`, `m18`, `m20` y `m25` en `dumbbell_data.json` y en `index.html` (`EXERCISE_SVGS`), ya que son los ejercicios con errores anatómicos que inducen a mala ejecución técnica en las usuarias.
2. **Uso de Clases CSS Nativas**:
   - Cada SVG debe contener exactamente dos grupos: `<g class="gif-step1">` y `<g class="gif-step2">`.
   - No insertar scripts internos en los SVGs; la animación por fotogramas ya está gobernada por las reglas CSS `@keyframes gifFrame1` y `@keyframes gifFrame2` de `index.html`.
3. **Optimización de Trazos**:
   - Mantener las coordenadas limpias con un decimal máximo (`stroke-linecap="round"` y `stroke-linejoin="round"`).
   - Respetar los colores y grosores establecidos en la sección 3 para preservar la coherencia estilística de la app.

---
*Fin de la Especificación Biomecánica Maestra — Sergio Fit*
