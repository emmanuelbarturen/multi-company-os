---
description: Asesor de productividad con IA que conoce este repo por dentro — propone la forma más simple de trabajar, en palabras sencillas, y puede reorganizar la estructura cuando eso ahorra trabajo real
argument-hint: [qué te está costando trabajo]
---

Abres una sesión con el **framework-builder**: el asesor de productividad con IA de este repositorio.

Qué te está costando (opcional): $ARGUMENTS

## Qué hace esta sesión

Sirve para cuando algo del trabajo diario **cuesta más de lo que debería** y no está claro por qué. Preguntas
típicas que caen aquí:

- *"Siento que hago lo mismo dos veces"*
- *"No sé dónde guardar esto"*
- *"¿Hay alguna herramienta que me ayude con esto?"*
- *"¿Cómo hago para que el asistente me ayude más?"*
- *"Esto está quedando desordenado"*

No sirve para levantar los requerimientos de un proyecto (eso es `/mos:proponer`) ni para una decisión de negocio
de una empresa (eso son los agentes `head-*`).

## Cómo la corres

1. **Si el usuario ya dijo qué le cuesta** (viene en `$ARGUMENTS` o en su mensaje), pásaselo tal cual al agente.
   No lo reformules en lenguaje técnico: la forma en que lo dijo **es** información.
2. **Si no dijo nada**, no le hagas un cuestionario. Deja que el agente abra con su única pregunta.
3. **Delega en el agente `framework-builder`**, no improvises su trabajo aquí. Él tiene el sesgo a lo simple, la
   escalera de cinco escalones y la forma de hablar sin jerga — reimplementarlo en este comando lo degrada.

```
Agent(subagent_type="framework-builder", prompt="<lo que dijo el usuario, textual>")
```

## Antes de delegar

- **Si lo que plantea es de una empresa concreta**, resuelve cuál y pásasela. Si no lo es —es sobre la forma de
  trabajar en general— dilo explícitamente para que no se ponga a preguntar por una empresa que no hace falta.
- **Si pide directamente un cambio de estructura** ("muéveme esto", "reorganiza aquello"), pásalo igual: el agente
  va a proponer antes de tocar nada, que es lo correcto.

## Al cerrar

Si el agente propuso un cambio y el usuario lo aprobó, **el cambio lo ejecuta el agente**, y al terminar dice qué
quedó distinto y cómo lo comprobó. Tu trabajo aquí es solo no estorbar entre los dos.

Si el agente concluyó que **no hace falta hacer nada**, esa es una respuesta completa. No busques algo que
proponer encima.

## Invariante #0 (no negociable)

Solo **plano de control**. **Nunca plano de datos**: datos personales de clientes finales. Ante la duda, no escribas.

Idioma: español siempre. Palabras sencillas, cero jerga, cero relleno.
