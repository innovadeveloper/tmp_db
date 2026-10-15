## core_operations.trip_location_2026_w28
**Tipo:** tabla
**Proposito:** Almacena las ubicaciones geográficas de los viajes durante la semana 28 del año 2026.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| location_id | bigint | No | nextval('core_operations.trip_location_location_id_seq'::regclass) | Identificador único de la ubicación |
| trip_id | bigint | No | Por confirmar | Identificador del viaje al que pertenece la ubicación |
| gps_timestamp | timestamp with time zone | No | Por confirmar | Fecha y hora exacta de la medición GPS |
| latitude | numeric(10,8) | No | Por confirmar | Latitud de la ubicación |
| longitude | numeric(11,8) | No | Por confirmar | Longitud de la ubicación |
| speed_kmh | numeric(5,2) | Sí | Por confirmar | Velocidad del vehículo en kilómetros por hora |
| heading | numeric(5,2) | Sí | Por confirmar | Dirección del movimiento del vehículo en grados |
| accuracy_meters | numeric(6,2) | Sí | Por confirmar | Precisión de la medición GPS en metros |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro |

**Clave primaria:** location_id, gps_timestamp
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_location_latitude: Verifica que la latitud esté entre -90 y 90 grados.
- chk_location_longitude: Verifica que la longitud esté entre -180 y 180 grados.
- trip_location_2026_w28_trip_id_gps_timestamp_idx: Índice btree en trip_id y gps_timestamp para mejorar la eficiencia de las consultas.

**Triggers:** Por confirmar

**Observaciones:** 
- La columna `trip_id` no tiene definido un valor por defecto ni se menciona en las restricciones, lo que sugiere que debe ser proporcionado al insertar un nuevo registro.
- La columna `created_at` tiene un valor por defecto que es la fecha y hora actual, lo que facilita el seguimiento de cuándo se creó cada registro.
