## core_operations.alert
**Tipo:** tabla
**Proposito:** Almacena alertas GPS en tiempo real, particionadas por mes.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| alert_id | bigint | No | nextval('core_operations.alert_alert_id_seq'::regclass) | Identificador único de la alerta |
| alert_type_id | integer | No | | Identificador del tipo de alerta |
| entity_type | character varying(20) | No | | Tipo de entidad afectada (VEHICLE, DRIVER, TRIP, ROUTE, SYSTEM) |
| entity_id | bigint | No | | Identificador de la entidad afectada |
| trip_id | bigint | Sí | | Identificador del viaje asociado |
| vehicle_id | integer | Sí | | Identificador del vehículo asociado |
| driver_id | integer | Sí | | Identificador del conductor asociado |
| severity | character varying(20) | No | | Gravedad de la alerta (CRITICAL, HIGH, MEDIUM, LOW, INFO) |
| alert_timestamp | timestamp with time zone | No | | Fecha y hora en que se generó la alerta |
| latitude | numeric(10,8) | Sí | | Latitud de la ubicación de la alerta |
| longitude | numeric(11,8) | Sí | | Longitud de la ubicación de la alerta |
| description | text | Sí | | Descripción detallada de la alerta |
| metadata | jsonb | Sí | | Metadatos adicionales en formato JSONB |
| acknowledged_by | bigint | Sí | | Identificador del usuario que reconoció la alerta |
| acknowledged_at | timestamp with time zone | Sí | | Fecha y hora en que la alerta fue reconocida |
| resolved_at | timestamp with time zone | Sí | | Fecha y hora en que la alerta fue resuelta |
| auto_closed_at | timestamp with time zone | Sí | | Fecha y hora en que la alerta fue cerrada automáticamente |
| status | character varying(20) | No | 'ACTIVE' | Estado actual de la alerta (ACTIVE, ACKNOWLEDGED, RESOLVED, AUTO_CLOSED) |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se creó la alerta |

**Clave primaria:** alert_id, alert_timestamp

**Claves foraneas:** 
- acknowledged_by -> identity."user".user_id
- driver_id -> hr.driver.driver_id
- alert_type_id -> core_operations.alert_type.alert_type_id
- vehicle_id -> fleet.vehicle.vehicle_id

**Indices y restricciones:** 
- chk_alert_entity: entity_type debe ser uno de los valores permitidos (VEHICLE, DRIVER, TRIP, ROUTE, SYSTEM)
- chk_alert_severity: severity debe ser uno de los valores permitidos (CRITICAL, HIGH, MEDIUM, LOW, INFO)
- chk_alert_status: status debe ser uno de los valores permitidos (ACTIVE, ACKNOWLEDGED, RESOLVED, AUTO_CLOSED)
- alert_pkey: Clave primaria compuesta por alert_id y alert_timestamp
- idx_alert_type: Índice B-tree en alert_type_id y alert_timestamp DESC
- idx_alert_meta_gin: Índice GIN en metadata
- idx_alert_status: Índice B-tree en status y alert_timestamp DESC
- idx_alert_active: Índice B-tree en status y alert_timestamp DESC para alertas activas
- idx_alert_vehicle: Índice B-tree en vehicle_id y alert_timestamp DESC
- idx_alert_vehicle_active: Índice B-tree en vehicle_id y alert_timestamp DESC para alertas activas

**Triggers:** No se especifican triggers en el SQL proporcionado.

**Observaciones:** 
- La tabla está particionada por rango de alert_timestamp.
- La columna trip_id es opcional y puede ser nula.
- La columna acknowledged_by es opcional y puede ser nula.
- La columna resolved_at es opcional y puede ser nula.
- La columna auto_closed_at es opcional y puede ser nula.
