## fleet.gps_raw_event_2026_w28
**Tipo:** tabla
**Proposito:** Almacena eventos de GPS brutos recopilados por dispositivos GPS en una semana específica.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| raw_event_id | bigint | No | nextval('fleet.gps_raw_event_raw_event_id_seq'::regclass) | Identificador único del evento GPS |
| gps_device_id | integer | No | Por confirmar | Identificador del dispositivo GPS que generó el evento |
| vehicle_id | integer | Sí | Por confirmar | Identificador del vehículo asociado al evento (si está disponible) |
| beacon_mac_address | character varying(17) | Sí | Por confirmar | Dirección MAC del beacon asociado al evento (si está disponible) |
| latitude | numeric(10,8) | No | Por confirmar | Latitud del evento GPS |
| longitude | numeric(11,8) | No | Por confirmar | Longitud del evento GPS |
| altitude | numeric(8,2) | Sí | Por confirmar | Altitud del evento GPS (si está disponible) |
| speed_kmh | numeric(5,2) | Sí | Por confirmar | Velocidad del vehículo en km/h (si está disponible) |
| heading | numeric(5,2) | Sí | Por confirmar | Dirección del movimiento del vehículo en grados (si está disponible) |
| accuracy_meters | numeric(6,2) | Sí | Por confirmar | Precisión del evento GPS en metros (si está disponible) |
| satellites | integer | Sí | Por confirmar | Número de satélites utilizados en el evento GPS (si está disponible) |
| gps_timestamp | timestamp with time zone | No | Por confirmar | Timestamp del evento GPS |
| server_timestamp | timestamp with time zone | Sí | now() | Timestamp del servidor cuando se recopiló el evento |
| battery_level | integer | Sí | Por confirmar | Nivel de batería del dispositivo GPS (si está disponible) |
| raw_data | character varying | Sí | Por confirmar | Datos brutos del evento GPS (si está disponible) |
| created_at | timestamp with time zone | Sí | now() | Timestamp cuando se creó el registro |

**Clave primaria:** raw_event_id, gps_timestamp

**Claves foraneas:** Ninguna

**Indices y restricciones:** 
- chk_gps_raw_accuracy: Verifica que la precisión del evento GPS sea mayor que 50 metros o nula
- chk_gps_raw_battery: Verifica que el nivel de batería esté entre 0 y 100 o sea nulo
- chk_gps_raw_heading: Verifica que la dirección esté entre 0 y 360 grados o sea nula
- chk_gps_raw_latitude: Verifica que la latitud esté entre -90 y 90 grados
- chk_gps_raw_longitude: Verifica que la longitud esté entre -180 y 180 grados
- chk_gps_raw_satellites: Verifica que el número de satélites sea mayor o igual a 0 o sea nulo
- chk_gps_raw_speed: Verifica que la velocidad esté entre 0 y 250 km/h o sea nula

**Triggers:** 
- Por confirmar (si existen)

**Observaciones:** 
- La tabla incluye restricciones de validación para asegurar la integridad de los datos.
- Se crean índices para mejorar el rendimiento de consultas frecuentes.
