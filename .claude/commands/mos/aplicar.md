---
description: Sesión de ejecución sobre el plan de tareas de un trabajo — EJECUTA las tareas (no solo las trackea), marca progreso verificado, y al cierre ofrece publicar la documentación
argument-hint: [trabajo]
---

Conduces una **sesión de ejecución**: tomas el plan de tareas de un trabajo y **lo ejecutas**. Este comando hace las
tareas, no las anota para que alguien más las haga.

Trabajo (opcional): $ARGUMENTS

## 0. Resolver la empresa — SIEMPRE PRIMERO

Lo que diga el usuario → el path en juego → la empresa ya fijada en la conversación → `AskUserQuestion`.
**Nunca elijas tú.** Resuelta, lee su `context.md`. Todas las rutas son relativas a `<empresa>/`.

## 1. ¿Qué ejecutamos?

Si el nombre no viene en $ARGUMENTS, escanea los trabajos con plan y muéstralos en un panel:

```bash
find "<empresa>/_GTD" -mindepth 3 -maxdepth 3 \( -name 'tareas.md' -o -name 'propuesta.md' \) ! -path '*/Archived/*' 2>/dev/null
```

`AskUserQuestion` (header "Trabajo"): una opción por carpeta. Si no hay nada, dilo — no hay planes que ejecutar, se
crean con `/mos:proponer` — y detente.

## 2. Cargar el estado

Lee el plan (`tareas.md`, o el checklist `## Tareas` de `propuesta.md` en tarea suelta) y el bloque `## Estado`.
Lee también `propuesta.md` y `solucion.md` como contexto de **qué** se está construyendo y **cómo**.
Resume en 3-5 líneas: **N de M tareas hechas · bloqueos · próximo paso.**

## 3. Loop de ejecución

Trabaja las tareas **en orden de numeración** (respeta dependencias), o la que el usuario elija. Por cada tanda:

- **Documental u operativa** (redactar un documento del repo, un diagrama, configurar una herramienta, una consulta
  de solo lectura): **la ejecutas tú, aquí.** Gate en una línea ("¿hago la 03 y la 04?") y a trabajar.
  **No conviertas en pregunta lo que ya está decidido en la propuesta.**
- **Técnica en otro repositorio o recurso** (código, infraestructura, despliegue): pide la ruta o el acceso y
  **ejecútala ahí**. Si el usuario decide que la hace él o su equipo, déjala asignada y anota el bloqueo en su línea:
  no la simules ni la marques.
- **Verifica antes de marcar.** Una tarea se marca solo cuando su resultado **existe y lo comprobaste**: el archivo
  está, la página responde, el proceso corre. Marca con `- [x] … (hecha: AAAA-MM-DD)`. Las frases "debería funcionar"
  o "quedó listo" no son verificación.
- Tras cada tanda: actualiza `## Estado` (**Fase: aplicar**, fecha, próximo paso) y la fecha `Actualizado:` de la cabecera.

Respeta lo decidido en `solucion.md`. Si al ejecutar descubres que una decisión no se sostiene, **no la cambies en
silencio**: decláralo y redirige a `/mos:proponer` en modo cambio.

## 4. Cierre

`AskUserQuestion` (`multiSelect: true`, header "Cierre"):

1. **Publicar la documentación** → skill `publicar-doc`. Solo aparece si `<empresa>/context.md` declara backend.
2. **Seguir en otra sesión** — solo actualizar `## Estado`.

Si el plan quedó al **100%**, dilo explícitamente y sugiere `/mos:archivar {slug}`.

## Invariante #0 — chequear ANTES de escribir (no negociable)

Solo **plano de control**. **Nunca plano de datos**: si un draft o una tarea arrastra datos personales de clientes
finales → **aborta y repórtalo**, no escribas. **Aislamiento:** no traigas datos de otra empresa.

Idioma: español siempre. Directo, breve, cero relleno.
