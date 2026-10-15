## core_operations.trip_location_2026_w26
**Tipo:** tabla
**Proposito:** Almacena la ubicación GPS de los viajes durante la semana 26 del año 2026.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| location_id | bigint | No | nextval('core_operations.trip_location_location_id_seq'::regclass) | Identificador único de la ubicación |
| trip_id | bigint | No | Ninguna | Identificador del viaje |
| gps_timestamp | timestamp with time zone | No | Ninguna | Timestamp del GPS |
| latitude | numeric(10,8) | No | Ninguna | Latitud GPS |
| longitude | numeric(11,8) | No | Ninguna | Longitud GPS |
| speed_kmh | numeric(5,2) | Sí | Ninguna | Velocidad en km/h |
| heading | numeric(5,2) | Sí | Ninguna | Dirección de encabezado |
| accuracy_meters | numeric(6,2) | Sí | Ninguna | Precisión en metros |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación |

**Clave primaria:** location_id, gps_timestamp
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_location_latitude: Verifica que la latitud esté entre -90 y 90 grados.
- chk_location_longitude: Verifica que la longitud esté entre -180 y 180 grados.
- trip_location_2026_w26_trip_id_gps_timestamp_idx: Índice en trip_id y gps_timestamp para mejorar la eficiencia de las consultas.

**Triggers:** Ninguno

**Observaciones:** 
- La tabla utiliza una secuencia para generar automáticamente el `location_id`.
- Las restricciones de latitud y longitud aseguran que los valores estén dentro de los límites válidos para coordenadas GPS.
- El índice en `trip_id` y `gps_timestamp` puede mejorar el rendimiento de consultas que filtran por estos campos.
