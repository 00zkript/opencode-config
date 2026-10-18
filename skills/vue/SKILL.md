---
name: Vue
description: Convenciones y generadores para proyectos Vue 3. Úsala junto al pack TypeScript.
---

# Vue

> Complementa el pack **TypeScript / JS / Node**.

## Andamiaje
- `npm create vue@latest` (Vite + TS + Router + Pinia).
- Componentes con `<script setup lang="ts">` (Composition API).

## Convenciones
- Composition API con `<script setup>`; props tipadas con `defineProps<Props>()`.
- Componentes en `PascalCase`, archivos `PascalCase.vue`.
- Estado global con **Pinia** (no Vuex en proyectos nuevos); un store por dominio.
- Vistas en `views/`, reutilizables en `components/`.
- `computed` para derivar; `watch` solo para efectos; nunca mutar props.

## Arquitectura típica
- `src/components` (UI), `src/views` (páginas), `src/stores` (Pinia),
  `src/composables` (lógica `useXxx`), `src/router`, `src/api`.

## Calidad y comandos
- Dev: `npm run dev`
- Lint/formato: `npm run lint`
- Tipos: `npx vue-tsc --noEmit`
- Tests: `npx vitest` (+ `@vue/test-utils`)
