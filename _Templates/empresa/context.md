<!-- Creado: AAAA-MM-DD · Actualizado: AAAA-MM-DD · Creador: <nombre> -->

# <Nombre de la empresa>

> **Este archivo se lee PRIMERO** en cualquier trabajo de esta empresa. Es su fuente de verdad.

## Ficha

| Campo | Valor |
|---|---|
| Id (carpeta, no se cambia) | `<slug>` |
| Nombre (display) | <nombre> |
| Estado | `estado: activa`  <!-- activa / pausada / archivada --> |
| Qué hace | <una línea: qué vende y a quién> |
| Etapa | <idea / validación / operando / escalando> |
| Modelo de negocio | <suscripción / servicios / transaccional / mixto> |
| Equipo | <cuántas personas y qué roles> |
| Moneda | <moneda de reporte> |
| Publicación | `publicacion: markdown` |
| Versión de plantilla | `template_version: v1` |

**Campo `publicacion:`** — a dónde se publican los documentos generados. `markdown` (default, no publica a ningún
lado) o el nombre de la herramienta externa configurada. Si no hay backend, el ciclo funciona igual: solo se salta
el paso de publicar. Lo consume la skill `publicar-doc`.

## Áreas de esta empresa

**Declara aquí las áreas que esta empresa realmente tiene.** El ruteo de documentos se hace contra esta tabla, no
contra ningún catálogo del framework. Borra las que no apliquen, renombra las que se llamen distinto, agrega las que
falten. Cada área declarada debe existir como carpeta con su propio `context.md`.

| Carpeta | Qué vive aquí |
|---|---|
| `Company/` | la empresa misma y su estrategia: contexto, equipo, objetivos, decisiones de rumbo, indicadores |
| `Producto/` | el qué y el para quién: catálogo y hoja de ruta |
| `Ingeniería/` | infraestructura y deuda técnica transversal, no atada a un proyecto concreto |
| `Ventas/` | pipeline, propuestas, contratos |
| `Marketing/` | demanda y posicionamiento: mercado, competidores, contenido |
| `Operaciones/` | procesos del día a día y coordinación |
| `Finanzas/` | dinero y administración: reportes, métricas, costos |
| `Legal/` | contratos, términos, cumplimiento normativo |
| `Misc/` | bandeja de entrada — lugar definitivo sin decidir |

> **Catálogo sugerido, no obligatorio.** Una consultora quizá reemplace `Producto/` por `Servicios/` y `Entregas/`.
> Un e-commerce quizá agregue `Logística/`. Ninguna empresa necesita las nueve.

## Carpetas de servicio (siempre presentes)

| Carpeta | Qué vive aquí |
|---|---|
| `_GTD/Proyectos/<slug>/` | el cómo de cada proyecto: `propuesta.md`, `exploracion.md`, `solucion.md`, `tareas.md` |
| `_GTD/Tareas-Sueltas/<slug>/` | trabajo que cabe en una página: solo `propuesta.md` |
| `_Referencias/` | archivos de afuera que se consultan para entender un contexto + `index.md` |
| `Decisiones/` | bitácora de decisiones de esta empresa, por quarter |

## Reglas propias de esta empresa

<Reglas que solo aplican aquí: convenciones de nombres, región de nube, tono de la marca, quién aprueba qué.
Si no hay ninguna todavía, deja la sección y escribe "ninguna por ahora".>

## Qué NO sale de esta carpeta

<Lo que nunca se publica hacia afuera ni se cita en otra empresa. Como mínimo: todo lo que cae bajo el Invariante #0
del CLAUDE.md raíz — datos personales de clientes finales.>

---

## Sobre los campos de control

**`estado:`** — `activa` (default), `pausada` o `archivada`. La resolución de empresa **solo ofrece las activas**.
Para dar de baja una empresa no borres nada: cambia este campo a `pausada` o `archivada` y registra el hito en
`_global/Decisiones/`, porque la baja es un evento del portafolio. El árbol se conserva; deja de aparecer en los paneles.

**`template_version:`** — la versión de `_Templates/empresa/` con la que se creó esta empresa. Cuando la plantilla
evoluciona, esta empresa **no cambia sola**: `_Templates/CHANGELOG.md` dice qué cambió entre versiones y qué aplicar
a mano. Sin este campo, a la quinta empresa tendrías cinco dialectos y las tablas de ruteo dejarían de ser ciertas.

**`Id` vs `Nombre`** — la carpeta es el identificador y no se renombra nunca: todas las referencias cuelgan de ella.
Si la empresa cambia de nombre comercial, cambia el campo `Nombre`, no la carpeta.
