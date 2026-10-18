---
name: TypeScript / JS / Node
description: Convenciones, generadores y comandos para proyectos JS/TS y Node. Base para proyectos Vue/React/Node.
---

# TypeScript / JS / Node

## Generadores / andamiaje
- Node: `npm init`; front: `npm create vite@latest`; framework: usa su CLI
  (`nest new`, `npx create-next-app`, `npm create vue@latest`).
- Tipos: `npm i -D @types/...`; config: `npx tsc --init`.
- Monorepo: `pnpm`/`npm` workspaces (no carpetas sueltas).

## Convenciones
- **TypeScript por defecto** con `strict: true`; evitar `any` (usar `unknown` + narrowing).
- ESLint + Prettier (o Biome); `--fix` antes de cerrar.
- Nombres: `camelCase` variables/funciones, `PascalCase` tipos/clases/componentes,
  `SCREAMING_SNAKE_CASE` constantes, archivos `kebab-case`.
- ESM (`import`/`export`); sin `require` en código nuevo.
- `async/await` y manejo explícito de errores (nunca `catch` vacío).
- Validar entrada en los bordes con `zod`/`valibot`.

## Arquitectura típica (Node)
- `src/` en capas: `routes`/`controllers` (entrada), `services` (casos de uso),
  `repositories` (datos), `domain` (tipos/reglas). Inyección por parámetros.
- Config con variables de entorno tipadas (`env.ts` + zod).

## Calidad y comandos
- Formato: `npx prettier --write .`
- Lint: `npx eslint . --fix`
- Tipos: `npx tsc --noEmit`
- Tests: `npx vitest run` (o `jest`)
- Ejecutar: `npm run dev` / `npm start`
