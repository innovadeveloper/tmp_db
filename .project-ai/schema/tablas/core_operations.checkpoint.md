## core_operations.checkpoint
**Tipo:** tabla
**Proposito:** Almacena información sobre los puntos de control, paraderos y terminales en una ruta, incluyendo su ubicación geográfica y características específicas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| checkpoint_id | integer | No | Sí | Identificador único del punto de control. |
| route_id | integer | No | Sí | Identificador de la ruta a la que pertenece el punto de control. |
| checkpoint_code | character varying(20) | Sí | Sí | Código único del punto de control. |
| name | character varying(255) | No | Sí | Nombre del punto de control. |
| checkpoint_type | core_operations.checkpoint_type_enum | No | Sí | Tipo de punto de control (paradero, punto de control, terminal). |
| is_route_endpoint | boolean | No | Falso | Indica si el punto de control es el inicio o fin de la ruta. |
| direction | character varying(10) | No | Sí | Dirección del punto de control (IDA, VUELTA, CIRCULAR). |
| sequence_number | integer | No | Sí | Número de secuencia del punto de control en la ruta. |
| latitude | numeric(10,8) | No | Sí | Latitud geográfica del punto de control. |
| longitude | numeric(11,8) | No | Sí | Longitud geográfica del punto de control. |
| distance_from_origin_km | numeric(8,2) | Sí | Sí | Distancia desde el origen de la ruta en kilómetros. |
| estimated_duration_minutes | integer | Sí | Sí | Duración estimada en minutos para llegar a este punto de control. |
| geofence_radius_meters | integer | No | 50 | Radio de geocerca en metros. Obligatorio para puntos de control y terminales. |
| is_active | boolean | No | Verdadero | Indica si el punto de control está activo. |
| created_at | timestamp with time zone | No | Ahora | Fecha y hora de creación del punto de control. |

**Clave primaria:** checkpoint_id

**Claves foraneas:** route_id -> core_operations.route(route_id)

**Indices y restricciones:** 
- chk_checkpoint_direction: Valida que la dirección sea IDA, VUELTA o CIRCULAR.
- chk_checkpoint_geofence: Valida que el radio de geocerca sea mayor que 0.
- chk_checkpoint_latitude: Valida que la latitud esté entre -90 y 90.
- chk_checkpoint_longitude: Valida que la longitud esté entre -180 y 180.
- chk_endpoint_only_terminal: Valida que si el punto de control es un terminal, su tipo debe ser terminal.
- chk_geofence_required_for_control: Valida que si el tipo de punto de control es paradero, el radio de geocerca debe estar definido.

**Triggers:** No se especifican en el SQL proporcionado.

**Observaciones:** No se identificaron problemas de diseño evidentes.
