<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Tienda de Café (EJEMPLO)

> **Empresa de ejemplo**, inventada para que se entienda cómo se trabaja en este repo. Junto con `estudio-web`
> muestra que **las áreas son libres**: estas dos no comparten ni un nombre de área. Bórrala cuando ya no te enseñe
> nada y crea las tuyas con `/mos:setup` o `/mos:empresa-nueva`.

## Ficha

| Campo | Valor |
|---|---|
| Id (carpeta, no se cambia) | `tienda-de-cafe` |
| Nombre (display) | Tienda de Café |
| Estado | `estado: activa` |
| Qué hace | Vende café de especialidad en un local de barrio, y grano molido para llevar |
| Etapa | operando |
| Modelo de negocio | Venta directa en local |
| Equipo | 4 personas: dos en barra, una en caja, la dueña |
| Moneda | EUR |
| Publicación | `publicacion: markdown` |
| Versión de plantilla | `template_version: v2` |

## Áreas de esta empresa

**Dos.** Un negocio de cuatro personas no necesita nueve carpetas: necesita saber qué se vende y que el local
funcione. Todo lo demás cabe dentro de esas dos.

| Carpeta | Qué vive aquí |
|---|---|
| `Ventas/` | qué se vende y a qué precio: carta, precios, lo que más sale, promociones |
| `Operaciones/` | que el local funcione: proveedores, horarios, turnos, stock, mantenimiento |

> Compara esta tabla con la de `estudio-web`: **ningún nombre coincide**. Así se ve "áreas libres" de verdad.
> Si mañana hace falta un área nueva, se crea **preguntando** — nunca sola.

## Carpetas de servicio

`_GTD/Proyectos/` · `_GTD/Tareas-Sueltas/` · `_Referencias/` · `Decisiones/`

## Reglas propias de esta empresa

- Un cambio de precio en la carta se anota en `Decisiones/` el día que se decide, no el día que se imprime.
- Antes de cambiar de proveedor se prueba el producto una semana en el local.

## Qué NO sale de esta carpeta

Nada de clientes individuales: ni nombres, ni teléfonos, ni qué compró cada quien. Aquí solo van totales —
cuántos cafés al día, qué porcentaje es para llevar. Es el Invariante #0 aplicado a un negocio de barrio.
