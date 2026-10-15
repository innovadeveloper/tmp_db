## core_operations.alert_2026_07
**Tipo:** tabla
**Proposito:** Almacena registros de alertas generadas en el sistema, incluyendo detalles sobre el tipo de alerta, entidad afectada, gravedad, ubicación, estado y tiempo de ocurrencia.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| alert_id | bigint | No | nextval('core_operations.alert_alert_id_seq'::regclass) | Identificador único de la alerta |
| alert_type_id | integer | No | Por confirmar | Identificador del tipo de alerta |
| entity_type | character varying(20) | No | Por confirmar | Tipo de entidad afectada (VEHICLE, DRIVER, TRIP, ROUTE, SYSTEM) |
| entity_id | bigint | No | Por confirmar | Identificador de la entidad afectada |
| trip_id | bigint | Sí | Por confirmar | Identificador del viaje asociado a la alerta |
| vehicle_id | integer | Sí | Por confirmar | Identificador del vehículo asociado a la alerta |
| driver_id | integer | Sí | Por confirmar | Identificador del conductor asociado a la alerta |
| severity | character varying(20) | No | Por confirmar | Gravedad de la alerta (CRITICAL, HIGH, MEDIUM, LOW, INFO) |
| alert_timestamp | timestamp with time zone | No | now() | Fecha y hora en que se generó la alerta |
| latitude | numeric(10,8) | Sí | Por confirmar | Latitud de la ubicación de la alerta |
| longitude | numeric(11,8) | Sí | Por confirmar | Longitud de la ubicación de la alerta |
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
- chk_alert_entity: Valida que el entity_type sea uno de los permitidos (VEHICLE, DRIVER, TRIP, ROUTE, SYSTEM)
- chk_alert_severity: Valida que el severity sea uno de los permitidos (CRITICAL, HIGH, MEDIUM, LOW, INFO)
- chk_alert_status: Valida que el status sea uno de los permitidos (ACTIVE, ACKNOWLEDGED, RESOLVED, AUTO_CLOSED)
- alert_2026_07_pkey: Clave primaria compuesta por alert_id y alert_timestamp
- alert_2026_07_alert_type_id_alert_timestamp_idx: Índice por alert_type_id y alert_timestamp en orden descendente
- alert_2026_07_metadata_idx: Índice GIN para la columna metadata
- alert_2026_07_status_alert_timestamp_idx: Índice por status y alert_timestamp en orden descendente
- alert_2026_07_status_alert_timestamp_idx1: Índice por status y alert_timestamp en orden descendente, filtrado para status = 'ACTIVE'
- alert_2026_07_vehicle_id_alert_timestamp_idx: Índice por vehicle_id y alert_timestamp en orden descendente
- alert_2026_07_vehicle_id_alert_timestamp_idx1: Índice por vehicle_id y alert_timestamp en orden descendente, filtrado para status = 'ACTIVE'

**Triggers:** Por confirmar

**Observaciones:** 
- La tabla utiliza secuencias para generar valores únicos para alert_id.
- Se aplican restricciones CHECK para garantizar la integridad de los valores en las columnas entity_type, severity y status.
- Se crean índices para mejorar el rendimiento de consultas filtradas por tipo de alerta, gravedad, estado y ubicación.
- El campo status tiene un valor por defecto de 'ACTIVE', lo que sugiere que las alertas se crean en estado activo por defecto.
