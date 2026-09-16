---
description: Cierra un trabajo terminado — mueve su carpeta a Archived/, registra el hito en Decisiones y actualiza el estado en el backend de publicación si lo hay
argument-hint: [trabajo]
---

Cierras un trabajo: verificas su plan, lo mueves a `Archived/` y dejas el hito en la bitácora. Es el final del ciclo.

Trabajo (opcional): $ARGUMENTS

## 0. Resolver la empresa — SIEMPRE PRIMERO

Lo que diga el usuario → el path en juego → la empresa ya fijada en la conversación → `AskUserQuestion`.
**Nunca elijas tú.** Todas las rutas son relativas a `<empresa>/`.

## 1. ¿Qué archivamos?

Si no viene en $ARGUMENTS, escanea los trabajos activos y muéstralos en un panel:

```bash
find "<empresa>/_GTD" -mindepth 3 -maxdepth 3 -name 'propuesta.md' ! -path '*/Archived/*' 2>/dev/null
```

`AskUserQuestion` (header "Trabajo"). Si no hay nada, dilo y detente. Deriva `{slug}`.

## 2. Pre-chequeo

Lee el plan de tareas y el bloque `## Estado`.

- **Al 100%** → sigue directo.
- **Con pendientes** → `AskUserQuestion` (header "Pendientes"): **Archivar igual** (anota en `## Estado` una línea con
  por qué se cierra con pendientes y cuáles son) / **Cancelar** (vuelve con `/mos:aplicar {slug}`).

## 3. Cierre en el backend de publicación

Solo si `<empresa>/context.md` declara un backend en `publicacion:` y el trabajo tiene enlace en su `## Estado`:
pregunta el estado final con `AskUserQuestion` (header "Estado"): **Terminado** / **Archivado sin terminar** /
**En pausa** (en este caso **no muevas la carpeta**: actualiza el Estado y termina). Actualiza allá vía `publicar-doc`.

Sin backend o sin enlace, sáltate este paso y dilo en el resumen final.

## 4. Mover a Archived/

1. Actualiza `## Estado`: **Fase: archivado**, fecha de hoy, y la fecha `Actualizado:` de la cabecera.
2. Mueve la carpeta completa a `Archived/` dentro de la misma rama (`_GTD/Proyectos/Archived/{slug}/` o
   `_GTD/Tareas-Sueltas/Archived/{slug}/`). El set completo de documentos viaja intacto.
   **No renombres la carpeta con la fecha:** la fecha de cierre vive en el Estado y en la bitácora.

## 5. Bitácora

Añade una línea al archivo del quarter actual en `<empresa>/Decisiones/Q<N>-<AAAA>.md`
(Q1 ene-mar, Q2 abr-jun, Q3 jul-sep, Q4 oct-dic). Si el trabajo afectó a **varias** empresas, escribe la misma línea
marcada `[cross]` en la bitácora de cada una. Solo si la decisión no pertenece a ninguna empresa en particular —
un cambio de foco del portafolio, por ejemplo — va a `_global/Decisiones/`:

```
AAAA-MM-DD — Archivado <slug>: <resultado en una línea>.
```

## 6. Confirmar

Devuelve: ruta final, estado en el backend (o "sin publicación"), la línea escrita en la bitácora, y las pendientes
documentadas si las hubo.

## Invariante #0 — chequear ANTES de escribir (no negociable)

Solo **plano de control**. **Nunca plano de datos**: aplica a todo lo que se publique. Si un draft arrastra datos
personales de clientes finales → **aborta y repórtalo**.

Idioma: español siempre. Directo, breve, cero relleno.
