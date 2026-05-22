# Documentación: Vista Materializada `tbl_sot_sellin_daily_sales_daily_dashboard`

## Información General

| Campo | Valor |
|-------|-------|
| **Nombre** | tbl_sot_sellin_daily_sales_daily_dashboard |
| **Catálogo** | heiaepmx002pwe01 |
| **Esquema / Base de datos** | gold_hnk_mx_loc_sellin |
| **Tipo** | MATERIALIZED_VIEW |
| **Propietario** | HEI-AEP-MX002-01-P-DATAPROCESSING |
| **Fecha de creación** | 19 de septiembre de 2025, 05:00 PM |
| **Última actualización** | 22 de mayo de 2026, 11:40 AM |
| **Tipo de cómputo de creación** | DBSQL Warehouse Compute |
| **Pipeline ID** | 3ff5d02b-f72d-4b97-9fcc-9ea9c6bda6c5 |
| **Table ID** | 05454499-1710-41fe-81d6-0e86193c7dd4 |
| **Estado del pipeline** | Completado (22 may 2026, 11:43 AM) |
| **Programación de refresco** | Sin programación |

---

## Descripción

Vista materializada del dominio **Sell-In** que consolida las ventas diarias para el dashboard de ventas diarias. Contiene información transaccional y dimensional de productos, clientes, rutas, jerarquías comerciales y métricas de venta para la operación de México (AEP OpCo Mexico).

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
| Certified | True |
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

## Columnas (279 columnas)

### Dimensiones Temporales

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 0 | `planta_id` | string | Identificador de la planta |
| 1 | `tipo_mercado` | string | Tipo de mercado |
| 2 | `dia` | string | Día de la venta |
| 3 | `anio` | string | Año de la venta |
| 4 | `anio_mes` | string | Combinación año-mes |
| 5 | `mes` | string | Mes de la venta |
| 6 | `semana` | string | Semana del año |
| 7 | `num_dia_semana` | string | Número de día de la semana |
| 8 | `dsr_ratio_anio_actual` | string | Ratio DSR del año actual |
| 9 | `dsr_ratio_anio_anterior` | string | Ratio DSR del año anterior |
| 10 | `dsr_ratio_anio_anterior_hoy` | string | Ratio DSR del año anterior a la fecha actual |

### Dimensiones de Producto

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 11 | `material_id` | string | Identificador del material / producto |
| 12 | `desc_material` | string | Descripción del material |
| 13 | `sku` | string | SKU del producto |
| 14 | `agrupador_producto_id` | string | Identificador del agrupador de producto |
| 15 | `grupo_producto_id` | string | Identificador del grupo de producto |
| 16 | `desc_grupo_producto` | string | Descripción del grupo de producto |
| 17 | `categoria_producto_id` | string | Identificador de la categoría de producto |
| 18 | `desc_categoria_producto` | string | Descripción de la categoría de producto |
| 19 | `desc_tipo_producto` | string | Descripción del tipo de producto |
| 20 | `categoria_id` | string | Identificador de categoría |
| 21 | `desc_categoria` | string | Descripción de categoría |
| 22 | `agrupacion_categoria_id` | string | Identificador de agrupación de categoría |
| 23 | `desc_agrupacion_categoria` | string | Descripción de agrupación de categoría |
| 24 | `desc_subcategoria` | string | Descripción de subcategoría |
| 25 | `marca_producto_id` | string | Identificador de marca del producto |
| 26 | `desc_marca_producto` | string | Descripción de marca del producto |
| 27 | `agrupador_marca_id` | string | Identificador del agrupador de marca |
| 28 | `desc_agrupador_marca` | string | Descripción del agrupador de marca |
| 29 | `marca_id` | string | Identificador de marca |
| 30 | `desc_marca` | string | Descripción de marca |
| 31 | `familia_marca_id` | string | Identificador de familia de marca |
| 32 | `desc_familia_marca` | string | Descripción de familia de marca |
| 33 | `extension_linea_id` | string | Identificador de extensión de línea |
| 34 | `desc_extension_linea` | string | Descripción de extensión de línea |
| 35 | `operacion_id` | string | Identificador de operación |
| 36 | `desc_operacion` | string | Descripción de operación |
| 37 | `multipack_id` | string | Identificador de multipack |
| 38 | `desc_multipack` | string | Descripción de multipack |
| 39 | `tamano_paquete_id` | string | Identificador de tamaño de paquete |
| 40 | `desc_tamano_paquete` | string | Descripción de tamaño de paquete |
| 41 | `tamano_paquete_primario_id` | string | Identificador de tamaño de paquete primario |
| 42 | `desc_tamano_paquete_primario` | string | Descripción de tamaño de paquete primario |
| 43 | `tipo_paquete_id` | string | Identificador de tipo de paquete |
| 44 | `color_envase_id` | string | Identificador de color de envase |
| 45 | `desc_color_envase` | string | Descripción de color de envase |
| 46 | `presentacion_ccm_id` | string | Identificador de presentación CCM |
| 47 | `desc_presentacion_ccm` | string | Descripción de presentación CCM |
| 48 | `presentacion_id` | string | Identificador de presentación |
| 49 | `desc_presentacion` | string | Descripción de presentación |
| 50 | `retornabilidad_id` | string | Identificador de retornabilidad |
| 51 | `desc_retornabilidad` | string | Descripción de retornabilidad |
| 52 | `retornable_id` | string | Identificador de retornable |
| 53 | `desc_retornable` | string | Descripción de retornable |
| 54 | `forma_id` | string | Identificador de forma |
| 55 | `desc_forma` | string | Descripción de forma |
| 56 | `udm_base` | string | Unidad de medida base |
| 57 | `tipo_producto_venta_id` | string | Identificador de tipo de producto de venta |
| 58 | `tipo_producto_venta_desc` | string | Descripción de tipo de producto de venta |
| 59 | `hmex_pack_group_id` | string | Identificador de grupo de empaque HMEX |
| 60 | `hmex_pack_group_desc` | string | Descripción de grupo de empaque HMEX |
| 61 | `hmex_pack_group_contador` | string | Contador del grupo de empaque HMEX |
| 62 | `hmex_pack_group` | string | Grupo de empaque HMEX |
| 63 | `npi` | string | Indicador NPI (New Product Introduction) |

### Dimensiones de Cliente

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 64 | `cliente_id` | string | Identificador del cliente |
| 65 | `organizacion_ventas_id` | string | Identificador de organización de ventas |
| 66 | `canal_distribucion_id` | string | Identificador del canal de distribución |
| 67 | `sector_id` | string | Identificador del sector |
| 68 | `sociedad_id` | string | Identificador de la sociedad |
| 69 | `cliente_desc` | string | Descripción / nombre del cliente |
| 70 | `organizacion_ventas_desc` | string | Descripción de organización de ventas |
| 71 | `creado_por` | string | Usuario que creó el registro |
| 72 | `grupo_autorizacion_id` | string | Identificador del grupo de autorización |
| 73 | `pet_borrado_flag` | string | Indicador de petición de borrado |
| 74 | `grupo_estadistica_id` | string | Identificador del grupo de estadística |
| 75 | `bloq_pedido_comercial_flag` | string | Indicador de bloqueo de pedido comercial |
| 76 | `esquema_cliente_id` | string | Identificador del esquema de cliente |
| 77 | `gerencia_zona_id` | string | Identificador de gerencia de zona |
| 78 | `gerencia_zona_desc` | string | Descripción de gerencia de zona |
| 79 | `zona_ventas_id` | string | Identificador de zona de ventas |
| 80 | `zona_ventas_desc` | string | Descripción de zona de ventas |
| 81 | `grupo_precios_id` | string | Identificador de grupo de precios |
| 82 | `tipo_lista_id` | string | Identificador de tipo de lista |
| 83 | `probabilidad_pedido` | string | Probabilidad de pedido |
| 84 | `bloq_entrega_comercial_flag` | string | Indicador de bloqueo de entrega comercial |
| 85 | `entrega_completa_falg` | string | Indicador de entrega completa |
| 86 | `max_parciales` | string | Máximo de entregas parciales |
| 87 | `entrega_parcial_flag` | string | Indicador de entrega parcial |
| 88 | `agrupamiento_pedido` | string | Agrupamiento de pedido |
| 89 | `part_lotes` | string | Participación en lotes |
| 90 | `prioridad_entrega` | string | Prioridad de entrega |
| 91 | `cuenta_cliente_id` | string | Identificador de cuenta de cliente |
| 92 | `condicion_expedicion_id` | string | Identificador de condición de expedición |
| 93 | `bloq_factura_comercial_flag` | string | Indicador de bloqueo de factura comercial |
| 94 | `tratamiento_factura` | string | Tratamiento de factura |
| 95 | `fecha_facturacion_id` | string | Identificador de fecha de facturación |
| 96 | `fecha_lista_factura_id` | string | Identificador de fecha de lista de factura |
| 97 | `presupuesto_estimativo_costes` | string | Presupuesto estimativo de costes |
| 98 | `limite_presupuesto_estimativo` | string | Límite del presupuesto estimativo |
| 99 | `moneda_id` | string | Identificador de moneda |
| 100 | `gec_id` | string | Identificador GEC |
| 101 | `gec_desc` | string | Descripción GEC |
| 102 | `grupo_imputacion_id` | string | Identificador de grupo de imputación |
| 103 | `centro_id` | string | Identificador del centro |
| 104 | `centro_desc` | string | Descripción del centro |
| 105 | `planta_homologada_id` | string | Identificador de planta homologada |
| 106 | `grupo_vendedores_id` | string | Identificador del grupo de vendedores |
| 107 | `grupo_vendedores_desc` | string | Descripción del grupo de vendedores |
| 108 | `oficina_ventas_id` | string | Identificador de oficina de ventas |
| 109 | `oficina_ventas_desc` | string | Descripción de oficina de ventas |
| 110 | `direccion_regional_desc` | string | Descripción de la dirección regional |
| 111 | `zona_desc` | string | Descripción de zona |
| 112 | `tipo_mercado_desc` | string | Descripción del tipo de mercado |
| 113 | `tipo_oficina` | string | Tipo de oficina |

### Dimensiones de Propuesta y Segmentación

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 114 | `propuesta_posiciones` | string | Propuesta de posiciones |
| 115 | `soc_nec` | string | Sociedad/necesidad |
| 116 | `tipo_cobro` | string | Tipo de cobro |
| 117 | `grupo_clientes_3_id` | string | Identificador de grupo de clientes 3 |
| 118 | `grupo_clientes_4_id` | string | Identificador de grupo de clientes 4 |
| 119 | `modalidad_venta_id` | string | Identificador de modalidad de venta |
| 120 | `modalidad_venta_desc` | string | Descripción de modalidad de venta |
| 121 | `cliente_rappel_flag` | string | Indicador de cliente con rappel |
| 122 | `inicio_rappel` | string | Inicio de rappel |
| 123 | `tipo_cotizacion` | string | Tipo de cotización |
| 124 | `determinacion_precios_flag` | string | Indicador de determinación de precios |
| 125 | `atrib1_flag` | string | Atributo 1 (flag) |
| 126 | `atrib2_flag` | string | Atributo 2 (flag) |
| 127 | `atrib3_flag` | string | Atributo 3 (flag) |
| 128 | `atrib4_flag` | string | Atributo 4 (flag) |
| 129 | `atrib5_flag` | string | Atributo 5 (flag) |
| 130 | `atrib6_flag` | string | Atributo 6 (flag) |
| 131 | `atrib7_flag` | string | Atributo 7 (flag) |
| 132 | `atrib8_flag` | string | Atributo 8 (flag) |
| 133 | `atrib9_flag` | string | Atributo 9 (flag) |
| 134 | `atrib10_flag` | string | Atributo 10 (flag) |
| 135 | `cond_pago_id` | string | Identificador de condición de pago |
| 136 | `esquema_propuesta_prod_id` | string | Identificador de esquema de propuesta de producto |
| 137 | `segmento_precio_id` | string | Identificador de segmento de precio |
| 138 | `segmento_descuento_id` | string | Identificador de segmento de descuento |
| 139 | `bulk_delivery` | string | Indicador de entrega a granel |
| 140 | `cliente_temporal_id` | string | Identificador de cliente temporal |
| 141 | `cliente_temporal_permisos_id` | string | Identificador de permisos de cliente temporal |
| 142 | `condicion_general_id` | string | Identificador de condición general |
| 143 | `condicion_general_desc` | string | Descripción de condición general |
| 144 | `grado_control_id` | string | Identificador de grado de control |
| 145 | `tipo_detallista_id` | string | Identificador de tipo de detallista |
| 146 | `tipo_cadena_id` | string | Identificador de tipo de cadena |
| 147 | `tipo_neg_controlado_id` | string | Identificador de tipo de negocio controlado |
| 148 | `formato_neg_controlado_id` | string | Identificador de formato de negocio controlado |
| 149 | `key_account_id` | string | Identificador de key account |
| 150 | `segmento_portafolio_id` | string | Identificador de segmento de portafolio |
| 151 | `segmento_exhibicion_id` | string | Identificador de segmento de exhibición |
| 152 | `segmento_comunicacion_id` | string | Identificador de segmento de comunicación |
| 153 | `segmento_propuesta_valor_id` | string | Identificador de segmento de propuesta de valor |
| 154 | `segmento_pelicula_exito_id` | string | Identificador de segmento de película de éxito |
| 155 | `ocas_consumo` | string | Ocasión de consumo |
| 156 | `ieps` | string | IEPS (Impuesto Especial sobre Producción y Servicios) |

### Dimensiones de Canal y Ruta

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 157 | `canal_id` | string | Identificador de canal |
| 158 | `canal_desc` | string | Descripción de canal |
| 159 | `ruta` | string | Ruta general |
| 160 | `ruta01_preventa` | string | Ruta 01 - Preventa |
| 161 | `ruta02_entrega` | string | Ruta 02 - Entrega |
| 162 | `ruta03_telmarket` | string | Ruta 03 - Telmarket |
| 163 | `ruta04_telmarket_advisor` | string | Ruta 04 - Telmarket Advisor |
| 164 | `ruta05_ejecutiva_premium` | string | Ruta 05 - Ejecutiva Premium |
| 165 | `ruta06_conquistador` | string | Ruta 06 - Conquistador |
| 166 | `ruta07_developer` | string | Ruta 07 - Developer |
| 167 | `ruta08_on_premise` | string | Ruta 08 - On Premise |
| 168 | `ruta09_sales_executive` | string | Ruta 09 - Sales Executive |
| 169 | `ruta10_convencional` | string | Ruta 10 - Convencional |
| 170 | `ruta11_comerciante` | string | Ruta 11 - Comerciante |
| 171 | `ruta12_edi` | string | Ruta 12 - EDI |
| 172 | `ruta13_opc` | string | Ruta 13 - OPC |
| 173 | `ruta14_dummy` | string | Ruta 14 - Dummy |
| 174 | `ruta15_nec_promoter` | string | Ruta 15 - NEC Promoter |
| 175 | `ruta16_key_account` | string | Ruta 16 - Key Account |
| 176 | `ruta17_telmarket` | string | Ruta 17 - Telmarket |
| 177 | `ruta18` | string | Ruta 18 |
| 178 | `ruta19` | string | Ruta 19 |
| 179 | `ruta20` | string | Ruta 20 |
| 180 | `ruta21` | string | Ruta 21 |
| 181 | `ruta22` | string | Ruta 22 |
| 182 | `ruta23` | string | Ruta 23 |
| 183 | `ruta24` | string | Ruta 24 |
| 184 | `ruta25` | string | Ruta 25 |
| 185 | `ruta26` | string | Ruta 26 |
| 186 | `ruta27` | string | Ruta 27 |
| 187 | `ruta28` | string | Ruta 28 |
| 188 | `ruta29` | string | Ruta 29 |
| 189 | `ruta30` | string | Ruta 30 |

### Dimensiones GEC Virtual y Valor Metálico

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 190 | `gec_virtual_id` | string | Identificador GEC virtual |
| 191 | `gec_virtual_desc` | string | Descripción GEC virtual |
| 192 | `valor_metalico_id` | string | Identificador de valor metálico |
| 193 | `valor_metalico_desc` | string | Descripción de valor metálico |
| 194 | `zona_precios_id` | string | Identificador de zona de precios |
| 195 | `zona_precios_desc` | string | Descripción de zona de precios |
| 196 | `productividad_id` | string | Identificador de productividad |
| 197 | `cliente_clave_id` | string | Identificador de cliente clave |
| 198 | `subtipo_local_id` | string | Identificador de subtipo local |
| 199 | `direccion_id` | string | Identificador de dirección |

### Información de Bloqueos y Datos Fiscales/Administrativos

| # | Columna | Tipo | Descripción |
|---|---------|------|-------------|
| 200 | `bloq_pedido_flag` | string | Indicador de bloqueo de pedido |
| 201 | `ramo_industrial_id` | string | Identificador de ramo industrial |
| 202 | `fecha_creacion` | string | Fecha de creación del registro |
| 203 | `bloq_factura_flag` | string | Indicador de bloqueo de factura |
| 204 | `clave_grupo_id` | string | Identificador de clave de grupo |
| 205 | `grupo_cuentas_id` | string | Identificador de grupo de cuentas |
| 206 | `grupo_cuentas_desc` | string | Descripción del grupo de cuentas |
| 207 | `nivel_socioeconomico` | string | Nivel socioeconómico |
| 208 | `pais` | string | País |
| 209 | `proveedor_id` | string | Identificador de proveedor |
| 210 | `bloq_entrega_flag` | string | Indicador de bloqueo de entrega |
| 211 | `nombre1` | string | Nombre 1 del cliente |
| 212 | `nombre2` | string | Nombre 2 del cliente |
| 213 | `nombre3` | string | Nombre 3 del cliente |
| 214 | `distrito_nielsen` | string | Distrito Nielsen |
| 215 | `distrito1` | string | Distrito 1 |
| 216 | `distrito2` | string | Distrito 2 |
| 217 | `cp` | string | Código postal |
| 218 | `region_id` | string | Identificador de región |
| 219 | `condado` | string | Condado |
| 220 | `clasificacion` | string | Clasificación |
| 221 | `bloq_contable_flag` | string | Indicador de bloqueo contable |
| 222 | `idioma` | string | Idioma |
| 223 | `fiscal_id` | string | Identificador fiscal |
| 224 | `recargo_equival_flag` | string | Indicador de recargo equivalente |
| 225 | `calle` | string | Calle del cliente |
| 226 | `telefono_1` | string | Teléfono 1 |
| 227 | `telefono_2` | string | Teléfono 2 |
| 228 | `fax` | string | Número de fax |
| 229 | `teletex` | string | Número de teletex |
| 230 | `telex` | string | Número de telex |
| 231 | `zona_transporte_id` | string | Identificador de zona de transporte |
| 232 | `cuenta_pro_diversos` | string | Cuenta pro-diversos |
| 233 | `sociedad_gl` | string | Sociedad GL |
| 234 | `fiscal_comunitario_id` | string | Identificador fiscal comunitario |
| 235 | `consumidor_final` | string | Indicador de consumidor final |
| 236 | `ramo_1_id` | string | Identificador de ramo 1 |
| 237 | `moneda` | string | Moneda |
| 238 | `dueno_permiso` | string | Dueño del permiso |
| 239 | `segmento_id` | string | Identificador de segmento |
| 240 | `segmento_desc` | string | Descripción de segmento |
| 241 | `canal_estrategico_id` | string | Identificador de canal estratégico |
| 242 | `canal_estrategico_desc` | string | Descripción de canal estratégico |
| 243 | `atrib9` | string | Atributo 9 |
| 244 | `persona_fisica_flag` | string | Indicador de persona física |
| 245 | `domicilio_fiscal` | string | Domicilio fiscal |
| 246 | `variante_ejercicio` | string | Variante de ejercicio |
| 247 | `utilizacion` | string | Utilización |
| 248 | `curp` | string | CURP (Clave Única de Registro de Población) |
| 249 | `instalacion` | string | Instalación |
| 250 | `persona_id` | string | Identificador de persona |
| 251 | `persona_desc` | string | Descripción de persona |
| 252 | `grupo_canal_id` | string | Identificador de grupo de canal |
| 253 | `grupo_canal_desc` | string | Descripción de grupo de canal |
| 254 | `tipo_canal_id` | string | Identificador de tipo de canal |
| 255 | `tipo_canal_desc` | string | Descripción de tipo de canal |
| 256 | `unidad_comercial_id` | string | Identificador de unidad comercial |
| 257 | `unidad_comercial_desc` | string | Descripción de unidad comercial |
| 258 | `cliente_origen` | string | Cliente de origen |
| 259 | `cliente_cadena` | string | Cliente cadena |
| 260 | `cliente_cadena_profitability` | string | Cliente cadena para análisis de rentabilidad |
| 261 | `ruta_venta` | string | Ruta de venta |
| 262 | `colonia` | string | Colonia del cliente |
| 263 | `latitud` | string | Latitud geográfica del cliente |
| 264 | `longitud` | string | Longitud geográfica del cliente |
| 265 | `sociedad_desc` | string | Descripción de la sociedad |
| 266 | `cuenta_asociada_id` | string | Identificador de cuenta asociada |
| 267 | `notif_pago_flag` | string | Indicador de notificación de pago |
| 268 | `vias_pago_id` | string | Identificador de vías de pago |
| 269 | `bloq_pago_flag` | string | Indicador de bloqueo de pago |
| 270 | `centro_costos` | string | Centro de costos |
| 271 | `grupo_tesoreria_id` | string | Identificador de grupo de tesorería |
| 272 | `registro_ant_id` | string | Identificador de registro anterior |
| 273 | `suplemento_pago` | string | Suplemento de pago |
| 274 | `nivel_reclamacion` | string | Nivel de reclamación |
| 275 | `procedimiento_reclamacion_id` | string | Identificador del procedimiento de reclamación |
| 276 | `personal_id` | string | Identificador de personal |
| 277 | `id_price_segment` | string | Identificador de segmento de precio |
| 278 | `price_segment_description` | string | Descripción del segmento de precio |

---

## Usuarios Principales (Top Users)

- Jorge Emilio Ibarra
- Ricardo Benavides
- Sergio Rivera
- Benito Antonio Rodríguez
- MONTEF05@heiway.net
- HEI-AEP-MX002-01-P-DATAPROCESSING
- Marcela de León

---

## Activos Relacionados

- **Data_Analytics** (Dashboard)
- **hnk_mx_data_analytics-job** (Job)
- **Daily Sales Assistant** (Asset)
- **Producto ROS** (Asset)
- **Daily Sales GROUP BY Day** (Consulta)

---

## Notas Técnicas

- La definición SQL de la vista no está disponible directamente en el catálogo (`Definition not supported for this table`).
- La vista es parte del pipeline `3ff5d02b-f72d-4b97-9fcc-9ea9c6bda6c5`.
- El catálogo base de referencia es `heiaepmx002pwe01` con namespace `default`.
- Compresión utilizada: **Snappy** (para Parquet y ORC).
- Zona horaria de sesión: **Etc/UTC**.
- Formato de datos por defecto: **Delta**.
- Contiene un total de **279 columnas**, todas de tipo `string`.

---

*Documentación generada el 22 de mayo de 2026 a partir del Databricks Unity Catalog.*
