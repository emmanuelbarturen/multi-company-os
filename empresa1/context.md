<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# empresa1 — SaaS B2B (EJEMPLO)

> **Empresa de ejemplo.** Existe para mostrar cómo se ve una empresa dada de alta y, junto con `empresa2`, para
> demostrar que **las áreas son libres**: estas dos tienen áreas distintas a propósito. Bórrala y crea las tuyas
> con `/mos:empresa-nueva`.

## Ficha

| Campo | Valor |
|---|---|
| Id (carpeta, no se cambia) | `empresa1` |
| Nombre (display) | empresa1 |
| Estado | `estado: activa` |
| Qué hace | Software de suscripción para equipos de operaciones de empresas medianas |
| Etapa | operando |
| Modelo de negocio | Suscripción mensual por asiento |
| Equipo | 6 personas: producto, 3 de ingeniería, ventas, soporte |
| Moneda | USD |
| Publicación | `publicacion: markdown` |
| Versión de plantilla | `template_version: v1` |

## Áreas de esta empresa

Seis. No tiene `Legal/` propia (usa asesoría externa) ni `Operaciones/` separada (vive dentro de `Ingeniería/`).

| Carpeta | Qué vive aquí |
|---|---|
| `Company/` | la empresa y su estrategia: contexto, equipo, objetivos del año, decisiones de rumbo, indicadores |
| `Producto/` | qué se vende y a quién: catálogo de funcionalidades, hoja de ruta, investigación de usuarios |
| `Ingeniería/` | arquitectura, infraestructura, deuda técnica transversal y operación del servicio |
| `Ventas/` | pipeline, propuestas, renovaciones, contratos |
| `Marketing/` | demanda y posicionamiento: mercado, competidores, contenido, canales |
| `Finanzas/` | ingresos recurrentes, costos, márgenes, caja |

## Carpetas de servicio

`_GTD/Proyectos/` · `_GTD/Tareas-Sueltas/` · `_Ingesta/` · `Decisiones/`

## Reglas propias de esta empresa

- Las decisiones de producto se registran con la fecha en que se tomaron, no en que se implementaron.
- Toda propuesta de precio pasa por `head-cfo` antes de llegar a un cliente.

## Qué NO sale de esta carpeta

Todo lo que cae bajo el Invariante #0: datos personales de los usuarios finales del producto. Aquí solo van
agregados — conteos de cuentas, uso por plan, ingresos. Nunca un registro individual.
