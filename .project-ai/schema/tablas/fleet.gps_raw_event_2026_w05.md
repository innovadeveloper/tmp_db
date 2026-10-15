## fleet.gps_raw_event_2026_w05
**Tipo:** tabla
**Proposito:** Almacena eventos de GPS raw recopilados por dispositivos GPS en la semana 05 del año 2026.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| raw_event_id | bigint | No | nextval('fleet.gps_raw_event_raw_event_id_seq'::regclass) | Identificador único del evento GPS raw. |
| gps_device_id | integer | No | | Identificador del dispositivo GPS que generó el evento. |
| vehicle_id | integer | Sí | | Identificador del vehículo asociado al evento. |
| beacon_mac_address | character varying(17) | Sí | | Dirección MAC del beacon asociado al evento. |
| latitude | numeric(10,8) | No | | Latitud del evento GPS. |
| longitude | numeric(11,8) | No | | Longitud del evento GPS. |
| altitude | numeric(8,2) | Sí | | Altitud del evento GPS. |
| speed_kmh | numeric(5,2) | Sí | | Velocidad del vehículo en km/h. |
| heading | numeric(5,2) | Sí | | Dirección del movimiento del vehículo en grados. |
| accuracy_meters | numeric(6,2) | Sí | | Precisión del evento GPS en metros. |
| satellites | integer | Sí | | Número de satélites utilizados para el evento GPS. |
| gps_timestamp | timestamp with time zone | No | | Timestamp del evento GPS. |
| server_timestamp | timestamp with time zone | Sí | now() | Timestamp del servidor cuando se recopiló el evento. |
| battery_level | integer | Sí | | Nivel de batería del dispositivo GPS. |
| raw_data | character varying | Sí | | Datos raw del evento GPS. |
| created_at | timestamp with time zone | Sí | now() | Timestamp cuando se creó el registro. |

**Clave primaria:** raw_event_id, gps_timestamp

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- chk_gps_raw_accuracy: Verifica que la precisión del evento GPS sea mayor que 0 o nula.
- chk_gps_raw_battery: Verifica que el nivel de batería esté entre 0 y 100 o sea nulo.
- chk_gps_raw_heading: Verifica que la dirección del movimiento esté entre 0 y 360 o sea nula.
- chk_gps_raw_latitude: Verifica que la latitud esté entre -90 y 90.
- chk_gps_raw_longitude: Verifica que la longitud esté entre -180 y 180.
- chk_gps_raw_satellites: Verifica que el número de satélites sea mayor o igual a 0 o sea nulo.
- chk_gps_raw_speed: Verifica que la velocidad esté entre 0 y 250 o sea nula.

**Triggers:** No se especifican triggers en el SQL proporcionado.

**Observaciones:** 
- La tabla incluye restricciones de validación para asegurar que los valores de las columnas estén dentro de rangos razonables.
- Se crean índices para mejorar el rendimiento de consultas frecuentes, especialmente por `gps_device_id`, `vehicle_id` y `gps_timestamp`.
