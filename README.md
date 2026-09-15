<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Multi-Company OS

**Un framework de trabajo para operar varias empresas desde un solo repositorio, con un asistente de IA como copiloto.**

No es software. Es una estructura de carpetas, un ciclo de trabajo y una capa de agentes que convierten a Claude Code
en alguien que sabe cómo está organizada tu operación — o tus operaciones, en plural.

Todo en español. Sin build, sin dependencias, sin instalación: clonas y funciona.

---

## La idea en tres frases

1. **Cada carpeta se autodescribe.** Un `context.md` por carpeta dice qué vive ahí y qué no. Es lo único que hace que
   un asistente sin memoria entienda una carpeta que no escribió.
2. **Todo trabajo tiene un solo hogar, dentro de una empresa nombrada.** El ciclo `/mos:explorar → /mos:proponer → /mos:aplicar →
   /mos:archivar` lo lleva de idea a archivo, siempre en `<empresa>/_GTD/`.
3. **Ningún dato de cliente entra.** Aquí vive cómo opera el negocio, nunca los datos de las personas a las que sirve.

El framework aporta ese contrato. **Cada empresa aporta su vocabulario**: sus áreas, sus procesos, sus reglas.

---

## Arrancar en 3 pasos

```
1. Copia esta carpeta a donde trabajes y ábrela con Claude Code.
2. Corre /mos:setup — define tus empresas y sus áreas, borra los ejemplos y declara tus MCPs.
3. Corre /mos:explorar y cuéntale el primer problema que quieras resolver.
```

Eso es todo. El paso 2 es de una sola vez; después, cada empresa nueva entra con `/mos:empresa-nueva`.

Si en el paso 2 configuraste algún MCP, **reinicia la sesión antes del paso 3**: el registro de servidores MCP se
congela al arrancar, así que no cargan hasta que vuelvas a abrir.

---

## Qué trae

**6 comandos** — uno de arranque y cinco para el ciclo de vida de todo trabajo.

| Comando | Para qué |
|---|---|
| `/mos:setup` | **Una sola vez:** define empresas y áreas, limpia los ejemplos, declara los MCPs |
| `/mos:empresa-nueva` | Da de alta una empresa más: declara sus áreas y crea su esqueleto |
| `/mos:explorar` | Piensa una idea sin compromiso. No escribe archivos salvo que se lo pidas |
| `/mos:proponer` | Entrevista en vivo → propuesta, solución y plan de tareas |
| `/mos:aplicar` | **Ejecuta** el plan de tareas y marca progreso verificado |
| `/mos:archivar` | Cierra el trabajo, lo mueve a `Archived/` y registra el hito |

**6 agentes** — tres para llevar un trabajo de idea a tareas, tres como consejo directivo.

| Agente | Para qué |
|---|---|
| `project-requirements` | Levanta requerimientos con priorización MoSCoW |
| `project-tech-lead` | Cierra el cómo: cada hueco termina en Decisión o en Spike |
| `project-manager` | Descompone el plan en tareas atómicas y verificables |
| `head-ceo` | Juicio estratégico bajo incertidumbre |
| `head-cfo` | Pricing, márgenes, economía unitaria, caja |
| `head-marketing` | Posicionamiento: contra qué compites y para quién |

**3 skills** — `diagrama-flujo` (Mermaid embebido), `wireframes` (baja fidelidad primero), `publicar-doc`
(publica a la herramienta que uses, o no publica y no falla).

> **Todos los comandos llevan el prefijo `/mos:`.** No es decoración: en Claude Code la subcarpeta de
> `.claude/commands/` **es** el namespace, así que los cinco viven en `.claude/commands/mos/`. Eso los separa de los
> comandos nativos y de cualquier plugin que tengas instalado. Si agregas un comando propio, va en esa carpeta.

**Plantillas** — `_Templates/empresa/` para dar de alta empresas, `_Templates/area-context.md` para declarar áreas,
`_Templates/proyecto/` con los cuatro documentos de un trabajo.

---

## Qué NO trae (a propósito)

- **Ninguna integración obligatoria.** Publicar a una herramienta externa es opcional y se declara por empresa. Sin
  configurar nada, todo se queda en Markdown y el ciclo funciona igual.
- **Ningún catálogo de áreas impuesto.** Hay uno sugerido; cada empresa lo recorta, lo renombra o lo ignora.
  `empresa1` tiene seis áreas y `empresa2` tiene cinco, con solo dos nombres en común. Es deliberado.
- **Ninguna dependencia de plugins, marketplaces ni skills externas.** Funciona con Claude Code estándar.
- **Ningún dato de negocio real.** Las dos empresas de ejemplo son ficticias.

---

## Las cuatro reglas que lo sostienen

Están completas en `CLAUDE.md`, que es lo que el asistente lee al abrir cada sesión. En resumen:

**Regla #1 — clasifica antes de ejecutar.** En la primera respuesta de cada sesión: ¿en qué empresa, y es un trabajo
nuevo o una pregunta suelta? Nada se ejecuta antes.

**Resolución de empresa.** Se resuelve por lo que digas, por el path en juego, o por la empresa ya fijada en la
conversación. Si nada de eso aplica, el asistente **pregunta**. Nunca asume.

**Aislamiento entre empresas.** El contexto de una empresa no entra en los documentos de otra. Si un aprendizaje sirve
a varias, se abstrae hasta perder el dato y sube a `_Templates/`. Es el riesgo que solo aparece al pasar de una a
varias, y la fuga es silenciosa. **Todo vive dentro de una empresa** — incluida su bitácora de decisiones: no hay
carpetas de contenido en la raíz.

**Invariante #0 — plano de control, nunca plano de datos.** Aquí vive cómo opera la empresa: ingresos, conteos,
funnel, decisiones, procesos. Nunca los datos personales de sus clientes finales. Solo agregados y derivadas.

---

## Estructura

```
.
├── CLAUDE.md              ← reglas globales y tablas de ruteo
├── .claude/               ← ÚNICA capa de IA: 6 agentes, 6 comandos, 3 skills
├── .mcp.example.json      ← plantilla de servidores MCP, sin credenciales
├── _Templates/            ← empresa, área, proyecto
├── empresa1/              ← EJEMPLO: SaaS B2B, 6 áreas
└── empresa2/              ← EJEMPLO: consultora, 5 áreas
```

Y dentro de cada empresa: su `context.md`, una carpeta por área declarada, `_GTD/Proyectos/` y `_GTD/Tareas-Sueltas/`,
`_Ingesta/` para material crudo y `Decisiones/` para su bitácora.

---

## Cómo crece

Agregar un agente o una skill es: crear el archivo en `.claude/`, registrar su fila en la tabla correspondiente de
`CLAUDE.md`, y mencionarlo aquí. **Un comando va en `.claude/commands/mos/`** para que herede el prefijo `/mos:`.
La capa es única y compartida: lo que agregues sirve para todas tus empresas.

El repo funciona **en local, sin git**. Si prefieres versionarlo, `.gitignore` ya está listo; si no, nada lo exige.

---

## Antes de compartir una copia

Este framework está pensado para compartirse — pasando la carpeta, un zip o un repo. La fuga de dato propio no ocurre
la primera vez: ocurre a la décima, cuando ya nadie revisa. Corre estos tres chequeos desde la raíz antes de entregar
una copia, y si alguno devuelve algo, revísalo a mano.

```bash
# 1. Marca, dominio o nombres propios que no deberían salir
grep -ril -E 'tu-marca|tu-dominio\.com|nombres-de-clientes' .

# 2. Rutas absolutas de tu máquina (se excluye este README, que contiene el patrón)
grep -rl '/Users/\|/home/' . --exclude=README.md

# 3. Qué empresas viajan en la copia (deberían ser solo las de ejemplo)
find . -maxdepth 2 -name context.md -not -path './_Templates/*'
```

El chequeo 1 lo adaptas a tus términos: pon ahí el nombre de tus empresas, tus dominios y los nombres de tus
clientes. El objetivo es que salgan **cero resultados** en los dos primeros, y solo `empresa1` y `empresa2` en el tercero.

Y borra `.mcp.json` de la copia si lo creaste: ahí viven tus credenciales. El `.mcp.example.json` es el que se comparte.
