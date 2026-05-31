# Grupo Clouds - Migración a React (TP2 Frontend)

- [LINK VERCEL](https://tp-2-front-end-desarrollo-de-sistem.vercel.app/)

## Descripción

Este proyecto es la migración a **React** de la web grupal "Grupo Clouds", originalmente desarrollada en HTML, CSS y Vanilla JS para el TP1. 
Se ha reestructurado por completo utilizando una arquitectura basada en componentes (Component-Based Architecture) para mejorar la escalabilidad, el mantenimiento y el rendimiento, manteniendo intacta la identidad visual corporativa ("Atmospheric Logic" y "Relámpago Dorado" en modo oscuro).

## Novedades de la Migración a React

- **Vite + React:** El proyecto ha abandonado la carga estática tradicional por el empaquetador ultrarrápido Vite junto con React.
- **Enrutamiento del lado del cliente (SPA):** Reemplazo de los múltiples archivos `.html` (`index.html`, `bitacora.html`, `eduardo.html`, etc.) por `React Router DOM`. La navegación ahora es instantánea sin recargas de página.
- **Componentización:** Toda la UI ha sido desglosada en componentes funcionales reutilizables (`Navbar.jsx`, `Footer.jsx`, `MovieCarousel.jsx`, `TechStack.jsx`, etc.).
- **Manejo de Estado (Hooks):** La lógica imperativa que residía en `js/main.js` (manipulación directa del DOM mediante `getElementById` y `classList`) fue convertida a un enfoque declarativo utilizando `useState` y `useEffect`. Esto aplica al Menú Móvil, el Theme Toggle y el Carrusel de Películas.
- **Single Source of Truth:** La información de los integrantes (perfiles, películas, discos, stack técnico) que antes estaba repetida y codificada en duro en 4 HTMLs distintos, ahora se centraliza en un único archivo de datos `src/data/teamData.js`. Un solo componente (`ProfilePage.jsx`) se encarga de renderizar la vista de cualquier integrante.

## Integrantes

- Eduardo Moreno - [Perfil dinámico en `/eduardo`]
- Leandro Paryszewski - [Perfil dinámico en `/leandro`]
- Marcelo Moreno - [Perfil dinámico en `/marcelo`]
- Melissa Galeano - [Perfil dinámico en `/melissa`]

## Tecnologías utilizadas

- **React 18** (Librería principal)
- **Vite** (Build Tool)
- **React Router DOM** (Navegación SPA)
- **JSX** (Sistema de renderizado y marcado)
- **CSS3** puro (Arquitectura global consolidada, sin frameworks)
- Google Fonts & Material Symbols Outlined

## Estructura del proyecto en React

- `index.html`: Punto de entrada principal de Vite, contiene la precarga de fuentes.
- `src/main.jsx`: Proveedor del enrutador y punto de anclaje (`ReactDOM.createRoot`).
- `src/App.jsx`: Declaración de rutas y componente raíz de la aplicación.
- `src/components/`: Componentes modulares de la interfaz:
  - `Navbar.jsx`: Controla navegación y menú slideout.
  - `MovieCarousel.jsx`: Carrusel autónomo.
  - `TechStack.jsx` / `TechIcons.jsx`: Renderizado mapeado de íconos SVG.
  - `Footer.jsx`, `MusicGrid.jsx`, `BackToTop.jsx`.
- `src/pages/`: Vistas completas de la aplicación (`HomePage`, `BitacoraPage`, `ProfilePage`).
- `src/data/teamData.js`: Arreglo de objetos exportable con la data del equipo.
- `src/styles/style.css`: Consolidación de todos los estilos modulares del proyecto original adaptados para React.

## Guía de Estilos — "Atmospheric Logic"

La identidad visual del proyecto se rige por el design system **[Atmospheric Logic](Documentacion/Proyecto-Core/DESIGN.md)**.

### Paleta de Colores

| Rol | Hex | Uso |
|---|---|---|
| Primario | `#006591` | Acciones principales, marca |
| Primario Contenedor | `#0ea5e9` | Acentos, highlights, gradientes |
| Secundario | `#006c4f` | Estados de éxito |
| Superficie (canvas) | `#fbf8fc` | Fondo base |
| Superficie Elevada | `#ffffff` | Tarjetas, elementos interactivos |
| Texto | `#1b1b1e` | Nunca negro puro (`#000000`) |

**Modo Oscuro:** El primario muta a dorado `#ffeebb` ("Relámpago Dorado").

**Reglas del sistema de diseño:**
- **"No-Line Rule":** Prohibidos los bordes sólidos de `1px`. La separación se logra con cambios tonales de fondo.
- **Glassmorphism:** Superficie al 70% de opacidad con `backdrop-blur: 24px` para navbars y modales.
- **Botones:** Gradiente a 135° (`#006591` → `#0ea5e9`), radio `0.75rem`.
- **Tarjetas:** Radio `1.5rem`, sin divisores internos.

### Tipografías

| Rol | Fuente | Google Fonts |
|---|---|---|
| Títulos / Display | **Plus Jakarta Sans** | [Abrir en Google Fonts](https://fonts.google.com/specimen/Plus+Jakarta+Sans) |
| Cuerpo / Labels | **Inter** | [Abrir en Google Fonts](https://fonts.google.com/specimen/Inter) |

### Iconografía

- **[Material Symbols Outlined](https://fonts.google.com/icons)** — íconos vectoriales (peso `300`, tamaño `24px`) servidos desde Google Fonts.

## Lógica Refactorizada (Hooks)

- `Navbar.jsx`: Maneja el overlay móvil, el menú slide-out y el botón "Dark Mode" de forma reactiva con `useState`. Escucha la tecla `Escape` con `useEffect` para cerrar menús, y previene el scroll global al abrir la navegación móvil (`document.body.style.overflow`).
- `MovieCarousel.jsx`: Reemplaza completamente el viejo slider manual. Maneja el slide activo y el iframe de video en reproducción mediante estados independientes. Garantiza que el reproductor incrustado de YouTube (iframe) se detenga al cambiar de slide o cerrarse.
- `App.jsx`: Hook de efecto (`useEffect`) inicial que lee el tema guardado en `localStorage` o `window.matchMedia` (preferencias del sistema) al montarse, evitando reseteos al recargar.

## Uso de IA en la Migración

Durante esta migración se utilizó un agente autónomo de IA integrado (Antigravity/Gemini) para:
- Leer y mapear la arquitectura monolítica antigua del TP1.
- Refactorizar las estructuras HTML largas y complejas a componentes funcionales JSX modernos.
- Extraer los datos textuales estáticos hacia un modelo JSON exportable (`teamData.js`).
- Portar y consolidar la modularización CSS hacia un entorno de Single Page Application.

## Documentación Complementaria

- [Repositorio TP1 — HTML/CSS/JS (versión original)](https://github.com/EduMMorenolp/TP-FrontEnd-DesarrolloDeSistemasWeb)
- [Consigna TP1](Documentacion/Proyecto-Core/Consigna%20TP1.md)
- [Consigna TP2](Documentacion/Proyecto-Core/Consigna%20TP2.md)
- [Arquitectura del Proyecto](Documentacion/Proyecto-Core/Arquitectura.md)
- [Design System — Atmospheric Logic](Documentacion/Proyecto-Core/DESIGN.md)
- [Bitácora del Equipo](Documentacion/Bitacora/Bitacora/Index-Bitacora.md)
- [Bitácora de IA](Documentacion/Bitacora/BitacoraIA/Index-BitacoraIA.md)

## Galería de Vistas

A continuación, se presentan las capturas de pantalla automáticas de las diferentes vistas de la aplicación:

### Página Principal (Home)
![Home](Documentacion/img/captura_home.png)

### Bitácora
![Bitácora](Documentacion/img/captura_bitacora.png)

### Proyectos
![Proyectos](Documentacion/img/captura_proyectos.png)

### GitHub
![GitHub](Documentacion/img/captura_github.png)

### Perfiles del Equipo
<details>
  <summary>Eduardo Moreno</summary>
  
  ![Perfil Eduardo](Documentacion/img/captura_perfil_eduardo.png)
</details>

<details>
  <summary>Leandro Paryszewski</summary>
  
  ![Perfil Leandro](Documentacion/img/captura_perfil_leandro.png)
</details>

<details>
  <summary>Melissa Galeano</summary>
  
  ![Perfil Melissa](Documentacion/img/captura_perfil_melissa.png)
</details>

<details>
  <summary>Marcelo Moreno</summary>
  
  ![Perfil Marcelo](Documentacion/img/captura_perfil_marcelo.png)
</details>

