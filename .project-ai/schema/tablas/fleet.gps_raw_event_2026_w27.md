## fleet.gps_raw_event_2026_w27
**Tipo:** tabla
**Proposito:** Almacena eventos de GPS raw para el año 2026, semana 27.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| raw_event_id | bigint | No | nextval('fleet.gps_raw_event_raw_event_id_seq'::regclass) | Identificador único del evento raw |
| gps_device_id | integer | No | Por confirmar | Identificador del dispositivo GPS |
| vehicle_id | integer | Sí | Por confirmar | Identificador del vehículo |
| beacon_mac_address | character varying(17) | Sí | Por confirmar | Dirección MAC del beacon |
| latitude | numeric(10,8) | No | Por confirmar | Latitud del evento GPS |
| longitude | numeric(11,8) | No | Por confirmar | Longitud del evento GPS |
| altitude | numeric(8,2) | Sí | Por confirmar | Altitud del evento GPS |
| speed_kmh | numeric(5,2) | Sí | Por confirmar | Velocidad en km/h |
| heading | numeric(5,2) | Sí | Por confirmar | Dirección del evento GPS |
| accuracy_meters | numeric(6,2) | Sí | Por confirmar | Precisión del evento GPS |
| satellites | integer | Sí | Por confirmar | Número de satélites utilizados |
| gps_timestamp | timestamp with time zone | No | Por confirmar | Timestamp del evento GPS |
| server_timestamp | timestamp with time zone | Sí | now() | Timestamp del servidor cuando se registró el evento |
| battery_level | integer | Sí | Por confirmar | Nivel de batería del dispositivo GPS |
| raw_data | character varying | Sí | Por confirmar | Datos raw del evento GPS |
| created_at | timestamp with time zone | Sí | now() | Timestamp cuando se creó el registro |

**Clave primaria:** raw_event_id, gps_timestamp

**Claves foraneas:** Ninguna

**Indices y restricciones:**
- chk_gps_raw_accuracy: Verifica que la precisión esté mayor que 50 metros
- chk_gps_raw_battery: Verifica que el nivel de batería esté entre 0 y 100
- chk_gps_raw_heading: Verifica que la dirección esté entre 0 y 360 grados
- chk_gps_raw_latitude: Verifica que la latitud esté entre -90 y 90 grados
- chk_gps_raw_longitude: Verifica que la longitud esté entre -180 y 180 grados
- chk_gps_raw_satellites: Verifica que el número de satélites sea mayor o igual a 0
- chk_gps_raw_speed: Verifica que la velocidad esté entre 0 y 250 km/h

**Triggers:** Ninguno

**Observaciones:** 
- La tabla incluye restricciones de verificación para asegurar que los valores de ciertas columnas estén dentro de un rango válido.
- Se crean índices en varias columnas para mejorar el rendimiento de consultas que filtran o ordenan por estas columnas.
