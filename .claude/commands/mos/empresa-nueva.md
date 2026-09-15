---
description: Da de alta una empresa nueva en el repo — crea su carpeta desde _Templates/empresa/, declara sus áreas con el usuario y deja el esqueleto listo para trabajar
argument-hint: [nombre de la empresa]
---

Das de alta una **empresa nueva** en este repo multi-empresa. Al terminar, la empresa queda con su `context.md`
declarando sus áreas, sus carpetas de servicio y su bitácora — lista para que el ciclo `/mos:explorar → /mos:proponer →
/mos:aplicar → /mos:archivar` opere sobre ella.

Nombre de la empresa (opcional): $ARGUMENTS

## 1. Nombre y slug

Si el nombre no viene en $ARGUMENTS, pídelo en una línea. Deriva el `{slug}` en kebab-case y **confírmalo** — es el
nombre de carpeta y no se cambia después sin romper referencias.

Si `{slug}/` ya existe, detente y dilo: esa empresa ya está dada de alta.

## 2. Ficha mínima

Un solo lote de preguntas, no más de cinco, para llenar la ficha de `context.md`:

- ¿Qué hace la empresa y para quién? (una línea)
- ¿En qué etapa está? (idea / validación / operando / escalando)
- ¿Modelo de negocio y moneda de reporte?
- ¿Cuántas personas y qué roles?
- ¿Publica documentación a alguna herramienta externa, o todo se queda en Markdown?

## 3. Declarar las áreas — el paso que importa

**Las áreas de una empresa se definen aquí, y solo aquí, con el usuario.** No hay catálogo obligatorio: una
consultora no tiene las mismas áreas que una SaaS. Presenta el catálogo sugerido de `_Templates/empresa/context.md`
con `AskUserQuestion` (`multiSelect: true`, header "Áreas") y deja que el usuario marque las que apliquen. La opción
nativa de texto libre sirve para agregar las que falten.

**No agregues ni una sola área que el usuario no haya marcado.** Ni porque "toda empresa necesita Legal", ni porque
la otra empresa la tiene, ni para dejar la estructura "completa". Un área que nadie pidió es una carpeta muerta que
después nadie se atreve a borrar.

Si marca muy pocas (una o dos), no lo corrijas: una empresa con tres áreas es más útil que nueve carpetas vacías.
Siempre se pueden agregar después — preguntando de nuevo.

## 4. Crear la estructura

1. Copia `_Templates/empresa/` a `{slug}/`.
2. Crea una carpeta por área declarada, cada una con su `context.md` a partir de `_Templates/area-context.md`,
   con la responsabilidad del área ya escrita (no la dejes en blanco — redáctala con lo que sabes de la empresa).

   **Si una carpeta de área ya existe** — porque alguien la creó a mano antes de correr este comando — **no la
   toques en silencio.** Pregunta con `AskUserQuestion` qué hacer con ella: *poblar su `context.md`* (si está
   vacía o no lo tiene), *dejarla como está*, o *no incluirla en la tabla de áreas*. Una carpeta que ya existe
   suele tener contenido o intención detrás; sobrescribir su `context.md` sin preguntar borra esa intención.
3. Rellena `{slug}/context.md`: la ficha del paso 2 y la tabla de áreas del paso 3, recortada a lo declarado.
4. **Estampa los campos de control:** `Id` = `{slug}` (la carpeta, que no se renombra nunca), `estado: activa`, y
   `template_version:` = la versión que encabeza `_Templates/CHANGELOG.md`. Sin ese sello, dentro de unos meses
   nadie sabrá con qué versión de la plantilla nació esta empresa.
5. Pon la fecha de hoy en las cabeceras `<!-- Creado: … -->` de todos los archivos creados.

## 5. Registrar el hito

Añade la **primera línea** de la bitácora de la empresa recién creada, en
`{slug}/Decisiones/Q<N>-<AAAA>.log` (Q1 ene-mar, Q2 abr-jun, Q3 jul-sep, Q4 oct-dic):

```
AAAA-MM-DD — Alta de la empresa <nombre> (<slug>). Áreas: <lista>.
```

No hay bitácora en la raíz: toda decisión pertenece a una empresa, y el alta pertenece a la que nace.

## 6. Dar de baja una empresa (la contraparte)

No hay comando de baja porque **no se borra nada**. Una empresa que se pausa, se vende o se cierra cambia el campo
`estado:` de su `context.md` a `pausada` o `archivada`, y el hito se registra en **su propia** bitácora. Deja de
ofrecerse en la resolución de empresa; su árbol se conserva intacto.

Si el usuario pide dar de baja una empresa durante esta sesión, hazlo así y no muevas ni borres carpetas.

## 7. Confirmar

Devuelve en pocas líneas: la ruta creada, las áreas declaradas, y el siguiente paso sugerido —
`/mos:explorar` para pensar el primer trabajo de esta empresa.

## Invariante #0 (no negociable)

Solo **plano de control** (cómo opera la empresa: ingresos, conteos, runway, funnel — agregados y derivadas).
**Nunca plano de datos**: datos personales de clientes finales. Ante la duda, no escribas.

Idioma: español siempre. Directo, breve, cero relleno.
