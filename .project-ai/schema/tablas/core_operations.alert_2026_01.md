## core_operations.alert_2026_01
**Tipo:** tabla
**Proposito:** Almacena registros de alertas generadas en el sistema, incluyendo su tipo, entidad afectada, gravedad, estado y metadatos.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| alert_id | bigint | No | nextval('core_operations.alert_alert_id_seq'::regclass) | Identificador único de la alerta |
| alert_type_id | integer | No | Por confirmar | Identificador del tipo de alerta |
| entity_type | character varying(20) | No | Por confirmar | Tipo de entidad afectada por la alerta (VEHICLE, DRIVER, TRIP, ROUTE, SYSTEM) |
| entity_id | bigint | No | Por confirmar | Identificador de la entidad afectada |
| trip_id | bigint | Sí | Por confirmar | Identificador del viaje asociado a la alerta |
| vehicle_id | integer | Sí | Por confirmar | Identificador del vehículo asociado a la alerta |
| driver_id | integer | Sí | Por confirmar | Identificador del conductor asociado a la alerta |
| severity | character varying(20) | No | Por confirmar | Gravedad de la alerta (CRITICAL, HIGH, MEDIUM, LOW, INFO) |
| alert_timestamp | timestamp with time zone | No | now() | Fecha y hora en que se generó la alerta |
| latitude | numeric(10,8) | Sí | Por confirmar | Latitud geográfica de la alerta |
| longitude | numeric(11,8) | Sí | Por confirmar | Longitud geográfica de la alerta |
| description | text | Sí | Por confirmar | Descripción detallada de la alerta |
| metadata | jsonb | Sí | Por confirmar | Metadatos adicionales en formato JSONB |
| acknowledged_by | bigint | Sí | Por confirmar | Identificador del usuario que reconoció la alerta |
| acknowledged_at | timestamp with time zone | Sí | Por confirmar | Fecha y hora en que la alerta fue reconocida |
| resolved_at | timestamp with time zone | Sí | Por confirmar | Fecha y hora en que la alerta fue resuelta |
| auto_closed_at | timestamp with time zone | Sí | Por confirmar | Fecha y hora en que la alerta fue cerrada automáticamente |
| status | character varying(20) | No | 'ACTIVE' | Estado actual de la alerta (ACTIVE, ACKNOWLEDGED, RESOLVED, AUTO_CLOSED) |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó la alerta |

**Clave primaria:** alert_id, alert_timestamp

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- chk_alert_entity: Verifica que el entity_type sea uno de los permitidos (VEHICLE, DRIVER, TRIP, ROUTE, SYSTEM).
- chk_alert_severity: Verifica que el severity sea uno de los permitidos (CRITICAL, HIGH, MEDIUM, LOW, INFO).
- chk_alert_status: Verifica que el status sea uno de los permitidos (ACTIVE, ACKNOWLEDGED, RESOLVED, AUTO_CLOSED).
- alert_2026_01_pkey: Índice primario compuesto por alert_id y alert_timestamp.
- alert_2026_01_alert_type_id_alert_timestamp_idx: Índice B-tree por alert_type_id y alert_timestamp en orden descendente.
- alert_2026_01_metadata_idx: Índice GIN para el campo metadata.
- alert_2026_01_status_alert_timestamp_idx: Índice B-tree por status y alert_timestamp en orden descendente.
- alert_2026_01_status_alert_timestamp_idx1: Índice B-tree por status y alert_timestamp en orden descendente, filtrado para status = 'ACTIVE'.
- alert_2026_01_vehicle_id_alert_timestamp_idx: Índice B-tree por vehicle_id y alert_timestamp en orden descendente.
- alert_2026_01_vehicle_id_alert_timestamp_idx1: Índice B-tree por vehicle_id y alert_timestamp en orden descendente, filtrado para status = 'ACTIVE'.

**Triggers:** Por confirmar

**Observaciones:** 
- La tabla no tiene triggers definidos.
- El campo trip_id es opcional, lo que sugiere que no todas las alertas están asociadas a un viaje.
- El campo status tiene un valor por defecto de 'ACTIVE', lo que indica que las alertas se crean en estado activo.
- El campo created_at tiene un valor por defecto de la fecha y hora actual, lo que indica que las alertas se crean automáticamente cuando se insertan.
