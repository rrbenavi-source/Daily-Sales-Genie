# Documentación: Metric View `tbl_sot_daily_sales_plan_metric_view`

## Información General

| Campo | Valor |
|-------|-------|
| **Nombre** | tbl_sot_daily_sales_plan_metric_view |
| **Catálogo** | heiaepmx002pwe01 |
| **Esquema / Base de datos** | gold_hnk_mx_loc_sellin |
| **Tipo** | METRIC VIEW |
| **Versión de definición** | 1.1 |
| **Tabla fuente (Source)** | tbl_sot_daily_sales_plan |

---

## Descripción

Metric View del dominio **Sell-In** que expone el plan de ventas mensual en hectolitros. Se construye sobre la vista materializada `tbl_sot_daily_sales_plan` y aplica un filtro de categorías de producto cervecero equivalente al aplicado en la metric view de ventas reales (`tbl_sot_sellin_daily_sales_daily_dashboard_metric_view`).

Los **nombres de dimensiones son intencionalmente idénticos** a los de la metric view de ventas reales para que el espacio Genie pueda hacer join automático entre plan y real al momento de responder preguntas de negocio (ej. "¿Cuál es el avance vs plan por marca y mes?").

---

## Consideraciones de Diseño

| Tema | Detalle |
|------|---------|
| **Granularidad del plan** | Mensual (no diaria). El plan no tiene columnas `dia`, `semana` ni `fecha`. Se agrega la dimensión `Año-Mes` como clave de join a nivel mensual. |
| **Filtro simplificado** | La tabla fuente no contiene `oficina_ventas_id` ni `grupo_cuentas_id`, por lo que solo aplica el filtro de `categoria_producto_id`. |
| **Canal Estrategico** | No se aplica la lógica DISCOUNTERS (`cliente_cadena`) porque el plan no tiene nivel de cliente; se usa `canal_estrategico_desc` directamente. |
| **Join con ventas reales** | Las dimensiones compartidas para join son: `Marca`, `Line Extension ID`, `HMEX Pack Group`, `ID Presentacion CCM`, `Packtype`, `Multipack`, `Presentacion`, `Presentacion CCM`, `Retornable`, `Subcategoria`, `ID SKU`, `SKU`, `Canal Estrategico`, `DR`, `Gerencia Zona`, `Zona`, `Año`, `Mes`, `Año-Mes`. |
| **`Region`** | En el plan el campo se llama `region`; en el real es `direccion_regional_desc`. El contenido es equivalente. |
| **`version`** | Dimensión adicional del plan que no existe en ventas reales. Permite filtrar en Genie por versión de plan (ej. versión original vs revisada). |

---

## Etiquetas (Tags)

| Tag | Valor |
|-----|-------|
| business_owner | manuel.dominguez1@heineken.com |
| deployment_type | Data Prime |
| devops_project | AEP OpCo Mexico 2 |
| env | p (producción) |
| hitt_version | 2.31.0 |
| project_description | Mexico 2.0 |
| project_name | mx002 |
| project_seq_no | 01 |

---

## Filtro Global (Filter)

```sql
categoria_producto_id IN ('002','007','008','009')
```

**Criterio del filtro:**
- Se incluyen únicamente categorías de producto: **002**, **007**, **008** y **009** (categorías de cerveza), alineadas con el filtro de la metric view de ventas reales.
- No se aplica filtro de `oficina_ventas_id` ni de `grupo_cuentas_id` porque estas columnas no existen en `tbl_sot_daily_sales_plan`.

---

## Medidas (Measures) — 1

| Nombre | Expresión | Descripción |
|--------|-----------|-------------|
| **HL Plan** | `SUM(hectolitro_ratio)` | Total de hectolitros del plan de venta (cuota / meta mensual) |

---

## Dimensiones (Dimensions) — 23

### Dimensiones de Producto

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Marca** | `desc_marca` | Marca del producto en el plan de venta |
| **Marca agrupadora** | `desc_marca_producto` | Marca agrupadora a la que está relacionado el producto del plan |
| **Line Extension Desc** | `desc_extension_linea` | Descripción de la extensión de línea del producto en el plan |
| **Line Extension ID** | `extension_linea_id` | Identificador de la extensión de línea del producto en el plan |
| **HMEX Pack Group Desc** | `hmex_pack_group_desc` | Descripción del grupo de empaque HMEX en el plan |
| **HMEX Pack Group** | `hmex_pack_group` | Grupo de empaque HMEX en el plan |
| **ID Presentacion CCM** | `presentacion_ccm_id` | Identificador de presentación CCM del producto en el plan |
| **Packtype** | `tipo_paquete_id` | Identificador del tipo de paquete del producto en el plan |
| **Multipack** | `desc_multipack` | Cantidad de latas en el paquete según el plan (ej. six pack, 12 pack) |
| **Presentacion** | `desc_presentacion` | Forma en la que se presenta el producto en el plan (botella, lata, etc.) |
| **Presentacion CCM** | `desc_presentacion_ccm` | Descripción del tamaño del producto en el plan |
| **Retornable** | `desc_retornable` | Tipo de retorno del producto en el plan |
| **Subcategoria** | `desc_subcategoria` | Subcategoría del producto en el plan |
| **ID SKU** | `material_id` | Identificador del material en el plan de venta |
| **SKU** | `material_desc` | Descripción del material en el plan de venta |
| **SKU_NPI** | `npi` | Indicador de producto nuevo (New Product Introduction) en el plan |

### Dimensiones de Canal y Comerciales

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Canal Estrategico** | `canal_estrategico_desc` | Canal estratégico al que pertenece el plan de venta |
| **DR** | `unidad_comercial_desc` | Dirección Regional (unidad comercial) del plan de venta |

### Dimensiones Geográficas

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Region** | `region` | Región comercial del plan de venta |
| **Gerencia Zona** | `gerencia_de_zona_desc` | Gerencia de zona (estado) del plan de venta |
| **Zona** | `zona_desc` | Zona del plan de venta |

### Dimensiones Temporales

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Año** | `anio_natural` | Año del plan de venta |
| **Mes** | `mes_natural` | Mes del plan de venta |
| **Año-Mes** | `anio_mes` | Período año-mes del plan (granularidad mensual; clave de join con ventas reales) |
| **Version Plan** | `version` | Versión del plan de venta (permite filtrar entre plan original y revisiones) |

---

## Definición YAML Completa

```yaml
version: 1.1

source: heiaepmx002pwe01.gold_hnk_mx_loc_sellin.tbl_sot_daily_sales_plan

filter: |-
  categoria_producto_id IN ('002','007','008','009')

dimensions:
  - name: Marca
    expr: desc_marca
    comment: Hace referencia a la marca del producto en el plan de venta
  - name: Marca agrupadora
    expr: desc_marca_producto
    comment: Representa la marca agrupadora a la que esta relacionado el producto del plan
  - name: Line Extension Desc
    expr: desc_extension_linea
    comment: Descripcion de la extension de linea del producto en el plan
  - name: Line Extension ID
    expr: extension_linea_id
    comment: Identificador de la extension de linea del producto en el plan
  - name: HMEX Pack Group Desc
    expr: hmex_pack_group_desc
    comment: Descripcion del grupo de empaque HMEX en el plan
  - name: HMEX Pack Group
    expr: hmex_pack_group
    comment: Grupo de empaque HMEX en el plan
  - name: ID Presentacion CCM
    expr: presentacion_ccm_id
    comment: Identificador de presentacion CCM del producto en el plan
  - name: Packtype
    expr: tipo_paquete_id
    comment: Identificador del tipo de paquete del producto en el plan
  - name: Multipack
    expr: desc_multipack
    comment: Cantidad de latas en el paquete segun el plan (ej. six pack o 12 pack)
  - name: Presentacion
    expr: desc_presentacion
    comment: Forma en la que se presenta el producto en el plan (botella, lata, etc.)
  - name: Presentacion CCM
    expr: desc_presentacion_ccm
    comment: Descripcion del tamano del producto en el plan
  - name: Retornable
    expr: desc_retornable
    comment: Tipo de retorno del producto en el plan
  - name: Subcategoria
    expr: desc_subcategoria
    comment: Subcategoria del producto en el plan de venta
  - name: ID SKU
    expr: material_id
    comment: Identificador del material en el plan de venta
  - name: SKU
    expr: material_desc
    comment: Descripcion del material en el plan de venta
  - name: SKU_NPI
    expr: npi
    comment: Indicador de producto nuevo (New Product Introduction) en el plan
  - name: Canal Estrategico
    expr: canal_estrategico_desc
    comment: Canal estrategico al que pertenece el plan de venta
  - name: DR
    expr: unidad_comercial_desc
    comment: Direccion Regional (unidad comercial) del plan de venta
  - name: Region
    expr: region
    comment: Region comercial del plan de venta
  - name: Gerencia Zona
    expr: gerencia_de_zona_desc
    comment: Gerencia de zona (estado) del plan de venta
  - name: Zona
    expr: zona_desc
    comment: Zona del plan de venta
  - name: Año
    expr: anio_natural
    comment: Anio del plan de venta
  - name: Mes
    expr: mes_natural
    comment: Mes del plan de venta
  - name: Año-Mes
    expr: anio_mes
    comment: Periodo anio-mes del plan (granularidad mensual; clave de join con ventas reales en Genie)
  - name: Version Plan
    expr: version
    comment: Version del plan de venta (permite filtrar entre plan original y revisiones)

measures:
  - name: HL Plan
    expr: SUM(hectolitro_ratio)
    comment: Total de hectolitros del plan de venta (cuota/meta mensual)
```

---

## Mapa de Join con la Metric View de Ventas Reales

Para que Genie pueda combinar plan vs real, ambas metric views deben estar registradas en el mismo espacio Genie. Las siguientes dimensiones son **comunes por nombre exacto** y habilitan el join automático:

| Dimensión (nombre en Genie) | Campo en Real | Campo en Plan | Nivel de join |
|-----------------------------|---------------|---------------|---------------|
| **Marca** | `desc_marca` | `desc_marca` | SKU |
| **Marca agrupadora** | `desc_marca_producto` | `desc_marca_producto` | SKU |
| **Line Extension ID** | `extension_linea_id` | `extension_linea_id` | SKU |
| **HMEX Pack Group** | `hmex_pack_group` | `hmex_pack_group` | Empaque |
| **ID Presentacion CCM** | `presentacion_ccm_id` | `presentacion_ccm_id` | Empaque |
| **Packtype** | `tipo_paquete_id` | `tipo_paquete_id` | Empaque |
| **Multipack** | `desc_multipack` | `desc_multipack` | Empaque |
| **Presentacion** | `desc_presentacion` | `desc_presentacion` | Empaque |
| **Presentacion CCM** | `desc_presentacion_ccm` | `desc_presentacion_ccm` | Empaque |
| **Retornable** | `desc_retornable` | `desc_retornable` | Empaque |
| **Subcategoria** | `desc_subcategoria` | `desc_subcategoria` | Categoría |
| **ID SKU** | `material_id` | `material_id` | SKU |
| **Canal Estrategico** | `CASE WHEN ... ELSE canal_estrategico_desc END` | `canal_estrategico_desc` | Canal ⚠️ |
| **DR** | `unidad_comercial_desc` | `unidad_comercial_desc` | Geografía |
| **Gerencia Zona** | `gerencia_zona_desc` | `gerencia_de_zona_desc` | Geografía |
| **Zona** | `zona_desc` | `zona_desc` | Geografía |
| **Año** | `anio` | `anio_natural` | Tiempo |
| **Mes** | `mes` | `mes_natural` | Tiempo ✅ |
| **Año-Mes** | `anio_mes` *(agregar a real)* | `anio_mes` | Tiempo ⚠️ |

> ✅ **Mes**: Confirmado que `mes_natural` en el plan usa formato `'01','02'...` — idéntico al campo `mes` de ventas reales. El join sobre `Mes` funciona sin transformación.
>
> ✅ **Año-Mes**: Confirmado que `anio_mes` usa formato `YYYYMM` en ambas tablas (columna #4 en ventas reales, columna #66 en plan). El join es directo con `expr: anio_mes` en ambas metric views.
>
> ⚠️ **Año-Mes (acción pendiente)**: Agregar la dimensión `Año-Mes` a la metric view de ventas reales con `expr: anio_mes`. La columna ya existe en la tabla fuente — solo falta exponerla en el YAML.
>
> ⚠️ **Canal Estrategico**: En ventas reales, la lógica DISCOUNTERS reclasifica dos cadenas específicas. En el plan no existe `cliente_cadena`, por lo que los valores de canal en el plan no reflejarán esa reclasificación.
>
> ℹ️ **Granularidad diaria vs mensual**: El real tiene datos por día; el plan es mensual. Genie agrega automáticamente el real a nivel de mes cuando compara plan vs real. Las dimensiones `Dia`, `fecha`, `Semana` y `dia_semana_abrev` del real no tienen equivalente en el plan y solo aplican a consultas de ventas reales.

---

## Activos Relacionados

- **tbl_sot_sellin_daily_sales_daily_dashboard_metric_view** (Metric View de ventas reales — par para join en Genie)
- **tbl_sot_daily_sales_plan** (Vista materializada fuente)
- **Daily Sales Assistant** (Genie Space donde se registran ambas metric views)

---

## Notas Técnicas

- Esta es una **Metric View** de Databricks versión 1.1, diseñada para ser consumida por **Genie AI** junto con la metric view de ventas reales.
- Tiene **1 medida** (`HL Plan`) y **25 dimensiones**.
- El plan tiene granularidad **mensual** (el real es diario). Genie agrega el real a nivel de mes automáticamente al comparar plan vs real. Las dimensiones `Dia`, `fecha`, `Semana` y `dia_semana_abrev` solo aplican a la metric view de ventas reales.
- `mes_natural` en el plan usa formato `'01','02'...` — mismo formato que `mes` en el real. El join sobre `Mes` funciona directo.
- `anio_mes` usa formato `YYYYMM` en ambas tablas fuente. Para activar el join por `Año-Mes` en Genie, agregar `expr: anio_mes` a la metric view de ventas reales (la columna ya existe en esa tabla).
- La dimensión **`Version Plan`** es exclusiva del plan y permite distinguir entre versión de cuota original y revisiones posteriores.
- Fuente directa: `heiaepmx002pwe01.gold_hnk_mx_loc_sellin.tbl_sot_daily_sales_plan`

---

*Documentación generada el 22 de mayo de 2026.*
