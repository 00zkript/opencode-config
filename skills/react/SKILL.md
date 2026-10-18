---
name: React
description: Convenciones y generadores para proyectos React. Úsala junto al pack TypeScript.
---

# React

> Complementa el pack **TypeScript / JS / Node**.

## Andamiaje
- SPA: `npm create vite@latest -- --template react-ts`.
- SSR: `npx create-next-app`.

## Convenciones
- Componentes **funcionales**; hooks siempre en el nivel superior (nunca condicionales).
- Componentes en `PascalCase`, uno por archivo.
- Estado local con `useState`/`useReducer`; global solo si hace falta (Zustand/Redux/Context).
- `useEffect` solo para sincronizar con el exterior; dependencias completas.
- Tipar props directamente (evitar `React.FC`).

## Arquitectura típica
- `src/components` (UI), `src/features/<feature>` (dominio), `src/hooks`,
  `src/api`, `src/routes`.

## Calidad y comandos
- Dev: `npm run dev`
- Lint: `npx eslint . --fix`
- Tipos: `npx tsc --noEmit`
- Tests: `npx vitest` + `@testing-library/react`
