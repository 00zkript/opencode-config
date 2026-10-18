---
name: Laravel / PHP
description: Convenciones, generadores y comandos para proyectos Laravel/PHP. Úsala al trabajar en un proyecto Laravel.
---

# Laravel / PHP

## Generadores (siempre antes de crear a mano)
- `php artisan make:model Post -mfs`, `make:controller`, `make:request`,
  `make:resource`, `make:migration`, `make:test`, `make:middleware`, `make:job`,
  `make:event`, `make:listener`, `make:policy`, `make:seeder`, `make:factory`.
- Dependencias: `composer require vendor/paquete` (nunca editar `vendor/`).
- Pruebas rápidas: `php artisan tinker`.

## Convenciones
- PSR-12 con `laravel/pint` (formato) y `phpstan`/`larastan` (estático).
- Modelos en singular (`User`), tablas en plural (`users`), controladores
  `PascalCase` + `Controller`.
- Migraciones **siempre** con `make:migration`: usa el timestamp real; crear a mano
  con `0000_` es mala práctica.
- Controladores delgados; la lógica va en servicios/actions; validación con `FormRequest`.
- Eager loading (`with`) para evitar N+1.

## Arquitectura típica
- `app/Http` (entrada), `app/Models` (Eloquent), `app/Services` o `app/Actions`
  (casos de uso), `app/Http/Resources` (salida API), `database/` (migraciones, seeders).

## Calidad y comandos
- Formato: `./vendor/bin/pint`
- Estático: `./vendor/bin/phpstan analyse`
- Tests: `php artisan test` (Pest o PHPUnit)
- Migraciones: `php artisan migrate`
- Humo: `php artisan route:list`, `php artisan about`

## Errores comunes
- Migraciones/seeds creados a mano con nombres o timestamps incorrectos.
- Falta de índices y foreign keys en migraciones.
- Consultas dentro de bucles (N+1).
- Validar en el controlador en vez de en un `FormRequest`.
