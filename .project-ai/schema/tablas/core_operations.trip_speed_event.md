## core_operations.trip_speed_event
**Tipo:** tabla  
**Proposito:** Almacena eventos de velocidad durante viajes, incluyendo detalles sobre la velocidad, el límite de velocidad, la gravedad del evento y la duración.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| speed_event_id | bigint | No | nextval('core_operations.trip_speed_event_speed_event_id_seq'::regclass) | Identificador único del evento de velocidad. |
| trip_id | bigint | No | Ninguna | Identificador del viaje al que pertenece el evento de velocidad. |
| event_timestamp | timestamp with time zone | No | Ninguna | Fecha y hora exacta del evento de velocidad. |
| latitude | numeric(10,8) | No | Ninguna | Latitud geográfica donde ocurrió el evento de velocidad. |
| longitude | numeric(11,8) | No | Ninguna | Longitud geográfica donde ocurrió el evento de velocidad. |
| speed_kmh | numeric(5,2) | No | Ninguna | Velocidad medida en kilómetros por hora. |
| speed_limit_kmh | integer | Sí | Ninguna | Límite de velocidad en kilómetros por hora. |
| excess_kmh | numeric(5,2) | Sí | Ninguna | Exceso de velocidad sobre el límite permitido, en kilómetros por hora. |
| duration_seconds | integer | Sí | Ninguna | Duración del evento de velocidad en segundos. |
| severity | character varying(20) | Sí | Ninguna | Gravedad del evento de velocidad, puede ser 'CRITICAL', 'HIGH', 'MEDIUM', o 'LOW'. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro del evento de velocidad. |

**Clave primaria:** speed_event_id  
**Claves foraneas:** Ninguna  
**Indices y restricciones:**  
- `trip_speed_event_pkey`: Clave primaria en `speed_event_id`.  
- `idx_speed_event_trip`: Índice B-tree en `trip_id` y `event_timestamp` para mejorar la eficiencia de las consultas que filtran por viaje y ordenan por tiempo.  
- `chk_speed_severity`: Restricción CHECK para asegurar que el valor de `severity` sea uno de los permitidos.

**Triggers:** Ninguno  
**Observaciones:** Ninguna
