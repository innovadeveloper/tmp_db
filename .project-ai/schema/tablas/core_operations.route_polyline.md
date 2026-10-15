## core_operations.route_polyline
**Tipo:** tabla
**Proposito:** Almacena información sobre las polilíneas asociadas a rutas, incluyendo su dirección y coordenadas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| polyline_id | bigint | No | Sí | Identificador único de la polilínea |
| route_id | integer | No | Sí | Identificador de la ruta a la que pertenece la polilínea |
| direction | character varying(10) | No | Sí | Dirección de la polilínea ('IDA' o 'VUELTA') |
| coordinates | jsonb | No | Sí | Coordenadas de la polilínea en formato JSONB |
| encoded_polyline | text | Sí | Sí | Polilínea codificada |
| total_points | integer | Sí | Sí | Número total de puntos en la polilínea |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación de la polilínea |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización de la polilínea |

**Clave primaria:** polyline_id
**Claves foraneas:** route_id -> core_operations.route(route_id)
**Indices y restricciones:** chk_polyline_direction, uq_polyline_route_direction, idx_polyline_route
**Triggers:** Por confirmar
**Observaciones:** No se han identificado problemas de diseño evidentes.
