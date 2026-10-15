## fleet.gps_raw_event
**Tipo:** tabla
**Proposito:** Almacena eventos GPS brutos recopilados por dispositivos GPS, particionados semanalmente.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| raw_event_id | bigint | No | Sí | Identificador único del evento GPS. |
| gps_device_id | integer | No | Sí | Identificador del dispositivo GPS que generó el evento. |
| vehicle_id | integer | Sí | Sí | Identificador del vehículo asociado al evento. |
| beacon_mac_address | character varying(17) | Sí | Sí | MAC del beacon BLE (anti-suplantación, fase 2). |
| latitude | numeric(10,8) | No | Sí | Latitud GPS en grados decimales. |
| longitude | numeric(11,8) | No | Sí | Longitud GPS en grados decimales. |
| altitude | numeric(8,2) | Sí | Sí | Altitud GPS en metros. |
| speed_kmh | numeric(5,2) | Sí | Sí | Velocidad del vehículo en km/h. |
| heading | numeric(5,2) | Sí | Sí | Dirección del vehículo en grados. |
| accuracy_meters | numeric(6,2) | Sí | Sí | Precisión del GPS en metros. |
| satellites | integer | Sí | Sí | Número de satélites utilizados por el GPS. |
| gps_timestamp | timestamp with time zone | No | Sí | Timestamp del evento GPS. |
| server_timestamp | timestamp with time zone | Sí | now() | Timestamp del servidor cuando se inserta el evento. |
| battery_level | integer | Sí | Sí | Nivel de batería del dispositivo GPS. |
| raw_data | character varying | Sí | Sí | Payload JSON completo para debugging. |
| created_at | timestamp with time zone | Sí | now() | Timestamp de creación del evento. |

**Clave primaria:** raw_event_id, gps_timestamp

**Claves foraneas:** 
- gps_device_id -> fleet.gps_device.gps_device_id
- vehicle_id -> fleet.vehicle.vehicle_id

**Indices y restricciones:** 
- chk_gps_raw_accuracy: Verifica que la precisión del GPS sea mayor que 50 metros.
- chk_gps_raw_battery: Verifica que el nivel de batería esté entre 0 y 100.
- chk_gps_raw_heading: Verifica que la dirección esté entre 0 y 360 grados.
- chk_gps_raw_latitude: Verifica que la latitud esté entre -90 y 90 grados.
- chk_gps_raw_longitude: Verifica que la longitud esté entre -180 y 180 grados.
- chk_gps_raw_satellites: Verifica que el número de satélites sea mayor o igual a 0.
- chk_gps_raw_speed: Verifica que la velocidad esté entre 0 y 250 km/h.
- idx_gps_raw_accuracy: Índice B-tree en accuracy_meters para eventos con precisión mayor a 50 metros.
- idx_gps_raw_device_time: Índice B-tree en gps_device_id y gps_timestamp para mejorar la consulta por dispositivo y tiempo.
- idx_gps_raw_timestamp: Índice B-tree en gps_timestamp para mejorar la consulta por tiempo.
- idx_gps_raw_vehicle_time: Índice B-tree en vehicle_id y gps_timestamp para mejorar la consulta por vehículo y tiempo.

**Triggers:** No se especifican triggers en el SQL proporcionado.

**Observaciones:** El evento se particiona semanalmente, lo que facilita la gestión y consulta de datos históricos. Las restricciones de verificación aseguran la integridad de los datos.
