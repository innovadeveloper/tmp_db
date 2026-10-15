## core_operations.trip_location
**Tipo:** tabla
**Proposito:** Almacena la ubicación geográfica de los viajes, incluyendo detalles como la latitud, longitud, velocidad y dirección.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| location_id | bigint | No | nextval('core_operations.trip_location_location_id_seq'::regclass) | Identificador único de la ubicación del viaje. |
| trip_id | bigint | No | Por confirmar | Identificador del viaje al que pertenece esta ubicación. |
| gps_timestamp | timestamp with time zone | No | Por confirmar | Fecha y hora exacta de la medición de la ubicación. |
| latitude | numeric(10,8) | No | Por confirmar | Latitud de la ubicación geográfica. |
| longitude | numeric(11,8) | No | Por confirmar | Longitud de la ubicación geográfica. |
| speed_kmh | numeric(5,2) | Sí | Por confirmar | Velocidad medida en kilómetros por hora. |
| heading | numeric(5,2) | Sí | Por confirmar | Dirección de movimiento en grados. |
| accuracy_meters | numeric(6,2) | Sí | Por confirmar | Precisión de la medición de la ubicación en metros. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación de la entrada. |

**Clave primaria:** trip_location_pkey (location_id, gps_timestamp)
**Claves foraneas:** Ninguna
**Indices y restricciones:** 
- chk_location_latitude: Verifica que la latitud esté entre -90 y 90 grados.
- chk_location_longitude: Verifica que la longitud esté entre -180 y 180 grados.
- idx_trip_location_trip: Índice btree en trip_id y gps_timestamp para mejorar la eficiencia de las consultas.

**Triggers:** No se especifican en el SQL proporcionado.

**Observaciones:** El uso de particiones por rango en la columna gps_timestamp permite mejorar el rendimiento al almacenar y consultar datos históricos de viajes.
