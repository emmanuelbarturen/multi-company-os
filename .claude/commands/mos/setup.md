---
description: Configura el repo por primera vez — define las empresas y sus áreas, limpia los ejemplos y deja los servidores MCP declarados. Se corre una vez al adoptar el framework
argument-hint: (sin argumentos)
---

Pones el framework a punto **la primera vez**. Al terminar, el repo tiene las empresas reales del usuario con sus
áreas declaradas, sin rastro de los ejemplos, y los servidores MCP que vaya a usar ya escritos en `.mcp.json`.

Este comando se corre **una vez**. Después, cada empresa nueva entra por `/mos:empresa-nueva`.

## 0. Reconocer el terreno

Antes de preguntar nada, mira qué hay:

```bash
find . -maxdepth 2 -name 'context.md' -not -path './_Templates/*' -not -path './.claude/*'
```

- **No aparece ninguna** → repo recién clonado, punto de partida limpio. Sigue al paso 1.
- **Aparecen empresas** → el repo ya está en uso, o se clonó desde la rama `ejemplo-de-uso`. **Dilo y pregunta**
  con `AskUserQuestion` si quiere (a) agregar empresas a lo que ya hay, (b) solo configurar MCPs, o (c) cancelar.
  **Nunca reconfigures un repo en uso sin que te lo confirme.**

Cuenta también qué hay en `.mcp.json`: si ya existe, este comando **añade**, no reemplaza.

## 1. Las empresas

Pregunta en una línea: *"¿Qué empresas vas a manejar en este repo? Dame sus nombres."* Acepta la lista en una sola
respuesta; no las pidas de a una.

Por cada nombre, deriva el `{slug}` en kebab-case y **confírmale la lista completa de slugs antes de crear nada** —
el slug es el identificador y no se renombra después.

Si menciona una sola empresa, no insistas: el framework funciona igual con una, y las demás entran después con
`/mos:empresa-nueva`.

## 2. Las áreas de cada empresa — una empresa a la vez

**Las áreas se definen aquí con el usuario, nunca por tu cuenta.** Por cada empresa, en orden:

1. Pregunta en una línea qué hace y en qué etapa está — lo justo para llenar su ficha.
2. Presenta el catálogo sugerido de `_Templates/empresa/context.md` con `AskUserQuestion`
   (`multiSelect: true`, header "Áreas"), con el nombre de la empresa en la pregunta para que se sepa cuál es.
   La opción nativa de texto libre sirve para áreas que no estén en el catálogo.

**No agregues ni una sola área que no haya marcado.** Ni porque la otra empresa la tiene, ni porque parezca que
falta, ni para dejar la estructura simétrica. **Dos empresas del mismo dueño pueden tener áreas completamente
distintas, y eso es lo normal, no un error.**

Si una carpeta de área ya existe en el árbol, no la toques: pregunta qué hacer con ella (poblar su `context.md`,
dejarla como está, o excluirla de la tabla).

## 3. Crear la estructura

Por cada empresa confirmada:

1. Copia `_Templates/empresa/` a `{slug}/`.
2. Crea una carpeta por área declarada, cada una con su `context.md` desde `_Templates/area-context.md`, con la
   responsabilidad redactada — no en blanco.
3. Rellena `{slug}/context.md`: la ficha del paso 2 y la tabla de áreas recortada a lo declarado.
4. Estampa los campos de control: `Id` = `{slug}`, `estado: activa`, y `template_version:` = la versión que
   encabeza `_Templates/CHANGELOG.md`.
5. Registra el alta en `_global/Decisiones/Q<N>-<AAAA>.log` — el alta es un evento del portafolio, no de la
   empresa. La bitácora de la empresa arranca vacía a propósito.
6. Fecha de hoy en todas las cabeceras `<!-- Creado: … -->`.

## 4. Limpiar los ejemplos — solo si los hay

La rama `main` viene **sin empresas**, así que lo normal es que este paso no aplique: dilo en una línea y sigue.

Aplica solo si el repo se clonó desde la rama `ejemplo-de-uso`, que trae dos empresas inventadas. En ese caso
pregunta con `AskUserQuestion` (header "Ejemplos"): **Borrarlas** (recomendado, una vez que ya tiene las suyas) /
**Conservarlas** (si quiere seguir consultándolas).

Si acepta, bórralas. **No las borres sin preguntar**, aunque el paso 3 haya salido bien.

## 5. Los servidores MCP

Los MCP son las fuentes de datos externas del asistente. **Son opcionales: el framework funciona sin ninguno.**

1. Muéstrale `.mcp.example.json` y pregunta, en una sola tanda, **qué fuentes necesita** — su gestor de documentos,
   su calendario, su nube, su base de datos, su herramienta de diseño. Que responda en lenguaje natural; tú traduces
   a servidores.
2. Por cada uno, escribe su entrada en `.mcp.json` (créalo si no existe; si existe, **añade**, no reemplaces).
3. **Las credenciales nunca van en el archivo.** Usa siempre referencias a variables de entorno —
   `"API_KEY": "${MI_API_KEY}"` — y dile dónde tiene que exportarlas. Si te ofrece una clave en el chat,
   **no la escribas en ningún archivo** y recuérdale que la ponga en su entorno.
4. Registra la fila de cada servidor en la tabla `Necesito data de → MCP` de `CLAUDE.md`. Un MCP configurado pero
   no registrado ahí es un MCP que el asistente no sabrá cuándo usar.

### El gotcha que siempre muerde

**El registro de servidores MCP se congela cuando arranca la sesión.** Escribir `.mcp.json` ahora mismo **no
los activa**: siguen sin existir para esta conversación. Díselo explícitamente al cerrar:

> Los MCP quedaron escritos, pero **no cargan hasta que reinicies la sesión**. Si alguno usa OAuth, son dos pasos
> seguidos: primero reiniciar para que se cargue, después autenticar desde `/mcp` ya dentro de la sesión nueva.
> Autenticar antes de reiniciar es imposible.

No prometas que un MCP "ya está funcionando" cuando solo escribiste su configuración. No lo has probado.

## 6. Confirmar

Devuelve en pocas líneas: las empresas creadas con sus áreas, si se borraron los ejemplos, los MCP declarados, y
los dos siguientes pasos: **reiniciar la sesión** (si configuró MCPs) y **`/mos:explorar`** para arrancar el primer
trabajo.

Si el repo llegó con empresas de ejemplo y decidió conservarlas, recuérdale que están ahí y que no son suyas.

## Invariante #0 (no negociable)

Solo **plano de control**. **Nunca plano de datos**: datos personales de clientes finales. Y ninguna credencial
escrita en un archivo del repo — solo referencias a variables de entorno.

Idioma: español siempre. Directo, breve, cero relleno.
