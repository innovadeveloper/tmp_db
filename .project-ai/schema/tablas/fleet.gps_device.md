## fleet.gps_device
**Tipo:** tabla
**Proposito:** Almacena información sobre los dispositivos GPS utilizados para rastrear vehículos, incluyendo trackers GPS y tablets Android.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| gps_device_id | integer | No | nextval('fleet.gps_device_gps_device_id_seq'::regclass) | Identificador único del dispositivo GPS |
| device_id | character varying(50) | No | | IMEI o Android ID único del dispositivo |
| device_type | character varying(20) | No | | Tipo de dispositivo, puede ser 'TRACKER_GPS' o 'ANDROID_TABLET' |
| company_id | integer | No | | Identificador de la compañía a la que pertenece el dispositivo |
| imei | character varying(20) | Sí | | Número de IMEI del dispositivo |
| serial_number | character varying(50) | Sí | | Número de serie del dispositivo |
| model | character varying(100) | Sí | | Modelo del dispositivo |
| manufacturer | character varying(100) | Sí | | Fabricante del dispositivo |
| sim_card_number | character varying(20) | Sí | | Número de SIM card del dispositivo |
| sim_provider | character varying(50) | Sí | | Proveedor de SIM card del dispositivo |
| firmware_version | character varying(50) | Sí | | Versión del firmware del dispositivo |
| vehicle_id | integer | Sí | | Identificador del vehículo al que está instalado el dispositivo |
| posting_interval_seconds | integer | No | 30 | Intervalo de transmisión GPS en segundos |
| last_communication_at | timestamp with time zone | Sí | | Fecha y hora de la última comunicación del dispositivo |
| status | character varying(20) | No | 'ACTIVE' | Estado del dispositivo, puede ser 'ACTIVE', 'INACTIVE', 'ERROR' o 'MAINTENANCE' |
| is_operational | boolean | No | true | Indica si el dispositivo está operativo |
| installed_at | timestamp with time zone | Sí | | Fecha y hora de instalación del dispositivo |
| installed_by | bigint | Sí | | Identificador del usuario que instaló el dispositivo |
| created_at | timestamp with time zone | No | now() | Fecha y hora de creación del registro |
| updated_at | timestamp with time zone | No | now() | Fecha y hora de la última actualización del registro |

**Clave primaria:** gps_device_id

**Claves foraneas:** 
- device_id -> shared.company.company_id
- installed_by -> identity."user".user_id
- vehicle_id -> fleet.vehicle.vehicle_id

**Indices y restricciones:** 
- chk_gps_device_interval: El intervalo de transmisión debe ser mayor que 0 y menor o igual a 300 segundos.
- chk_gps_device_status: El estado del dispositivo debe ser uno de los siguientes: 'ACTIVE', 'INACTIVE', 'ERROR' o 'MAINTENANCE'.
- chk_gps_device_type: El tipo de dispositivo debe ser 'TRACKER_GPS' o 'ANDROID_TABLET'.
- gps_device_device_id_key: El device_id debe ser único.
- gps_device_imei_key: El imei debe ser único.
- gps_device_pkey: La clave primaria gps_device_id.
- idx_gps_device_company: Índice en company_id y status.
- idx_gps_device_device_id: Índice en device_id.
- idx_gps_device_last_comm: Índice en last_communication_at para dispositivos operativos.
- idx_gps_device_vehicle: Índice en vehicle_id y is_operational para dispositivos operativos.
- idx_gps_device_vehicle_unique: Índice único en vehicle_id para dispositivos operativos y con vehicle_id no nulo.

**Triggers:** No se especifican triggers en el SQL proporcionado.

**Observaciones:** 
- El campo 'vehicle_id' puede tener valores nulos, lo que indica que el dispositivo puede no estar instalado en ningún vehículo.
- El campo 'is_operational' se utiliza para filtrar índices y restricciones, lo que sugiere que la operatividad del dispositivo es un factor importante en la gestión de los datos.
