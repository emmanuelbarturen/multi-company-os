<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Cambios de las plantillas

Las empresas se crean **copiando** `_Templates/empresa/`. Eso significa que una empresa creada hoy no se actualiza
sola cuando la plantilla cambie mañana: **el drift está garantizado si nadie lo registra.**

Este archivo es ese registro. Cada vez que cambies algo en `_Templates/`, sube la versión y escribe aquí **qué
cambió** y **qué hay que aplicar a mano** en las empresas que ya existen. Luego actualiza el campo
`template_version:` de las empresas que migres.

## v1 — 2026-09-15

Versión inicial. `_Templates/empresa/` (context.md con ficha, tabla de áreas declarables, `_GTD/`, `_Ingesta/index.md`,
`Decisiones/`), `_Templates/area-context.md` y `_Templates/proyecto/` (propuesta · exploración · solución · tareas).

Campos de control en la ficha de empresa: `estado`, `template_version`, e `Id` separado de `Nombre`.

**Migración desde versiones anteriores:** no aplica.
