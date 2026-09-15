<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# Estudio Web (EJEMPLO)

> **Empresa de ejemplo**, inventada para que se entienda cómo se trabaja en este repo. Junto con `tienda-de-cafe`
> muestra que **las áreas son libres**: estas dos no comparten ni un nombre de área. Bórrala cuando ya no te enseñe
> nada y crea las tuyas con `/mos:setup` o `/mos:empresa-nueva`.

## Ficha

| Campo | Valor |
|---|---|
| Id (carpeta, no se cambia) | `estudio-web` |
| Nombre (display) | Estudio Web |
| Estado | `estado: activa` |
| Qué hace | Diseña y construye sitios web para negocios pequeños, por encargo |
| Etapa | validación |
| Modelo de negocio | Proyecto cerrado, con presupuesto pactado antes de empezar |
| Equipo | 2 socios, más gente por encargo cuando hace falta |
| Moneda | EUR |
| Publicación | `publicacion: markdown` |
| Versión de plantilla | `template_version: v2` |

## Áreas de esta empresa

**Dos.** Un estudio de dos personas vive de dos cosas: conseguir el encargo y entregarlo bien. No hay más.

| Carpeta | Qué vive aquí |
|---|---|
| `Comercial/` | conseguir encargos: prospectos, presupuestos, cómo se cotiza, referidos |
| `Entregas/` | los encargos en curso y cerrados: qué se acordó, en qué va, qué se aprendió al terminar |

> Compara esta tabla con la de `tienda-de-cafe`: **ningún nombre coincide**, y sin embargo `Comercial/` y `Ventas/`
> hacen un trabajo parecido. Cada negocio llama a las cosas como las llama de verdad: el framework no lo corrige.

## Carpetas de servicio

`_GTD/Proyectos/` · `_GTD/Tareas-Sueltas/` · `_Referencias/` · `Decisiones/`

## Reglas propias de esta empresa

- Ningún encargo arranca sin alcance firmado. Lo acordado por chat no cuenta como alcance.
- Todo encargo cerrado deja una retrospectiva en `Entregas/`, aunque haya salido bien.

## Qué NO sale de esta carpeta

Nombres de clientes en cualquier documento que salga del estudio. Los casos de éxito se escriben anonimizados
salvo permiso escrito del cliente.
