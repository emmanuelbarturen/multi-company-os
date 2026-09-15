<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Bitácora global

Bitácora de las decisiones que **no pertenecen a ninguna empresa**. Un evento por línea, con fecha, en el archivo
del quarter actual: `Q<N>-<AAAA>.log` (Q1 ene-mar, Q2 abr-jun, Q3 jul-sep, Q4 oct-dic).

## Qué es "global" y qué no

La prueba es una sola pregunta: **si mañana cierras una empresa, ¿esta decisión sigue teniendo sentido?**
Si sí, es global. Si se cae con ella, era de esa empresa.

| Nivel | Dónde se registra | Ejemplos |
|---|---|---|
| **De una empresa** | `<empresa>/Decisiones/` | subir un precio, cambiar un proceso, cerrar un proyecto |
| **De varias, pero no todas** | La misma línea marcada `[cross]` en la bitácora de **cada empresa afectada** | mover un proyecto de una empresa a otra, compartir un proveedor entre dos |
| **Global** | **aquí** | dar de alta o de baja una empresa, decidir dónde poner el foco del portafolio, cambiar una regla del framework |

Una decisión que afecta a dos de tus cinco empresas **no es global**: pertenece a esas dos, y ellas son quienes
necesitan verla al leer su propia bitácora. Global es lo que sigue siendo verdad aunque cambie la lista de empresas.

## Formato

```
2026-09-15 — Alta de la empresa <nombre> (<slug>). Áreas: <lista>.
2026-09-15 — Foco del trimestre en <empresa>: las demás quedan en mantenimiento.
```

## Qué NO vive aquí

`_global/` **no es una empresa**: no tiene `context.md`, no tiene áreas, no tiene `_GTD/`, y no aparece nunca como
opción al resolver en qué empresa se trabaja. Su bitácora se llama `bitacora/`, no `Decisiones/`, precisamente para
que no se confunda con la de una empresa. Es un ámbito, al lado de las empresas, no por encima de ellas.

El trabajo nunca vive aquí. Un trabajo que toca varias empresas tiene una empresa dueña y su carpeta vive en
`<empresa-dueña>/_GTD/` — aquí solo queda el registro de la decisión, si la hubo.
