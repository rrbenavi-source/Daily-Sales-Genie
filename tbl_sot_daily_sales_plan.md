# Documentación: Vista Materializada `tbl_sot_daily_sales_plan`

## Información General

| Campo | Valor |
|-------|-------|
| **Nombre** | tbl_sot_daily_sales_plan |
| **Catálogo** | heiaepmx002pwe01 |
| **Esquema / Base de datos** | gold_hnk_mx_loc_sellin |
| **Tipo** | MATERIALIZED_VIEW |
| **Propietario** | HEI-AEP-MX002-01-P-DATAPROCESSING |
| **Fecha de creación** | 20 de noviembre de 2025, 11:25 AM |
| **Última actualización** | 22 de mayo de 2026, 11:34 AM |
| **Tipo de cómputo de creación** | DBSQL Warehouse Compute |
| **Pipeline ID** | 3ff5d02b-f72d-4b97-9fcc-9ea9c6bda6c5 |
| **Table ID** | dad5dccc-d1ef-4c98-9786-39f6376f9fb9 |
| **Estado del pipeline** | Completado (22 may 2026, 11:43 AM) |
| **Programación de refresco** | Sin programación |

---

## Descripción

Vista materializada del dominio **Sell-In** que consolida el plan de ventas diarias (cuota / meta de venta) para la operación de México. Contiene información dimensional de jerarquías comerciales (unidad comercial, canal estratégico, región, gerencia de zona), jerarquía de producto (material, marca, familia, empaque, envase, presentación) y métricas de plan como la ratio de hectolitros, junto con datos temporales (año-mes, mes natural, año natural, versión).

---

## Calidad

| Dimensión | Estado |
|-----------|--------|
| **Estado general** | ✅ Healthy (al 22 may 2026) |
| **Freshness** | ✅ OK |
| **Completeness** | ✅ OK |
| **Data Quality Monitoring** | Habilitado |
| **Predictive Optimization** | Habilitado |

---

## Etiquetas (Tags)

| Tag | Valor |
|-----|-------|
| business_function | COMMERCIAL |
| business_owner | manuel.dominguez1@heineken.com |
| deployment_type | Data Prime |
| devops_project | AEP OpCo Mexico 2 |
| env | p (producción) |
| hitt_version | 2.31.0 |
| project_description | Mexico 2.0 |
| project_name | mx002 |
| project_seq_no | 01 |

---

## Propiedades Delta

| Propiedad | Valor |
|-----------|-------|
| deletedFileRetentionDuration | 14 days |
| enableChangeDataFeed | true |
| enableDeletionVectors | true |
| enableRowTracking | true |
| logRetentionDuration | 60 days |

---

## Columnas (71 columnas)

### Dimensiones Comerciales / Geográficas

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 0 | `unidad_comercial` | string | Identificador de la unidad comercial |
| 1 | `unidad_comercial_desc` | string | Descripción de la unidad comercial |
| 2 | `canal_estrategico` | string | Identificador del canal estratégico |
| 3 | `canal_estrategico_desc` | string | Descripción del canal estratégico |
| 4 | `region` | string | Región comercial |
| 5 | `gerencia_de_zona` | string | Identificador de la gerencia de zona |
| 6 | `gerencia_de_zona_desc` | string | Descripción de la gerencia de zona |
| 70 | `zona_desc` | string | Descripción de la zona |

### Métricas de Plan

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 7 | `hectolitro_ratio` | double | Ratio de hectolitros del plan de venta |

### Dimensiones de Producto

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 8 | `material_id` | string | Identificador del material / producto |
| 9 | `material_desc` | string | Descripción del material |
| 10 | `material_sku` | string | SKU del material |
| 11 | `id_price_segment` | string | Identificador del segmento de precio |
| 12 | `price_segment_description` | string | Descripción del segmento de precio |
| 13 | `agrupador_producto_id` | string | Identificador del agrupador de producto |
| 14 | `grupo_producto_id` | string | Identificador del grupo de producto |
| 15 | `desc_grupo_producto` | string | Descripción del grupo de producto |
| 16 | `categoria_producto_id` | string | Identificador de la categoría de producto |
| 17 | `desc_categoria_producto` | string | Descripción de la categoría de producto |
| 18 | `tipo_producto_id` | string | Identificador del tipo de producto |
| 19 | `desc_tipo_producto` | string | Descripción del tipo de producto |
| 20 | `categoria_id` | string | Identificador de categoría |
| 21 | `desc_categoria` | string | Descripción de categoría |
| 22 | `agrupacion_categoria_id` | string | Identificador de agrupación de categoría |
| 23 | `desc_agrupacion_categoria` | string | Descripción de agrupación de categoría |
| 24 | `subcategoria_id` | string | Identificador de subcategoría |
| 25 | `desc_subcategoria` | string | Descripción de subcategoría |
| 26 | `marca_producto_id` | string | Identificador de marca del producto |
| 27 | `desc_marca_producto` | string | Descripción de marca del producto |
| 28 | `agrupador_marca_id` | string | Identificador del agrupador de marca |
| 29 | `desc_agrupador_marca` | string | Descripción del agrupador de marca |
| 30 | `marca_id` | string | Identificador de marca |
| 31 | `desc_marca` | string | Descripción de marca |
| 32 | `familia_marca_id` | string | Identificador de familia de marca |
| 33 | `desc_familia_marca` | string | Descripción de familia de marca |
| 34 | `extension_linea_id` | string | Identificador de extensión de línea |
| 35 | `desc_extension_linea` | string | Descripción de extensión de línea |
| 36 | `operacion_id` | string | Identificador de operación del producto |
| 37 | `desc_operacion` | string | Descripción de operación del producto |
| 38 | `multipack_id` | string | Identificador de multipack |
| 39 | `desc_multipack` | string | Descripción de multipack |
| 40 | `tamano_paquete_id` | string | Identificador de tamaño de paquete |
| 41 | `desc_tamano_paquete` | string | Descripción de tamaño de paquete |
| 42 | `tamano_paquete_primario_id` | string | Identificador de tamaño de paquete primario |
| 43 | `desc_tamano_paquete_primario` | string | Descripción de tamaño de paquete primario |
| 44 | `tipo_paquete_id` | string | Identificador de tipo de paquete |
| 45 | `color_envase_id` | string | Identificador de color de envase |
| 46 | `desc_color_envase` | string | Descripción de color de envase |
| 47 | `presentacion_ccm_id` | string | Identificador de presentación CCM |
| 48 | `desc_presentacion_ccm` | string | Descripción de presentación CCM |
| 49 | `presentacion_id` | string | Identificador de presentación |
| 50 | `desc_presentacion` | string | Descripción de presentación |
| 51 | `retornabilidad_id` | string | Identificador de retornabilidad |
| 52 | `desc_retornabilidad` | string | Descripción de retornabilidad |
| 53 | `retornable_id` | string | Identificador de retornable |
| 54 | `desc_retornable` | string | Descripción de retornable |
| 55 | `forma_id` | string | Identificador de forma del envase |
| 56 | `desc_forma` | string | Descripción de forma del envase |
| 57 | `udm_base` | string | Unidad de medida base |
| 58 | `tipo_producto_venta_id` | string | Identificador del tipo de producto de venta |
| 59 | `tipo_producto_venta_desc` | string | Descripción del tipo de producto de venta |
| 60 | `hmex_pack_group_id` | string | Identificador del grupo de empaque HMEX |
| 61 | `hmex_pack_group_desc` | string | Descripción del grupo de empaque HMEX |
| 62 | `hmex_pack_group_contador` | decimal(17,0) | Contador del grupo de empaque HMEX |
| 63 | `hmex_pack_group` | string | Grupo de empaque HMEX |
| 64 | `npi` | char(1) | Indicador NPI (New Product Introduction) |
| 65 | `tipo_sku` | string | Tipo de SKU |

### Dimensiones Temporales

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 66 | `anio_mes` | string | Combinación año-mes |
| 67 | `mes_natural` | string | Mes en lenguaje natural |
| 68 | `anio_natural` | string | Año en lenguaje natural |
| 69 | `version` | string | Versión del plan |

---

## Usuarios Principales (Top Users)

- Ricardo Benavides
- Benito Antonio Rodríguez

---

## Activos Relacionados

- **New Query 2026-05-19 17:49:46** (Consulta)

---

## Notas Técnicas

- La definición SQL de la vista no está disponible directamente en el catálogo (`Definition not supported for this table`).
- La vista forma parte del mismo pipeline que otras vistas del dominio Sell-In: `3ff5d02b-f72d-4b97-9fcc-9ea9c6bda6c5`.
- El catálogo base de referencia es `heiaepmx002pwe01` con namespace `default`.
- Contiene un total de **71 columnas**.
- A diferencia del dashboard de ventas diarias, esta tabla **no incluye columnas de clientes ni de transacciones reales**: se enfoca exclusivamente en el plan/cuota.
- La columna `hectolitro_ratio` es la única columna numérica (tipo `double`); `hmex_pack_group_contador` es `decimal(17,0)`; `npi` es `char(1)`; el resto son `string`.
- Compresión utilizada: **Snappy** (Parquet y ORC).
- Zona horaria de sesión: **Etc/UTC**.
- Formato de datos por defecto: **Delta**.

---

*Documentación generada el 22 de mayo de 2026 a partir del Databricks Unity Catalog.*
