<!-- Creado: AAAA-MM-DD · Actualizado: AAAA-MM-DD · Creador: <nombre> -->

# Tareas — <Título del trabajo>

Tareas atómicas. **Una tarea es atómica cuando quien la recibe sabe exactamente qué entregar y cómo se
comprueba que está hecha**, sin volver a preguntar.

| # | Tarea | Depende de | Cómo se verifica | Estado |
|---|---|---|---|---|
| T1 | <…> | — | <…> | pendiente |
| T2 | <…> | T1 | <…> | pendiente |

**Estados:** `pendiente` · `en curso` · `hecha` · `bloqueada (por qué)` · `descartada (por qué)`.

## Publicación

Si `<empresa>/context.md` declara un backend en `publicacion:`, estas tareas se sincronizan ahí al correr
`/mos:aplicar`. Si no, este archivo es la única fuente y nada falla.
