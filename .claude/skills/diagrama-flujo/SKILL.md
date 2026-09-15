---
name: diagrama-flujo
description: Crea diagramas de flujo, de proceso, de secuencia, de estados y de arquitectura en Mermaid, embebidos en el documento que los necesita. Sin dependencias externas — Mermaid se renderiza nativo. USE WHEN diagrama de flujo, flowchart, diagrama de proceso, diagrama de arquitectura, dibuja el flujo, visualiza el proceso, mapea el proceso, diagrama de secuencia, diagrama de estados, mermaid. NOT FOR wireframes o diseño de interfaz (usa `wireframes`), NOT FOR ilustraciones, NOT FOR incrustar datos personales de clientes finales en el diagrama.
---

# diagrama-flujo

Dibuja un sistema o proceso que **ya se entiende**. Si todavía no está claro cómo funciona, eso no es un diagrama:
es una exploración (`/mos:explorar`) o un levantamiento de requerimientos (`project-requirements`).

## Elegir el tipo antes de dibujar

| Lo que quieres mostrar | Tipo de Mermaid |
|---|---|
| Pasos y decisiones de un proceso | `flowchart TD` (o `LR` si es largo y plano) |
| Quién habla con quién y en qué orden | `sequenceDiagram` |
| En qué estados puede estar algo y cómo transita | `stateDiagram-v2` |
| Quién hace qué en un proceso con varios responsables | `flowchart` con `subgraph` por responsable |
| Componentes de un sistema y sus dependencias | `flowchart LR` con `subgraph` por capa |

**Si dudas entre dos, elige el flowchart.** Se entiende sin explicación previa, que es el punto.

## Reglas de dibujo

1. **Un diagrama responde una pregunta.** Escríbela antes de dibujar. Si el diagrama responde tres, son tres diagramas.
2. **Máximo ~20 nodos.** Pasado eso nadie lo lee: parte en dos, o sube un nivel de abstracción.
3. **Las decisiones son preguntas de sí/no**, y sus dos salidas van etiquetadas. Una decisión con una sola salida no
   es una decisión.
4. **Nombra los nodos con verbos**, no con sustantivos: "Validar pedido", no "Validación".
5. **Todo camino termina.** Un nodo sin salida que no sea un final explícito es un error del diagrama, no del proceso.
6. **Español en las etiquetas.**

## Dónde va el diagrama

**Por defecto, embebido** en el documento que lo necesita, como bloque ```mermaid. Un diagrama que vive suelto se
desactualiza; uno que vive dentro del documento se actualiza cuando el documento se actualiza.

Los diagramas de un trabajo van dentro de su `solucion.md` o `propuesta.md`. Los diagramas de un proceso permanente
van dentro del `context.md` de su área o del documento del proceso.

## Iterar

Muestra el diagrama y pregunta **una sola cosa**: qué falta o qué sobra. Ajusta y vuelve a mostrar. Tres rondas
suelen bastar; si pasas de cinco, el problema no es el diagrama: es que el proceso no está claro todavía. Dilo.

## Guardia del Invariante #0

Nunca incrustes datos personales de clientes finales en las etiquetas de un diagrama: ni nombres, ni documentos, ni
correos. Los ejemplos van abstraídos ("Cliente A", "Pedido #1"). Un diagrama se comparte más que un documento.
