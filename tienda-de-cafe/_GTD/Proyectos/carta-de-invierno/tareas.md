<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Tareas — Carta de invierno

Tareas atómicas. **Una tarea es atómica cuando quien la recibe sabe exactamente qué entregar y cómo se comprueba
que está hecha**, sin volver a preguntar.

| # | Tarea | Depende de | Cómo se verifica | Estado |
|---|---|---|---|---|
| T1 | Elegir las tres bebidas de la lista de candidatas | — | Las tres están escritas en `solucion.md` | hecha (2026-09-15) |
| T2 | Confirmar con el proveedor que trae el tercer ingrediente antes del 20-oct | T1 | Respuesta del proveedor por escrito | hecha (2026-09-15) |
| T3 | Probar las tres recetas en barra y cronometrarlas | T1 | Las tres bajo 3 minutos, anotado en el spike de `solucion.md` | en curso |
| T4 | Fijar el precio de cada bebida | T3 | Los tres precios escritos en `Ventas/` | pendiente |
| T5 | Diseñar e imprimir la carta de temporada | T4 | Las cartas impresas, físicas, en el local | pendiente |
| T6 | Enseñar las tres recetas al equipo | T3 | Las cuatro personas prepararon cada una al menos una vez | pendiente |

**Estados:** `pendiente` · `en curso` · `hecha` · `bloqueada (por qué)` · `descartada (por qué)`.

## Publicación

`tienda-de-cafe/context.md` declara `publicacion: markdown`, así que este archivo es la única fuente y no se
sincroniza con ninguna herramienta externa. El ciclo funciona igual.
