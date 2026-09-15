---
name: wireframes
description: Diseña wireframes y mockups de pantallas en baja fidelidad para acordar estructura y flujo antes de escribir código o diseño visual. Empieza en ASCII dentro del documento y sube de fidelidad solo si hace falta. USE WHEN wireframe, mockup, prototipo de pantalla, cómo se ve la interfaz, diseña la pantalla, boceto de UI, layout de la vista. NOT FOR diagramas de flujo o arquitectura (usa `diagrama-flujo`), NOT FOR diseño visual final ni sistema de marca, NOT FOR incrustar datos personales de clientes finales en el mockup.
---

# wireframes

Un wireframe existe para **acordar estructura y flujo antes de gastar en lo caro**: el código y el diseño visual.
Si ya hay acuerdo sobre la estructura, no hagas wireframe: pasa a construir.

## Baja fidelidad primero — siempre

**Empieza en ASCII, dentro del documento.** No es una limitación: es la forma correcta de empezar. Un wireframe feo
recibe críticas sobre la estructura; uno bonito recibe críticas sobre los colores, que es exactamente lo que no
quieres discutir todavía.

```
┌─────────────────────────────────────────┐
│  Logo            Buscar…      [Perfil]  │
├──────────┬──────────────────────────────┤
│ Filtros  │  Título de la sección        │
│ ☐ Opción │  ┌────────┐ ┌────────┐       │
│ ☐ Opción │  │ Tarjeta│ │ Tarjeta│       │
│ ☐ Opción │  └────────┘ └────────┘       │
│          │         [ Ver más ]          │
└──────────┴──────────────────────────────┘
```

Sube de fidelidad **solo** cuando la estructura ya está acordada y alguien necesita ver el resultado real.

## Qué define un wireframe (y qué no)

**Sí define:** qué información aparece en la pantalla, su jerarquía, qué acciones puede tomar la persona, qué pasa
después de cada acción, y qué se ve cuando no hay datos, cuando está cargando y cuando algo falla.

**No define:** colores, tipografías, espaciados exactos, iconos ni copy final. Si la conversación se va ahí,
redirígela: todavía no toca.

## Los tres estados que siempre se olvidan

Por cada pantalla, dibuja o describe: **vacío** (aún no hay datos), **cargando**, y **error**. Son la mitad de los
bugs de interfaz y el noventa por ciento de lo que no se acordó a tiempo.

## Flujo, no pantallas sueltas

Una pantalla aislada no se puede evaluar. Muestra la secuencia: de dónde llega la persona, qué hace, a dónde va.
Si el flujo tiene ramas, usa la skill `diagrama-flujo` para el flujo y los wireframes para cada pantalla.

## Dónde vive

Embebido en `propuesta.md` o `solucion.md` del trabajo, dentro de un bloque de código. Como cualquier otro
artefacto del ciclo, se actualiza cuando el documento se actualiza.

## Guardia del Invariante #0

Los datos de ejemplo en un wireframe son **inventados**: "Ana Pérez", "Pedido #1042". Nunca copies datos reales de
clientes finales en un mockup, por realista que lo haga.
