## core_operations.trip_event
**Tipo:** tabla
**Proposito:** Almacena información sobre eventos asociados a viajes, incluyendo su tipo, subtipo, ubicación, velocidad y gravedad.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| trip_event_id | bigint | No | Sí | Identificador único del evento de viaje. |
| trip_id | bigint | No | Sí | Identificador del viaje al que pertenece el evento. |
| event_type | character varying(50) | No | Sí | Tipo de evento (por ejemplo, "Siniestro", "Reparación"). |
| event_subtype | character varying(50) | Sí | Sí | Subtipo de evento, si es aplicable. |
| event_timestamp | timestamp with time zone | No | Sí | Fecha y hora exacta del evento. |
| latitude | numeric(10,8) | Sí | Sí | Latitud geográfica donde ocurrió el evento. |
| longitude | numeric(11,8) | Sí | Sí | Longitud geográfica donde ocurrió el evento. |
| speed_kmh | numeric(5,2) | Sí | Sí | Velocidad en kilómetros por hora al momento del evento. |
| severity | character varying(20) | Sí | Sí | Gravedad del evento, puede ser 'CRITICAL', 'HIGH', 'MEDIUM', 'LOW' o 'INFO'. |
| description | text | Sí | Sí | Descripción detallada del evento. |
| metadata | jsonb | Sí | Sí | Metadatos adicionales en formato JSONB. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro. |

**Clave primaria:** trip_event_id
**Claves foraneas:** trip_id -> core_operations.trip.trip_id
**Indices y restricciones:** 
- chk_event_severity: Verifica que el valor de severity esté en el conjunto permitido.
- idx_trip_event_meta_gin: Índice GIN para la columna metadata.
- idx_trip_event_trip: Índice B-tree para trip_id y event_timestamp.
- idx_trip_event_type: Índice B-tree para event_type y event_timestamp en orden descendente.
**Triggers:** Ninguna
**Observaciones:** Ninguna
