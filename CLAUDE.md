<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# CLAUDE.md

Guía para Claude Code al trabajar en este repositorio.

## Qué es este repo

**Multi-Company OS** es un framework de trabajo para operar **varias empresas** desde un solo repositorio, con un
asistente de IA como copiloto. No es un proyecto de software: es un conjunto de documentos Markdown que retratan cada
empresa por función de negocio, más una capa de agentes, comandos y skills compartida por todas.

No hay build, ni lint, ni tests. **El producto son los `.md`.** Todo se escribe en español.

El framework aporta el **contrato** — toda carpeta se autodescribe, todo trabajo tiene un solo hogar dentro de una
empresa nombrada, ningún dato de cliente entra. Cada empresa aporta su **vocabulario** — sus áreas, sus procesos, su
gente. Ninguna empresa es especial: la primera se trata igual que la décima.

---

## Regla #1 — antes de ejecutar, clasifica DOS cosas

**Irrefutable.** En la **primera respuesta de cada sesión**, antes de ejecutar nada, resuelve con `AskUserQuestion`:

1. **¿En qué empresa?** — ver *Resolución de empresa* abajo.
2. **¿Qué tipo de trabajo?** — (a) un trabajo nuevo que arranca con `/mos:explorar`, o (b) una pregunta suelta.

Nada se ejecuta hasta que ambas estén resueltas.

Se salta solo cuando el primer mensaje ya las responde por sí mismo: nombra la empresa e invoca un comando del ciclo,
retoma un proyecto existente por su nombre, o es la lectura trivial de un archivo ya nombrado. **En la duda, pregunta.**

> Por qué: sin la clasificación de trabajo, lo que merecía entrar al ciclo `/mos:explorar → /mos:proponer → /mos:aplicar → /mos:archivar`
> termina como conversación suelta y se pierde. Sin la clasificación de empresa, termina escrito en la empresa equivocada.

---

## Resolución de empresa

Con varias empresas en el mismo repo, **saber en cuál estás es un paso explícito, nunca una suposición**. El orden de
resolución es este, y el primero que dé resultado gana:

1. **El usuario la nombra** en su mensaje ("en la consultora…", "para empresa1…").
2. **El path lo determina:** el archivo o carpeta en juego está bajo `<empresa>/`.
3. **La sesión ya la fijó:** una empresa resuelta antes en esta misma conversación sigue vigente hasta que el usuario la
   cambie.
4. **Nada de lo anterior aplica** → `AskUserQuestion` con las empresas existentes como opciones. **Nunca elijas tú.**

Una vez resuelta, **lee `<empresa>/context.md` antes de cualquier otra cosa**: ahí están su ficha, su tabla de áreas y
sus reglas propias.

**Solo se ofrecen empresas con `estado: activa`.** Las pausadas o archivadas se ofrecen únicamente si el usuario las
nombra explícitamente, y al abrirlas dilo en una línea.

### Cambio de empresa a mitad de sesión — recontextualiza

Cambiar de empresa **no es cambiar de carpeta: es cambiar de cabeza.** Cuando el usuario diga "y en la otra empresa…",
haz estas tres cosas antes de responder cualquier cosa:

1. **Dilo en voz alta:** "cambio a `<empresa>`".
2. **Relee `<empresa>/context.md`** completo. No asumas que se parece a la anterior.
3. **Descarta los supuestos de la empresa anterior** — sus áreas, sus reglas, sus números, sus convenciones. Nada de
   eso viaja.

> Este es el modo de falla que **no existía** con una sola empresa y que ninguna regla de rutas atrapa: nadie escribió
> en la carpeta equivocada, pero el razonamiento venía contaminado. Es el error más barato de evitar y el más caro
> de no evitar.

**Si la resolución falla** — el usuario nombra una empresa que no existe, o el path es ambiguo — **pregunta y
detente**. Nunca tomes la primera carpeta de la lista ni la última empresa usada como default.

**Trabajo que cruza empresas** (comparar dos, mover algo de una a otra, una decisión que afecta a varias): se nombra
explícitamente como cross-empresa y se registra en la bitácora de **cada empresa afectada**, con la misma línea
marcada `[cross]`. **No existe bitácora fuera de una empresa:** toda decisión pertenece a alguien.

---

## Regla de aislamiento entre empresas

**El contexto de una empresa no entra en los documentos de otra.** Nunca. Ni ejemplos, ni cifras, ni nombres, ni
"lo que funcionó allá".

- Al escribir en `<empresa-A>/`, no cites datos de `<empresa-B>`. Si necesitas la comparación, la conclusión se
  escribe en cada bitácora por separado, sin arrastrar las cifras de la otra.
- Si un aprendizaje sirve a varias empresas, **se abstrae hasta perder el dato** y sube a `_Templates/`.
  Lo que sube es la forma, no el caso.
- Al leer para responder algo de una empresa, no cargues los `context.md` de las otras.

> Por qué: es el riesgo que solo aparece al pasar de una empresa a varias, y la fuga es silenciosa — nadie se entera
> hasta que un documento de un cliente cita a otro.

**El aislamiento es sobre los datos, no sobre la atención.** Quien opera varias empresas tiene una sola cabeza y una
sola agenda: que los datos no se mezclen no significa que el trabajo no pueda tocar dos empresas. Cuando un trabajo
las toca:

- **Declara un dueño.** El trabajo vive en `<empresa-dueña>/_GTD/`, no en las dos.
- **Deja el espejo.** En la otra empresa, una línea en su `Decisiones/` que apunte al trabajo, sin copiar su contenido.
- **La decisión se registra en todas.** La misma línea, marcada `[cross]`, en la bitácora de cada empresa afectada.

> **Hueco conocido:** no hay un `_GTD/` en la raíz. Un ítem genuinamente transversal — el mismo contador para todas,
> una decisión de portafolio — hoy se resuelve con la forma de arriba. Si con el uso resulta insuficiente, la
> siguiente iteración es un `_GTD/` raíz mínimo. Está declarado a propósito, no olvidado.

---

## Invariante #0 — plano de control, nunca plano de datos

**Regla que define qué puede existir en este repo:** aquí vive solo el *plano de control* de cada empresa — **cómo
opera**: ingresos, conteos, runway, funnel, decisiones, procesos. **Nunca** el *plano de datos* de sus productos: datos
personales de clientes finales, documentos de identidad, registros individuales, credenciales.

No traigas registros con identidad individual a estos documentos ni al contexto del modelo. **Solo agregados y
derivadas.** Si un ejemplo arrastra un dato personal, abstráelo. Ante la duda, no lo escribas.

Aplica a todo: documentos, diagramas, prompts, salidas de MCPs y cualquier cosa que se publique hacia afuera.

---

## Estructura

```
.
├── CLAUDE.md              ← este archivo: reglas globales y tablas de ruteo
├── README.md              ← qué es el framework y cómo arrancar
├── .claude/               ← ÚNICA capa de IA, compartida por todas las empresas
│   ├── agents/            ← 6 agentes
│   ├── commands/mos/      ← 6 comandos (la subcarpeta ES el namespace /mos:)
│   ├── skills/            ← 3 skills
│   └── settings.json
├── .mcp.example.json      ← plantilla de servidores MCP, sin credenciales
├── _Templates/            ← plantillas: empresa, área, proyecto
│   ├── empresa/           ← lo que copia /mos:empresa-nueva
│   ├── area-context.md
│   └── proyecto/
├── empresa1/              ← EJEMPLO didáctico — bórralo
└── empresa2/              ← EJEMPLO didáctico — bórralo
```

Y dentro de cada empresa:

```
<empresa>/
├── context.md             ← ficha + TABLA DE ÁREAS + reglas propias   ← se lee PRIMERO
├── <área>/context.md      ← una carpeta por área declarada
├── _GTD/
│   ├── Proyectos/<slug>/  ← propuesta.md · exploracion.md · solucion.md · tareas.md
│   │   └── Archived/
│   └── Tareas-Sueltas/<slug>/  ← solo propuesta.md
│       └── Archived/
├── _Ingesta/              ← material crudo sin procesar + index.md
├── _Templates/            ← plantillas propias de esta empresa (opcional)
└── Decisiones/            ← bitácora de ESTA empresa
```

### Las áreas son libres — y por eso cada empresa declara las suyas

Un e-commerce, una consultora y una SaaS no tienen las mismas áreas. **El framework no impone un catálogo.** Cada
empresa declara su tabla de áreas en su `context.md`, y **el ruteo se hace contra esa tabla declarada, nunca contra
un catálogo asumido**.

`_Templates/empresa/context.md` trae un catálogo *sugerido* como punto de partida. Recórtalo, renómbralo, amplíalo.

**Al crear un documento, ubícalo por función, no por tema.**

**Cuando ninguna área declarada encaja** — pasa, porque el catálogo lo escribe cada empresa y las tablas de ruteo de
más abajo no pueden ser exhaustivas contra un catálogo libre: **pregunta**, ofreciendo las áreas declaradas más la
opción de crear una nueva. No lo metas a la fuerza en la que más se parece. Si eso ocurre dos veces con el mismo tipo
de documento, falta declarar un área.

**Cuando el trabajo no encaja con ningún agente** de las tablas de abajo, usa el `head-` que corresponda por función
(estrategia, dinero, mercado) o resuélvelo en el hilo principal. La tabla es un mapa, no una barrera.

**Una empresa con una sola área es válida.** No infles el catálogo para que se vea completo.

### Las áreas no se crean solas — nunca

**Un área se declara con el usuario, en `/mos:setup` o en `/mos:empresa-nueva`, y en ningún otro momento.** Ninguna
sesión crea una carpeta de área por su cuenta, por más obvia que parezca la necesidad. Si al ubicar un documento
descubres que falta un área:

1. **Pregunta** con `AskUserQuestion`: crear el área, o ubicar el documento en una de las ya declaradas.
2. Si el usuario acepta, crea la carpeta **y** su `context.md` **y** agrega su fila a la tabla de
   `<empresa>/context.md`. Las tres cosas, o la tabla deja de ser cierta y el ruteo se cae.

**Si una carpeta de área ya existe pero no tiene `context.md`** — alguien la creó a mano — **tampoco la pueblas en
silencio.** Pregunta qué es esa carpeta y qué debe decir su `context.md`. Una carpeta que ya existe tiene intención
detrás; escribirle encima un `context.md` inventado la borra.

**El nombre de carpeta es el identificador.** Renombrarlo rompe todas las referencias. Si la empresa cambia de nombre
comercial, **deja la carpeta como está** y cambia el campo `nombre` de su `context.md`: la carpeta es el `id`, el
campo es lo que se muestra.

### `context.md` es la fuente de verdad de su carpeta

**Lee el `context.md` antes de crear, mover o editar cualquier documento de una carpeta.** Arranca con la
responsabilidad del área y debajo lleva sus reglas y datos operativos. Si una carpeta aún no tiene `context.md`,
aplican las reglas de este archivo — y créalo.

---

## Convenciones de todo el repo

**Metadatos en cada `.md`.** Todo archivo lleva arriba tres datos: fecha de creación, fecha de actualización y creador.
Al crear, escríbelos; al editar, actualiza la fecha de actualización.

```markdown
<!-- Creado: AAAA-MM-DD · Actualizado: AAAA-MM-DD · Creador: <nombre> -->
```

**Dónde van los planes.** Dos tipos. (1) **Plan de proyecto** (alcance o diseño de un proyecto concreto) →
`<empresa>/_GTD/Proyectos/<slug>/solucion.md`. (2) **Cualquier otro plan** (plan-mode, scratch de sesión) → `/Plans/`
en la raíz, que es donde el harness de plan-mode escribe y no se puede redirigir. Cuando un plan se aprueba y se
empieza a implementar, escribe arriba la **fecha de ejecución**; si va en varias tandas, registra cada una.

**Bitácora de decisiones — siempre dentro de una empresa.** Toda **decisión importante, cambio de definición o
hito** se registra de forma legible para humanos, con fecha, una línea o bloque por evento, en
`<empresa>/Decisiones/Q<N>-<AAAA>.log`.

**No hay bitácora en la raíz.** Una decisión que afecta a varias empresas se escribe en la de **cada una**, con la
misma línea marcada `[cross]`. Duplicar una línea es más barato que perder el registro — y quien lee la bitácora de
una empresa ve todo lo que la afecta, sin tener que saber que existe otro archivo en otro lado.

Los cambios del **framework** no van a ninguna bitácora de empresa: si tocan plantillas, van a
`_Templates/CHANGELOG.md`; si tocan doctrina, se editan directamente en este archivo.

No entra aquí el trabajo rutinario ni el detalle de implementación: solo lo que cambia el rumbo o la definición.
El quarter se determina por la fecha actual (Q1 ene-mar, Q2 abr-jun, Q3 jul-sep, Q4 oct-dic).

**Material crudo.** Lo que llega de afuera sin procesar va a `<empresa>/_Ingesta/<Categoría>/`, a **un solo nivel** y
categorizado por tipo de documento, no por extensión. `_Ingesta/index.md` es un registro vivo obligatorio: toda alta o
procesamiento actualiza su fila. Es insumo, no conclusión — el análisis resultante va a su área y cita la fuente.

**Publicación hacia afuera.** El repo es la fuente de verdad. Publicar a una herramienta externa (Notion, un wiki, un
gestor de tareas) es **opcional**: se declara en el campo `publicacion:` de `<empresa>/context.md`. Sin backend
configurado, todo se queda en Markdown y nada falla.

---

## Infraestructura de IA — agentes, comandos, skills y MCPs

> **Sección router.** Como `CLAUDE.md` es el único archivo que Claude carga siempre al abrir sesión, **esta es la fuente
> de verdad de qué usar y cuándo**, aunque los componentes también se auto-descubran.

**Dónde viven:** los agentes en `.claude/agents/*.md`, los comandos en **`.claude/commands/mos/*.md`**, las skills en
`.claude/skills/*/SKILL.md` y los servidores MCP en `.mcp.json` de la raíz (plantilla en `.mcp.example.json`).

**La subcarpeta es el namespace.** Un archivo en `.claude/commands/mos/` se invoca como `/mos:<archivo>`. Todo comando
propio de este framework va ahí, sin excepción: el prefijo `mos:` lo separa de los comandos nativos de Claude Code y
de cualquier plugin que tengas instalado. Un comando suelto en `.claude/commands/` quedaría sin prefijo y podría
colisionar.
**Una sola copia, compartida por todas las empresas.** Para dar de alta un componente: (1) crea el archivo,
(2) registra su fila aquí, (3) menciónalo en `README.md`.

### Situación → Comando (el ciclo de vida de todo trabajo)

| Situación / disparador | Comando |
|---|---|
| **Primera vez en el repo**: definir empresas y áreas, limpiar ejemplos, declarar MCPs | `/mos:setup` |
| Dar de alta una empresa nueva en un repo ya configurado | `/mos:empresa-nueva` |
| Pensar una idea o problema sin compromiso, pesar opciones antes de crear nada | `/mos:explorar` |
| Crear o modificar un trabajo (tarea suelta o proyecto) hasta su plan de tareas | `/mos:proponer` |
| Ejecutar el plan de tareas y publicar lo que corresponda | `/mos:aplicar` |
| Cerrar un trabajo terminado (a `Archived/` + registro en `Decisiones/`) | `/mos:archivar` |

Los cuatro comandos del ciclo **resuelven la empresa antes de escribir nada**. `/mos:setup` se corre **una vez**,
al adoptar el framework; después, cada empresa entra por `/mos:empresa-nueva`.

### Situación → Agente

| Situación / disparador | Agente |
|---|---|
| Levantar requerimientos, definir el alcance de algo nuevo, traducir una idea de negocio a especificación | `project-requirements` |
| Cerrar el cómo técnico: stack, servicios, infraestructura, decisiones de arquitectura, qué es spike y qué no | `project-tech-lead` |
| Descomponer un plan en tareas atómicas para quien las va a ejecutar | `project-manager` |
| Decidir bajo incertidumbre, juicio estratégico, evaluar una apuesta contraria, trabajar la estrategia de la empresa | `head-ceo` |
| Pricing, márgenes, unit economics, runway, control de costos, decisiones de financiamiento | `head-cfo` |
| Posicionamiento, contra qué competimos, elegir segmento o categoría, el funnel no cierra aunque nos conozcan | `head-marketing` |
| _(cada instalación agrega sus filas)_ | — |

### Situación → Skill

| Situación / disparador | Skill |
|---|---|
| Diagrama de flujo, de proceso, de arquitectura o de secuencia | `diagrama-flujo` |
| Wireframe, mockup o prototipo de una pantalla | `wireframes` |
| Publicar un documento generado hacia la herramienta externa de la empresa | `publicar-doc` |
| _(cada instalación agrega sus filas)_ | — |

### Necesito data de → MCP

Esta tabla llega **vacía a propósito**: los MCPs dependen de las herramientas que use cada quien. Declara el servidor
en `.mcp.json` (plantilla en `.mcp.example.json`), habilítalo en `.claude/settings.local.json` si requiere permiso
explícito, y registra su fila aquí.

| Fuente de datos | MCP / herramienta | Notas |
|---|---|---|
| _(vacía — cada instalación agrega sus filas)_ | — | — |

**Regla para MCPs (Invariante #0):** read-only y con lista blanca de campos siempre que sea posible. Nunca traer plano
de datos al contexto del modelo — solo agregados y derivadas.

---

## Notas

- **Este repo es una plantilla.** `empresa1/` y `empresa2/` son ejemplos didácticos con áreas **distintas entre sí**,
  a propósito, para mostrar que las áreas son libres. Bórralos y crea los tuyos con `/mos:empresa-nueva`.
- **Nada aquí depende de una instalación particular de Claude Code.** Los agentes, comandos y skills funcionan con
  Claude Code estándar; no requieren plugins, marketplaces ni skills externas.
- **Este repo se usa en local, sin git.** No hay historial ni remoto: las copias de seguridad y el versionado, si los
  quieres, son cosa tuya fuera del repo. `.gitignore` existe igual, para quien reciba el framework y sí use git.
- **Antes de compartir una copia**, corre los tres chequeos de `README.md` → *Antes de compartir una copia*: el
  objetivo es que ninguna empresa real ni ningún dato propio viajen con ella.
