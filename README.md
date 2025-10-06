# Contador de Personas Avanzado 📊

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

**Desarrollado por:** Daniel Terroba Alcala

Una aplicación web robusta y auto-contenida en un solo archivo HTML para el conteo de personas, gestión de aforo y análisis de datos históricos. Diseñada sin frameworks, con un enfoque en la personalización, la accesibilidad y la persistencia de datos local.

![https://i.imgur.com/8a6Q4sS.png](https://i.imgur.com/8a6Q4sS.png)

---

## 📋 Tabla de Contenidos

1.  [**Características Principales**](#características-principales-)
2.  [**Guía Rápida de Inicio**](#guía-rápida-de-inicio-)
3.  [**Análisis Detallado de Funcionalidades**](#análisis-detallado-de-funcionalidades-)
    * [Módulo de Conteo y Visualización](#módulo-de-conteo-y-visualización-en-tiempo-real-)
    * [Módulo de Controles e Interacción](#módulo-de-controles-e-interacción-)
    * [Módulo de Gestión de Datos y Persistencia](#módulo-de-gestión-de-datos-y-persistencia-)
    * [Módulo de Historial y Análisis Gráfico](#módulo-de-historial-y-análisis-gráfico-)
    * [Módulo de Personalización y Temas](#módulo-de-personalización-y-temas-)
    * [Módulo de Accesibilidad](#módulo-de-accesibilidad-e-interacción-avanzada-)
    * [Módulo de Integración y Extras](#módulo-de-integración-y-extras-)
4.  [**Arquitectura y Aspectos Técnicos**](#arquitectura-y-aspectos-técnicos-)
5.  [**Autoría y Licencia**](#autoría-y-licencia-)

---

## ✨ Características Principales

* **Conteo en Tiempo Real:** Interfaz clara con un contador numérico y un *gauge* semicircular que visualiza el aforo.
* **Dos Modos de Operación:** `Modo Libre` para conteo simple y `Modo con Límite` para control de aforo.
* **Gestión de Aforo Inteligente:** Alerta visual al superar el límite con opciones para continuar o establecer un nuevo aforo.
* **Historial Completo:** Guarda "instantes" (snapshots) con título y descripción para contextualizar los datos.
* **Visualización de Datos Avanzada:**
    * **Gráficas de Barras** por semana, mes y año.
    * **Calendario Interactivo** con un mapa de calor (`heatmap`) que muestra los días de mayor actividad.
    * **Gráfica de Líneas** para analizar la evolución del aforo en las últimas 24 horas.
* **Alta Personalización:** 8 temas de color (4 claros, 4 oscuros) y un sistema de modo oscuro/claro.
* **Enfoque en Accesibilidad:** `Modo Accesible` con fuentes más grandes, soporte para lectores de pantalla y anuncios por voz (TTS).
* **Gestión de Datos:** Importa y exporta la base de datos completa en formato `JSON` y los instantes en `CSV`.
* **Widget Integrable:** Genera un código `<iframe>` para incrustar el contador en cualquier página web.
* **Sin Dependencias Externas:** Funciona de forma autónoma en un solo archivo HTML, usando `localStorage` para persistencia.
* **Modo "Fiestuqui" 🎉:** Un divertido *easter egg* que anima el contador con figuras danzantes.

---

## 🚀 Guía Rápida de Inicio

1.  **Abrir la aplicación:** Simplemente abre el archivo `HTML` en cualquier navegador moderno.
2.  **Establecer Aforo:** Si usas el `Modo con Límite`, define el aforo máximo a través del menú de opciones (⚙️) -> `Cambiar Modo`.
3.  **Contar:** Usa los botones `+1`, `-1`, `+10`, `-10` para ajustar el contador.
4.  **Registrar un Momento:** Pulsa `Guardar instante` para guardar el conteo actual. Puedes añadirle un título y una descripción para recordar por qué ese momento fue importante (ej. "Inicio de concierto", "Promoción activa").
5.  **Analizar Datos:** Explora la sección `Histórico y Gráficas`. Cambia entre la vista de `Gráfica` y `Calendario` y filtra por `Semana/Mes/Año` para descubrir patrones.

---

## 🛠️ Análisis Detallado de Funcionalidades

### Módulo de Conteo y Visualización en Tiempo Real  visu

* **Contador Numérico (`#gauge-count`):** El corazón de la app. Muestra el número actual. Usa `aria-live="polite"` para ser accesible con lectores de pantalla.
* **Gauge Semicircular (`#gauge-canvas`):** Renderizado con `<canvas>`, este medidor visualiza la ocupación actual respecto a la capacidad máxima. El color de la barra cambia de verde (seguro), a amarillo (precaución) y rojo (límite alcanzado o superado).
* **Indicador de Capacidad (`#gauge-capacity`):** Debajo del contador, muestra el aforo máximo y el porcentaje de ocupación (`/ 100 (50%)`) o el texto "Modo Libre".
* **Semáforo de Aforo (`#traffic-light`):** Un círculo de color que provee una señal visual rápida del estado del aforo, complementado por una etiqueta de texto descriptiva.

### Módulo de Controles e Interacción 🕹️

* **Botones de Ajuste Rápido:** `+1`, `-1`, `+10`, `-10` para modificaciones ágiles.
* **Ajuste Personalizado (`#btn-custom`):** Abre un modal para sumar o restar cualquier cantidad específica, útil para correcciones grandes.
* **Guardar Instante (`#btn-save`):** Abre un modal para registrar el estado actual. Permite añadir:
    * **Título (`#snapshot-title-input`):** Para nombrar eventos (ej. "Partido de fútbol").
    * **Descripción (`#snapshot-note-input`):** Para añadir contexto (ej. "Día lluvioso, menos gente de lo esperado").
* **Reset (`#btn-reset`):** Reinicia el contador actual a `0` tras una confirmación. **Importante:** No borra el historial de instantes.
* **Gestión de Límite de Aforo (`#exceed-limit-modal`):**
    * **Detección Automática:** Si en `Modo con Límite` se intenta superar el aforo, la operación se pausa y se muestra un modal de advertencia.
    * **Opciones del Usuario:** El modal permite `Cancelar` la acción o `Confirmar y Continuar`, superando el aforo.
    * **Ajuste Manual Opcional:** Incluye un checkbox para, tras confirmar, abrir directamente el modal de `Establecer Aforo Máximo` con el nuevo valor como mínimo, facilitando la actualización del límite.

### Módulo de Gestión de Datos y Persistencia 💾

* **Base de Datos Local (`localStorage`):** La aplicación guarda todo el estado (`state`) en el `localStorage` del navegador. Esto incluye el conteo actual, la configuración y todos los instantes guardados, garantizando que los datos persisten entre sesiones.
* **Exportar Datos (`#export-data-btn` y `#export-csv-btn`):**
    * **JSON:** Exporta el estado completo de la aplicación. Sirve como una **copia de seguridad total** que puede ser restaurada.
    * **CSV:** Exporta la lista de instantes en un formato de tabla, ideal para analizar en hojas de cálculo como Excel o Google Sheets.
* **Importar Datos (`#import-data-btn`):** Permite restaurar la aplicación a un estado previo seleccionando un archivo `.json` exportado anteriormente.
* **Borrar Base de Datos (`#delete-all-data-btn`):** Una opción de alto riesgo en el menú de ajustes que elimina **permanentemente** toda la información guardada. Requiere una doble confirmación con un temporizador de 5 segundos para evitar borrados accidentales.
* **Datos de Demostración (`generateInitialData()`):** Si un usuario abre la aplicación por primera vez y no hay datos, el script genera un historial ficticio y realista de los últimos 30 días para que las gráficas y el calendario tengan contenido y el usuario pueda explorar todas las funcionalidades desde el primer momento.

### Módulo de Historial y Análisis Gráfico 📈

* **Lista de Instantes (`#snapshot-list`):** Muestra los instantes guardados en las **últimas 24 horas** para una revisión rápida. Cada elemento muestra el título, conteo, hora y un botón para eliminarlo.
* **Selector de Vistas y Periodos:** Permite al usuario alternar entre `Gráfica` y `Calendario`, y filtrar el rango de tiempo entre `Semana`, `Mes` y `Año`.
* **Gráfica de Barras (`#history-bar-chart`):** Muestra la **ocupación máxima** registrada para cada día, mes o semana (según el filtro). Las barras son interactivas: al hacer clic en una, se actualiza la gráfica de líneas inferior.
* **Gráfica de Líneas (`#history-line-chart`):** Por defecto, muestra la evolución del conteo en las **últimas 24 horas**. Si se selecciona una barra en la gráfica superior, esta gráfica se actualiza para mostrar la evolución detallada de ese día en concreto.
* **Vista de Calendario (`#calendar-container`):**
    * **Mapa de Calor (`Heatmap`):** Cada día del mes se colorea en función del pico de aforo alcanzado. Días con más gente tienen un color más intenso, permitiendo identificar patrones de un solo vistazo.
    * **Navegación:** Permite moverse entre meses y años. Incluye un selector de año desplegable.
    * **Interactividad:** Al hacer clic en un día, se abre un modal (`#day-notes-modal`) que lista todos los instantes guardados en esa fecha, permitiendo un análisis detallado.
    * **Detalle de Instante:** Desde la lista de instantes del día, se puede hacer clic para ver un modal (`#snapshot-detail-modal`) con toda la información de un registro específico.

### Módulo de Personalización y Temas 🎨

* **Sistema de Temas Basado en Variables CSS:** La apariencia se controla mediante variables CSS, lo que permite cambios de tema instantáneos y fluidos.
* **Selector de Temas (`#theme-selector-btn`):** Abre un panel con **8 temas predefinidos**:
    * **Claros:** Azul Cielo, Bosque Sereno, Atardecer, Minimalista.
    * **Oscuros:** Azul Nocturno, Fiesta Neón, Océano Profundo, Cosmos.
* **Modo Oscuro/Claro (`#dark-mode-switch`):** Un interruptor global que alterna entre las paletas de temas claros y oscuros.
* **Estilos de Botones Dinámicos:** Algunos temas modifican el radio de los bordes de los botones (`--button-border-radius`) para ofrecer una estética diferente (cuadrados, redondeados, píldora).

### Módulo de Accesibilidad e Interacción Avanzada ♿

* **Modo Accesible (`#accessible-mode-switch`):** Al activarse, aumenta el tamaño de las fuentes y los espaciados en toda la aplicación para mejorar la legibilidad.
* **Anuncios por Voz (TTS - Text-to-Speech):**
    * **Anunciar Cambios (`#tts-mode-switch`):** Si se activa, la aplicación narra en voz alta cada cambio en el contador (ej. "Más uno. Total 51").
    * **Lectura a Demanda (`#tts-btn`):** Un botón sobre el *gauge* permite al usuario escuchar el estado actual del aforo en cualquier momento.
* **Atributos ARIA:** El código utiliza etiquetas `aria-label` y `aria-live` para asegurar que los elementos interactivos y la información dinámica sean correctamente interpretados por lectores de pantalla.

### Módulo de Integración y Extras ✨

* **Widget Integrable (`#share-widget-btn`):** Abre un modal que proporciona un código `<iframe>` para incrustar una versión minimalista y en tiempo real del contador en cualquier otra página web. La aplicación detecta si se está ejecutando en modo widget (`?widget=true`) para mostrar solo la vista simplificada.
* **Modo "Fiestuqui" (`#fiestuqui-mode-switch`):** Un *easter egg* que, al activarse, renderiza pequeñas figuras humanas animadas y danzantes dentro del *gauge*. El número de figuras corresponde al contador (con un límite de 500 para mantener el rendimiento).
* **Marca de Agua del Autor (`addWatermark()`):** El script incluye una función que añade una discreta marca de agua con el nombre del autor en la esquina inferior de la pantalla. El texto está ofuscado en Base64 (`atob`) y un `setInterval` asegura que permanezca visible.

---

## 🏗️ Arquitectura y Aspectos Técnicos

* **Stack Tecnológico:** La aplicación está construida exclusivamente con **HTML, CSS y JavaScript (Vanilla JS)**, sin necesidad de frameworks o librerías externas, a excepción de **`Chart.js`** para la renderización de las gráficas.
* **Persistencia:** Se utiliza `localStorage` como única base de datos, lo que la convierte en una aplicación 100% *client-side* (se ejecuta enteramente en el navegador del usuario) y *offline-first*.
* **Estado Centralizado:** Toda la lógica de la aplicación gira en torno a un único objeto `state` de JavaScript. Cualquier cambio en este objeto y su posterior guardado en `localStorage` se refleja en la interfaz a través de la función `updateUI()`, siguiendo un patrón de diseño simple y efectivo.
* **Diseño Responsivo:** La interfaz se adapta a pantallas más pequeñas (menos de 900px), reorganizando la disposición de los elementos para una mejor experiencia en dispositivos móviles.

---

## ©️ Autoría y Licencia

Este proyecto ha sido concebido y desarrollado en su totalidad por **Daniel Terroba Alcala**.

El código fuente incluye menciones de autoría y copyright. Actualmente no se especifica una licencia de software formal en un archivo `LICENSE.md`, por lo que, por defecto, se rige bajo la ley de **copyright estándar ("Todos los derechos reservados")**.

Para permitir su uso, modificación o distribución, se recomienda al autor añadir un archivo `LICENSE.md` con una licencia de software apropiada (ej. MIT para código abierto, o una licencia restrictiva como CC BY-NC-ND si se desea limitar su uso).
