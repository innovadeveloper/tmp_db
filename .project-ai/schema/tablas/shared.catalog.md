## shared.catalog
**Tipo:** tabla
**Proposito:** Catálogo genérico sin FKs - valores parametrizables

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| catalog_id | integer | No | nextval('shared.catalog_catalog_id_seq'::regclass) | Identificador único del catálogo |
| category | character varying(50) | No | Por confirmar | Categoría del catálogo (vehicle_status, trip_status, fuel_type) |
| code | character varying(50) | No | Por confirmar | Código único dentro de la categoría |
| name | character varying(100) | No | Por confirmar | Nombre del catálogo |
| description | text | Sí | Por confirmar | Descripción del catálogo |
| display_order | integer | Sí | 0 | Orden de visualización en dropdowns de UI |
| is_active | boolean | Sí | true | Indica si el catálogo está activo |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del catálogo |

**Clave primaria:** catalog_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- uq_catalog_category_code: Único para cada combinación de category y code
- idx_catalog_category: Índice por category y is_active
- idx_catalog_category_order: Índice por category, display_order y is_active (solo para is_active = true)
- idx_catalog_code: Índice por category y code

**Triggers:** Por confirmar

**Particionado:** Por confirmar

**Observaciones:** Por confirmar
