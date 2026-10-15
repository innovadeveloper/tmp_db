## core_operations.trip_location_2026_w05
**Tipo:** tabla
**Proposito:** Almacena la ubicación geográfica de los viajes durante la semana 5 del año 2026.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| location_id | bigint | No | nextval('core_operations.trip_location_location_id_seq'::regclass) | Identificador único de la ubicación |
| trip_id | bigint | No | Por confirmar | Identificador del viaje |
| gps_timestamp | timestamp with time zone | No | Por confirmar | Fecha y hora de la medición de la ubicación |
| latitude | numeric(10,8) | No | Por confirmar | Latitud de la ubicación |
| longitude | numeric(11,8) | No | Por confirmar | Longitud de la ubicación |
| speed_kmh | numeric(5,2) | Sí | Por confirmar | Velocidad del viaje en kilómetros por hora |
| heading | numeric(5,2) | Sí | Por confirmar | Dirección del viaje en grados |
| accuracy_meters | numeric(6,2) | Sí | Por confirmar | Precisión de la medición en metros |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro |

**Clave primaria:** location_id, gps_timestamp
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_location_latitude: Verifica que la latitud esté entre -90 y 90 grados.
- chk_location_longitude: Verifica que la longitud esté entre -180 y 180 grados.
**Triggers:** Ninguno
**Observaciones:** La tabla no tiene restricciones adicionales ni triggers.
