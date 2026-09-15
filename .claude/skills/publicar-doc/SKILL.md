---
name: publicar-doc
description: Publica documentación generada hacia la herramienta externa que la empresa haya declarado en el campo `publicacion:` de su context.md. Si no hay backend configurado, degrada en silencio a markdown y no falla. Valida el Invariante #0 (nunca datos personales de clientes finales) antes de escribir. USE WHEN publicar documento, subir la doc, sincronizar con la herramienta, publicar el proyecto, dónde va este documento. NOT FOR reestructurar la herramienta externa, NOT FOR publicar datos personales de clientes finales.
---

# publicar-doc

Publica un documento del repo hacia el backend externo de una empresa. **El repo siempre es la fuente de verdad**;
el backend es un espejo para quien no lee el repo.

## Principio: degradar, no fallar

**Publicar es opcional.** Si la empresa no declaró backend, esta skill no es un error ni un bloqueo: informa en una
línea que la empresa no tiene publicación configurada, confirma que el documento ya está en el repo, y termina
normalmente. **Nunca pidas instalar nada. Nunca dejes el ciclo a medias por esto.**

## 1. Resolver la empresa y su backend

1. Resuelve la empresa (lo que diga el usuario → el path del documento → la empresa fijada en la conversación →
   `AskUserQuestion`). **Nunca elijas tú.**
2. Lee `<empresa>/context.md` y busca el campo `publicacion:`.

| Valor de `publicacion:` | Qué haces |
|---|---|
| ausente, vacío o `markdown` | Nada que publicar. Informa en una línea y termina bien. |
| el nombre de una herramienta | Sigue al paso 2. |

Si el campo nombra una herramienta pero no hay forma de alcanzarla en esta sesión (sin integración disponible,
sin credenciales), **dilo en una línea y termina bien**. El documento ya está en el repo; eso basta.

## 2. Preparar el documento

- **Qué se publica:** el contenido del `.md` tal cual, sin la cabecera de metadatos.
- **Qué NO se publica, nunca:** el bloque `## Estado` (es interno y de trabajo), el plan de tareas si el backend
  tiene su propio gestor de tareas, y cualquier cosa que `<empresa>/context.md` liste bajo *Qué NO sale de esta carpeta*.
- **Título de destino:** el primer encabezado `#` del documento, no el nombre del archivo.
- **Reusar, no duplicar:** antes de crear, busca si ya existe un destino con ese título y actualízalo. Publicar dos
  veces el mismo documento como dos páginas distintas es el error más caro de esta skill.

## 3. Guardia del Invariante #0 — antes de escribir

Revisa el documento en busca de datos personales de clientes finales: nombres con documento de identidad, números de
documento, datos biométricos, direcciones, correos y teléfonos de personas, registros individuales.

**Si encuentras algo: aborta y repórtalo.** No publiques una versión "parcheada" sin avisar. Publicar es una acción
hacia afuera y no se revierte: lo que salió puede quedar cacheado o indexado aunque después se borre.

## 4. Confirmar

Devuelve en pocas líneas: qué documento se publicó, a dónde (o por qué no), si se creó o se actualizó un destino
existente, y el enlace resultante para que quien llamó lo escriba en el bloque `## Estado` del trabajo.

## Gotchas

- **El repo gana siempre.** Si el backend y el repo divergen, el repo tiene razón. Nunca traigas contenido del
  backend de vuelta al repo sin que el usuario lo pida explícitamente.
- **Publicar no es archivar.** Que un documento esté publicado no significa que el trabajo esté cerrado; eso lo
  hace `/mos:archivar`.
- **Una empresa, un backend.** No publiques el documento de una empresa en el espacio de otra, aunque compartan
  herramienta. Es la regla de aislamiento aplicada hacia afuera.
