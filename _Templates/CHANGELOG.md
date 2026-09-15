<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Cambios de las plantillas

Las empresas se crean **copiando** `_Templates/empresa/`. Eso significa que una empresa creada hoy no se actualiza
sola cuando la plantilla cambie mañana: **el drift está garantizado si nadie lo registra.**

Este archivo es ese registro. Cada vez que cambies algo en `_Templates/`, sube la versión y escribe aquí **qué
cambió** y **qué hay que aplicar a mano** en las empresas que ya existen. Luego actualiza el campo
`template_version:` de las empresas que migres.

## v2 — 2026-09-15

`_Ingesta/` pasa a llamarse **`_Referencias/`**, y su descripción se reescribió.

**Por qué:** el nombre sugería la primera etapa de un proceso — algo que entra y hay que procesar. Su intención real
siempre fue otra: un lugar de archivos que se **consultan** para entender mejor un contexto. La descripción vieja
reforzaba el malentendido ("material crudo", "insumo", "toda alta o procesamiento"), así que no bastaba con renombrar
la carpeta.

**Qué cambió, concretamente:**

- La carpeta, en la plantilla y en cada empresa.
- El texto de la convención en `CLAUDE.md`: ahora dice explícitamente que **no es una bandeja que haya que vaciar** y
  que un archivo puede quedarse ahí años sin que nadie lo procese, sin que eso sea deuda.
- Los estados del `index.md`: `sin procesar / en análisis / procesado / descartado` →
  `disponible / en uso / citado / obsoleto`. Los viejos describían un flujo; los nuevos describen disponibilidad.
- Las columnas del `index.md`: «Origen» → «De dónde salió», «Quién lo consume» → «Para qué sirve».

**Migración desde v1:** renombrar `<empresa>/_Ingesta/` a `<empresa>/_Referencias/`, actualizar la fila de la tabla de
carpetas de servicio en `<empresa>/context.md`, y reemplazar la cabecera de su `index.md`. Los archivos guardados no se
tocan. Sube `template_version:` a `v2`.

## v1 — 2026-09-15

Versión inicial. `_Templates/empresa/` (context.md con ficha, tabla de áreas declarables, `_GTD/`, `_Referencias/index.md`,
`Decisiones/`), `_Templates/area-context.md` y `_Templates/proyecto/` (propuesta · exploración · solución · tareas).

Campos de control en la ficha de empresa: `estado`, `template_version`, e `Id` separado de `Nombre`.

**Migración desde versiones anteriores:** no aplica.
