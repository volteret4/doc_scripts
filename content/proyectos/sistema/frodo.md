+++
title = 'Frodo'
weight = 5
+++

App de escritorio con **Tauri 2 + SvelteKit** (TypeScript, `adapter-static`) — sin
README propio más allá del título, pero la estructura del código es clara:
`src/routes/+page.svelte` como pantalla principal, `src/lib/Sidebar.svelte` +
`AddModal.svelte` para navegación y alta de elementos, `store.svelte.ts` para estado
compartido (runas de Svelte 5) y `presets.ts` con configuraciones predefinidas — el
patrón típico de una app de gestión de una lista de "cosas" (proyectos, tareas o
similar) con barra lateral, más un modal para añadir entradas nuevas.

```bash
npm run dev       # vite dev
npm run tauri dev # ventana nativa vía Tauri
npm run build
```
