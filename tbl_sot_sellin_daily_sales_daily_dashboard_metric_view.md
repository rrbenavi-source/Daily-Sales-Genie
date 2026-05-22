# Documentación: Metric View `tbl_sot_sellin_daily_sales_daily_dashboard_metric_view`

## Información General

| Campo | Valor |
|-------|-------|
| **Nombre** | tbl_sot_sellin_daily_sales_daily_dashboard_metric_view |
| **Catálogo** | heiaepmx002pwe01 |
| **Esquema / Base de datos** | gold_hnk_mx_loc_sellin |
| **Tipo** | METRIC VIEW |
| **Versión de definición** | 1.1 |
| **Propietario** | Jorge Emilio Ibarra |
| **Tabla fuente (Source)** | tbl_sot_sellin_daily_sales_daily_dashboard |

---

## Descripción

Metric View del dominio **Sell-In** que expone métricas de ventas diarias en hectolitros para el dashboard diario. Se construye sobre la vista materializada `tbl_sot_sellin_daily_sales_daily_dashboard` y aplica filtros de exclusión para remover oficinas de ventas específicas (prefijos CH, CK, MH), restringir el análisis a ciertos grupos de cuentas y categorías de producto cervecero. Permite a los usuarios de Genie AI y dashboards consultar ventas del año actual, del año anterior y del año anterior al día de hoy, desagregando por dimensiones de producto, cliente, canal y tiempo.

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

El filtro excluye oficinas de ventas no relevantes y restringe el universo de datos a:

```sql
oficina_ventas_id NOT IN (
  'CH00','CH02','CH04','CH05','CH07','CH14',
  'CK00','CK01','CK02','CK03','CK04','CK05',
  'CK06','CK07','CK08','CK09','CK10','CK11',
  'CK12','CK13','CK14','CK15','CK16','CK17',
  'CK18','CK19','CK20','CK21','CK22','CK23',
  'CK24','CK25','CK26','CK27','CK28',
  'CK29','CK30','CK31','CK32','CK33','CK34',
  'CK35','CK36','CK37','CK38','CK39','CK40',
  'CK41','CK42','CK43','CK44','CK45','CK46',
  'MH00','MH02','MH04','MH05','MH07','MH14'
)
AND grupo_cuentas_id IN ('0200', '0151', '0150')
AND categoria_producto_id IN ('002','007','008','009')
```

**Criterios del filtro:**
- Se excluyen las oficinas de ventas con prefijos **CH** (mercados especiales), **CK** (mercados CK) y **MH** (mercados MH).
- Se incluyen únicamente grupos de cuentas: **0200**, **0151** y **0150**.
- Se incluyen únicamente categorías de producto: **002**, **007**, **008** y **009** (categorías de cerveza).

---

## Medidas (Measures) — 3

| Nombre | Expresión | Descripción |
|--------|-----------|-------------|
| **HL Actual** | `SUM(dsr_ratio_anio_actual)` | Total de ventas en hectolitros del año actual |
| **HL Anterior** | `SUM(dsr_ratio_anio_anterior)` | Total de ventas en hectolitros del año anterior |
| **HL Anterior mes cerrado** | `SUM(dsr_ratio_anio_anterior_hoy)` | Total de ventas del día de consulta pero del año completo anterior (mes cerrado) |

---

## Dimensiones (Dimensions) — 33

### Dimensiones de Producto

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Marca** | `desc_marca` | Marca del producto que se vendió |
| **Marca agrupadora** | `desc_marca_producto` | Marca agrupadora a la que está relacionado el producto |
| **Line Extension Desc** | `desc_extension_linea` | Descripción de la extensión de línea que usa el producto |
| **Line Extension ID** | `extension_linea_id` | ID de la línea de extensión que usa el producto para la venta |
| **HMEX Pack Group Desc** | `hmex_pack_group_desc` | Descripción del grupo de packs que pertenece a Heineken |
| **HMEX Pack Group** | `hmex_pack_group` | Descripción del producto que se compró (grupo empaque HMEX) |
| **ID Presentacion CCM** | `presentacion_ccm_id` | Número que representa la cantidad (presentación CCM) |
| **Packtype** | `tipo_paquete_id` | Número de onzas que tiene el paquete |
| **Multipack** | `desc_multipack` | Cantidad de latas en el paquete (ej. six pack o 12 pack) |
| **Presentacion** | `desc_presentacion` | Forma en la que se presenta el producto (botella, lata, etc.) |
| **Presentacion CCM** | `desc_presentacion_ccm` | Descripción del tamaño del producto que se compró |
| **Retornable** | `desc_retornable` | Tipo de retorno que tiene el producto vendido |
| **Subcategoria** | `desc_subcategoria` | Subcategoría a la que pertenece el producto |
| **ID SKU** | `material_id` | Identificador del material que se vendió |
| **SKU** | `desc_material` | Descripción del material que se vendió |
| **SKU_NPI** | `NPI` | Identificador de producto nuevo (New Product Introduction). Habilita análisis de adopción, escala, cobertura y desempeño temprano post-lanzamiento. |

### Dimensiones de Canal y Cliente

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Canal Estrategico** | `CASE WHEN cliente_cadena IN ('0300557408','0300381749') THEN 'DISCOUNTERS' ELSE canal_estrategico_desc END` | Tipo de cadena que usa el cliente (con lógica especial para Discounters) |
| **Market type** | `tipo_mercado_desc` | Tamaño/tipo del mercado del producto vendido |
| **Tipo mercado** | `tipo_mercado` | Mercado al que pertenece el producto |
| **ID Cliente** | `cliente_id` | Identificador del cliente a quien se realizó la venta |
| **Cliente** | `cliente_desc` | Nombre/descripción del cliente a quien se realizó la venta |

### Dimensiones Geográficas y Organizacionales

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Region** | `direccion_regional_desc` | Nombre de la región a la que pertenece |
| **Gerencia Zona** | `gerencia_zona_desc` | Estado en donde se hizo la venta |
| **Zona** | `zona_desc` | Estado en donde se hizo la compra del producto |
| **Zona de Ventas** | `zona_ventas_desc` | Zona en la cual se realizó la venta |
| **Oficina de Ventas** | `oficina_ventas_desc` | Oficina en donde se hizo la venta del producto |
| **DR** | `unidad_comercial_desc` | Unidad comercial (Dirección Regional) en donde se hizo la compra |

### Dimensiones Temporales

| Nombre | Expresión (campo fuente) | Descripción |
|--------|--------------------------|-------------|
| **Año** | `anio` | Año en el que se hizo la venta |
| **Mes** | `mes` | Mes en el que se hizo la venta |
| **Dia** | `dia` | Día en que se hizo la venta del producto |
| **fecha** | `CAST(CONCAT(anio, '-', mes, '-', dia) AS DATE)` | Fecha completa de la compra (calculada) |
| **Semana** | `semana` | Número de semana del año en donde se hizo la compra |
| **dia_semana_abrev** | `CASE DAYOFWEEK(...)` — do/lu/ma/mi/ju/vi/sa | Día de la semana abreviado (calculado a partir de la fecha) |

---

## Definición YAML Completa

```yaml
version: 1.1

source: heiaepmx002pwe01.gold_hnk_mx_loc_sellin.tbl_sot_sellin_daily_sales_daily_dashboard

filter: |-
  oficina_ventas_id NOT IN (
    'CH00','CH02','CH04','CH05','CH07','CH14',
    'CK00','CK01','CK02','CK03','CK04','CK05',
    'CK06','CK07','CK08','CK09','CK10','CK11',
    'CK12','CK13','CK14','CK15','CK16','CK17',
    'CK18','CK19','CK20','CK21','CK22','CK23',
    'CK24','CK25','CK26','CK27','CK28',
    'CK29','CK30','CK31','CK32','CK33','CK34',
    'CK35','CK36','CK37','CK38','CK39','CK40',
    'CK41','CK42','CK43','CK44','CK45','CK46',
    'MH00','MH02','MH04','MH05','MH07','MH14'
  ) AND grupo_cuentas_id IN ('0200', '0151', '0150')
  AND categoria_producto_id IN ('002','007','008','009')

dimensions:
  - name: Marca
    expr: desc_marca
    comment: Hace referencia a la marca del producto que se vendio
  - name: Canal Estrategico
    expr: |-
      CASE WHEN cliente_cadena IN ('0300557408','0300381749') THEN 'DISCOUNTERS'
      ELSE canal_estrategico_desc END
    comment: Hace referencia al tipo de cadena que usa el cliente
  - name: Line Extension Desc
    expr: desc_extension_linea
    comment: Es la descripcion de la extension de linea que usa el producto
  - name: HMEX Pack Group Desc
    expr: hmex_pack_group_desc
    comment: Es la descripcion del grupo de packs que pertenece a heinken
  - name: Line Extension ID
    expr: extension_linea_id
    comment: Es un id hacerca de la linea de extension que usa producto para la venta
  - name: Packtype
    expr: tipo_paquete_id
    comment: Es el numero de onzas que tiene el paquete
  - name: HMEX Pack Group
    expr: hmex_pack_group
    comment: Es la descripcion del prodcuto que se compro
  - name: ID Presentacion CCM
    expr: presentacion_ccm_id
    comment: Es un numero que representa la cantidad de
  - name: Market type
    expr: tipo_mercado_desc
    comment: Es el tamano del producto que se vendio
  - name: Marca agrupadora
    expr: desc_marca_producto
    comment: Representa la marca a la que esta relacionado el producto
  - name: Multipack
    expr: desc_multipack
    comment: Representa la cantidad de latas que tiene si es un six pack o un 12 pack
  - name: Presentacion
    expr: desc_presentacion
    comment: Es la forma en la que se presenta lo comprado puede ser una botella o una lata
  - name: Presentacion CCM
    expr: desc_presentacion_ccm
    comment: Es una descripcion del tamaño del producto que se compro
  - name: Retornable
    expr: desc_retornable
    comment: Es el tipo de retorno que tiene el producto que se vendio
  - name: Subcategoria
    expr: desc_subcategoria
    comment: Hace referencia a la subcategoria que pertenece el producto que se vendio
  - name: Region
    expr: direccion_regional_desc
    comment: Es el nombre de la region a la que pertenece el prodcuto
  - name: Año
    expr: anio
    comment: Es el anio en el que se hizo la venta
  - name: Mes
    expr: mes
    comment: Es el mes en el que se hizo la venta
  - name: Dia
    expr: dia
    comment: Es el dia que se hizo la venta del prodcuto
  - name: fecha
    expr: "CAST(CONCAT(anio, '-', mes, '-', dia) AS DATE)"
    comment: Representa la fecha en la cual se hizo la compra
  - name: dia_semana_abrev
    expr: |-
      CASE DAYOFWEEK(CAST(CONCAT(anio, '-', mes, '-', dia) AS DATE))
      WHEN 1 THEN 'do'
      WHEN 2 THEN 'lu'
      WHEN 3 THEN 'ma'
      WHEN 4 THEN 'mi'
      WHEN 5 THEN 'ju'
      WHEN 6 THEN 'vi'
      WHEN 7 THEN 'sa'
      END
    comment: Hace referencia al dia de la semana abreviado en el que se hizo la compra
  - name: Gerencia Zona
    expr: gerencia_zona_desc
    comment: Hace referencia al estado que en donde se hizo la venta
  - name: Oficina de Ventas
    expr: oficina_ventas_desc
    comment: Hace referencia a la oficina en donde se hizo la venta del producto
  - name: Semana
    expr: semana
    comment: Es el numero de la semana del año en donde se hizo la compra
  - name: Tipo mercado
    expr: tipo_mercado
    comment: Hace referencia al mercado que pertenece el producto que se vendio
  - name: DR
    expr: unidad_comercial_desc
    comment: Es la unidad comercial en donde se hizo la compra
  - name: Zona
    expr: zona_desc
    comment: Representa el estado en donde se hizo la compra del producto
  - name: Zona de Ventas
    expr: zona_ventas_desc
    comment: Hace referencia a la zona en la cual se hizo
  - name: ID Cliente
    expr: cliente_id
    comment: Identificador del cliente a quien se realizo la venta
  - name: Cliente
    expr: cliente_desc
    comment: Descripción del cliente a quien se realizo la venta
  - name: ID SKU
    expr: material_id
    comment: Identificador del material que se vendio
  - name: SKU
    expr: desc_material
    comment: Descripcion del material que se vendio
  - name: SKU_NPI
    expr: NPI
    comment: "Campo utilizado para identificar productos nuevos y habilitar análisis específicos de adopción, escala, cobertura y desempeño temprano post-lanzamiento."

measures:
  - name: HL Actual
    expr: SUM(dsr_ratio_anio_actual)
    comment: Hace referencia al total de ventas del anio actual
  - name: HL Anterior
    expr: SUM(dsr_ratio_anio_anterior)
    comment: Hacer referencia al total de ventas del anio anterior
  - name: HL Anterior mes cerrado
    expr: SUM(dsr_ratio_anio_anterior_hoy)
    comment: Hace referencia al total de ventas del dia de consulta pero del anio completo anterior
```

---

## Usuarios Principales (Top Users)

- MONTEF05@heiway.net
- Ricardo Benavides
- Benito Antonio Rodríguez
- Jorge Emilio Ibarra

---

## Activos Relacionados

- **Data_Analytics** (Dashboard)
- **hnk_mx_data_analytics-job** (Job)
- **Daily Sales Assistant** (Asset / Genie AI)

---

## Notas Técnicas

- Esta es una **Metric View** de Databricks (no una tabla ni una vista materializada). Está diseñada para ser consumida directamente por **Genie AI** y dashboards mediante lenguaje natural.
- Tiene **3 medidas** (métricas numéricas) y **33 dimensiones** (atributos para filtrar y agrupar).
- La dimensión **Canal Estrategico** incluye lógica de negocio: dos cadenas específicas (`0300557408` y `0300381749`) son reclasificadas como `'DISCOUNTERS'` independientemente de su canal estratégico original.
- La dimensión **fecha** y **dia_semana_abrev** son **calculadas** (no existen como columnas en la tabla fuente): se construyen concatenando los campos `anio`, `mes` y `dia`.
- La dimensión **SKU_NPI** mapea al campo `NPI` de la tabla fuente, que indica si es un producto nuevo (New Product Introduction).
- El filtro excluye **46 códigos de oficinas de ventas** de los grupos CH, CK y MH, limitando el análisis al universo de negocio principal de México.
- Fuente directa: `heiaepmx002pwe01.gold_hnk_mx_loc_sellin.tbl_sot_sellin_daily_sales_daily_dashboard`

---

*Documentación generada el 22 de mayo de 2026 a partir del Databricks Unity Catalog.*
