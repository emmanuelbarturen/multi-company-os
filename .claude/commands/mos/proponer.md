---
description: Crea o modifica la propuesta de un trabajo — tarea suelta (1 archivo con checklist) o trabajo completo (entrevista en vivo → propuesta, solución y plan de tareas). Sesión retomable vía el bloque Estado
argument-hint: [trabajo o tema]
---

Conduces una sesión para **proponer** un trabajo: definir su **qué**, su **cómo** y su **plan de tareas ejecutable**.
**No delegas la entrevista a un subagente**: la corres TÚ en el hilo principal, porque solo el hilo principal puede
interactuar turno a turno. Adoptas los playbooks de `project-requirements` (lotes de 3-5 preguntas, MoSCoW, alcance
dentro/fuera) y `project-tech-lead` (cada "por validar" termina en Decisión o Spike).

**Contrato del comando: una propuesta no se cierra sin su plan de tareas** — `tareas.md` en trabajo completo, o el
checklist `## Tareas` dentro de `propuesta.md` en tarea suelta. Ese plan es lo que `/mos:aplicar` ejecuta.

Trabajo o tema (opcional): $ARGUMENTS

## 0. Resolver la empresa — SIEMPRE PRIMERO

Antes de leer o escribir nada: lo que diga el usuario → el path en juego → la empresa ya fijada en esta conversación
→ `AskUserQuestion` con las empresas existentes. **Nunca elijas tú.** Resuelta, lee su `context.md`.

Todas las rutas de aquí en adelante son relativas a `<empresa>/`.

## Dónde vive todo (los drafts locales son la fuente de verdad)

**Tarea suelta** (cabe en una página, un actor, sin decisiones técnicas propias, ≤5 tareas)
→ `<empresa>/_GTD/Tareas-Sueltas/{slug}/propuesta.md`: objetivo, contexto, checklist `## Tareas`, bloque `## Estado`.

**Trabajo completo** (requerimientos formales, decisiones técnicas propias, o lo construye alguien más)
→ `<empresa>/_GTD/Proyectos/{slug}/`, nombres fijos:

- `propuesta.md` — el **qué y por qué**: objetivo, alcance dentro/fuera, requerimientos MoSCoW, criterios de aceptación, `## Estado`.
- `exploracion.md` — **discovery**: opciones consideradas, referencias, preguntas abiertas que aún no son spec.
- `solucion.md` — el **cómo**: enfoque, tabla de Decisiones, tabla de Spikes, riesgos, mapa a requerimientos.
- `tareas.md` — **el plan ejecutable**: tareas atómicas numeradas por dependencias. Obligatorio al cerrar.

Parte de `_Templates/proyecto/`. La publicación externa es solo un destino en hitos y cierre, nunca la copia de
trabajo. Todo `.md` lleva su cabecera de metadatos.

## 1. ¿En qué trabajamos?

El nombre puede venir en $ARGUMENTS. **Si no viene, no lo inventes:** escanea los trabajos de esta empresa y
muéstralos en un panel.

```bash
find "<empresa>/_GTD" -mindepth 3 -maxdepth 3 -name 'propuesta.md' ! -path '*/Archived/*' 2>/dev/null
```

Presenta con `AskUserQuestion` (header "Trabajo"): una opción por carpeta **más "➕ Nuevo"** al final. Deriva
`{slug}` y decide la rama:

- **Nuevo** → §2.
- **Existente sin cerrar** (su `## Estado` está en fase explorar/mos:proponer con frentes abiertos) → lee todos sus docs,
  resume en 3-5 líneas (qué está documentado, qué falta, próximo paso) y **retoma la entrevista donde quedó**.
- **Existente ya documentado** (requerimientos cerrados y plan de tareas hecho) → **modo cambio** (§5).

## 2. Calibrar alcance (solo si es nuevo)

`AskUserQuestion` (header "Alcance"): **Tarea suelta** / **Trabajo completo**, con la heurística de arriba en las
descriptions y tu recomendación marcada. Si a mitad de camino una tarea suelta crece — aparece una decisión técnica
propia, pasa de cinco tareas, o lo va a construir alguien más — dilo y **gradúala**: mueve la carpeta a
`_GTD/Proyectos/`, expande `propuesta.md` al formato completo y suma los otros tres documentos.

## 3. Rama tarea suelta

Un solo lote de 3-5 preguntas: problema real · resultado esperado · qué NO entra · tareas concretas. Con las
respuestas escribe `propuesta.md` desde `_Templates/proyecto/propuesta.md`, con el checklist `## Tareas` numerado por
dependencias (01 antes que 02). Salta a §6.

## 4. Rama trabajo completo (entrevista en vivo)

1. **Cimientos:** crea `propuesta.md` con su bloque `## Estado` y `exploracion.md`. Si `/mos:explorar` dejó conclusiones,
   hereda esos bullets como punto de partida.
2. **Loop de requerimientos** (playbook `project-requirements`): lotes de **3-5 preguntas** priorizadas por impacto.
   Cubre antes de cerrar: **problema real · actor · resultado esperado y su métrica · alcance dentro y fuera · flujo
   principal · reglas y casos borde · restricciones · prioridad**. No avances si el problema o el alcance siguen ambiguos.
3. **Documentar, con visto bueno:** cuando un frente quede estable, pregunta *"Esto ya está definido, ¿lo documento?"*
   e indica a cuál documento va — discovery y preguntas abiertas a `exploracion.md`; lo que ya es spec a `propuesta.md`
   (alcance, requerimientos con MoSCoW, criterios "Dado / Cuando / Entonces"). Tras escribir, **actualiza `## Estado`**:
   eso es lo que hace la sesión retomable.
4. **Cierre de requerimientos:** `AskUserQuestion` (header "Siguiente"): **Definir la solución ahora** (recomendado —
   sin el cómo, las tareas se armarían sobre decisiones no tomadas) / **Dejarla pendiente**.
5. **Loop de solución** (playbook `project-tech-lead`) → `solucion.md`: relee propuesta y exploración, identifica los
   huecos, pregunta en lotes de 3-5. **Decisión vs Spike es la regla clave:** cada hueco termina en **Decisión**
   (resoluble ahora — respeta las convenciones declaradas en `<empresa>/context.md` y reusa lo que la empresa ya
   tiene antes de inventar; justifica en una o dos líneas) o en **Spike** (validación empírica con objetivo, método y
   **criterio de éxito medible**). La fase no cierra con un hueco bloqueante sin Decisión ni Spike.
6. **Cierre obligatorio — el plan de tareas** → `tareas.md`: descompón el alcance en tareas atómicas con el playbook
   de `project-manager`. **Una tarea es atómica cuando quien la recibe sabe qué entregar y cómo se comprueba, sin
   volver a preguntar.** Numeradas por dependencias, agrupadas por etapas, cada una con su verificación. Es un draft
   local: preséntalo y ajústalo con el usuario antes de dar la propuesta por cerrada.

## 5. Modo cambio (trabajo ya documentado)

El cambio puede venir en $ARGUMENTS; si no, pídelo en una línea. Clasifícalo (si dudas, di tu lectura y confírmala):

- **Funcional** (alcance, requerimiento, flujo, regla, métrica) → playbook requirements → edita `propuesta.md`.
- **Técnico** (enfoque, servicio, una Decisión o un Spike) → playbook tech-lead → edita `solucion.md`. Respeta las
  decisiones ya tomadas; si el cambio las contradice, decláralo como decisión que **se revierte o actualiza**, no lo escondas.
- **Ambos** → primero el qué, luego el cómo. No los mezcles en el mismo lote.

Pregunta solo lo que el cambio deja ambiguo; no re-levantes lo ya cerrado. **Edita quirúrgicamente.**
**Coherencia obligatoria:** un Must nuevo en `propuesta.md` necesita su fila en el mapa de `solucion.md`.
**Y siempre actualiza `tareas.md`:** tacha las tareas que el cambio invalida con una línea de por qué, y añade las
nuevas al final de su etapa. Cierra actualizando `## Estado`.

## 6. Cierre

Actualiza `## Estado` (si el plan quedó listo: **Fase: aplicar**). Ofrece con `AskUserQuestion`
(`multiSelect: true`, header "Cierre"):

1. **Publicar la documentación** → skill `publicar-doc`. Si `<empresa>/context.md` no declara backend en
   `publicacion:`, esta opción no aparece.
2. **Ejecutar ahora** → indícale correr `/mos:aplicar {slug}`.
3. **Crear wireframe** → skill `wireframes`.
4. **Crear diagrama de flujo o arquitectura** → skill `diagrama-flujo`.

Delega en cada skill, no reimplementes su trabajo. Si no selecciona nada, cierra sin más.

## Invariante #0 (no negociable)

Solo **plano de control**. **Nunca plano de datos**: datos personales de clientes finales en ningún draft ni en
ninguna publicación. Si un ejemplo arrastra un dato personal, abstráelo. Ante la duda, no escribas.

**Aislamiento:** no cites datos de otra empresa en estos documentos.

Idioma: español siempre. Directo, breve, cero relleno.
