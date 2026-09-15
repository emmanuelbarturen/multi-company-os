<!-- Creado: 2026-09-15 · Actualizado: 2026-09-15 · Creador: Oxalc -->

# empresa2 — Consultora de servicios (EJEMPLO)

> **Empresa de ejemplo.** Sus áreas **no son las mismas que las de `empresa1`**, y eso es el punto: el framework no
> impone un catálogo. Una consultora no tiene `Producto/` ni `Ingeniería/`; tiene `Servicios/` y `Entregas/`.
> Bórrala y crea las tuyas con `/mos:empresa-nueva`.

## Ficha

| Campo | Valor |
|---|---|
| Id (carpeta, no se cambia) | `empresa2` |
| Nombre (display) | empresa2 |
| Estado | `estado: activa` |
| Qué hace | Consultoría por proyecto para equipos que necesitan capacidad técnica temporal |
| Etapa | validación |
| Modelo de negocio | Proyecto cerrado y retainer mensual |
| Equipo | 2 socios más colaboradores por proyecto |
| Moneda | USD |
| Publicación | `publicacion: markdown` |
| Versión de plantilla | `template_version: v1` |

## Áreas de esta empresa

Cinco, con nombres propios. No tiene `Producto/`, `Ingeniería/` ni `Marketing/`: su demanda viene de referidos y su
capacidad técnica se contrata por proyecto.

| Carpeta | Qué vive aquí |
|---|---|
| `Company/` | la consultora y su estrategia: socios, objetivos, decisiones de rumbo, capacidad disponible |
| `Servicios/` | qué se ofrece: tipos de encargo, alcance típico de cada uno, cómo se cotiza |
| `Entregas/` | los encargos en curso y cerrados: alcance acordado, hitos, retrospectivas |
| `Comercial/` | prospección, propuestas, contratos, referidos |
| `Finanzas/` | facturación por proyecto, cobranza, costos de colaboradores, caja |

> Compara esta tabla con la de `empresa1`: seis áreas contra cinco, y solo dos nombres coinciden. **Así se ve
> "áreas libres" en la práctica** — y el ruteo sigue funcionando porque cada empresa declara la suya.

## Carpetas de servicio

`_GTD/Proyectos/` · `_GTD/Tareas-Sueltas/` · `_Ingesta/` · `Decisiones/`

## Reglas propias de esta empresa

- Un encargo no arranca sin alcance firmado. Lo acordado por chat no cuenta como alcance.
- Cada encargo cerrado deja una retrospectiva en `Entregas/`, aunque haya salido bien.

## Qué NO sale de esta carpeta

Nombres de clientes en cualquier documento que se comparta fuera, y todo lo que cae bajo el Invariante #0.
Los casos de éxito se escriben anonimizados salvo autorización escrita del cliente.
