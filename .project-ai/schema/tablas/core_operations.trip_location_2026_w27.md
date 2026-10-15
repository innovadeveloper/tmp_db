## core_operations.trip_location_2026_w27
**Tipo:** tabla
**Proposito:** Almacena la ubicación geográfica de los viajes durante la semana 27 del año 2026.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| location_id | bigint | No | nextval('core_operations.trip_location_location_id_seq'::regclass) | Identificador único de la ubicación del viaje. |
| trip_id | bigint | No | Ninguna | Identificador del viaje al que pertenece la ubicación. |
| gps_timestamp | timestamp with time zone | No | Ninguna | Fecha y hora exacta de la medición de la ubicación según el GPS. |
| latitude | numeric(10,8) | No | Ninguna | Latitud de la ubicación geográfica. |
| longitude | numeric(11,8) | No | Ninguna | Longitud de la ubicación geográfica. |
| speed_kmh | numeric(5,2) | Sí | Ninguna | Velocidad del vehículo en kilómetros por hora. |
| heading | numeric(5,2) | Sí | Ninguna | Dirección del movimiento del vehículo en grados. |
| accuracy_meters | numeric(6,2) | Sí | Ninguna | Precisión de la medición de la ubicación en metros. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro. |

**Clave primaria:** location_id, gps_timestamp
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_location_latitude: Verifica que la latitud esté entre -90 y 90 grados.
- chk_location_longitude: Verifica que la longitud esté entre -180 y 180 grados.
- trip_location_2026_w27_trip_id_gps_timestamp_idx: Índice btree en trip_id y gps_timestamp para mejorar la eficiencia de las consultas.

**Triggers:** Ninguno

**Observaciones:** 
- La tabla utiliza una secuencia para generar automáticamente los valores de location_id.
- Las restricciones de latitud y longitud aseguran que los valores estén dentro de los límites válidos para coordenadas geográficas.
- El índice en trip_id y gps_timestamp puede mejorar el rendimiento de las consultas que buscan registros por viaje y tiempo.
