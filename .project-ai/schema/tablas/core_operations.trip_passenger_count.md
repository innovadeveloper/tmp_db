## core_operations.trip_passenger_count
**Tipo:** tabla  
**Proposito:** Almacena información sobre el conteo de pasajeros en cada parada durante un viaje.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| passenger_count_id | bigint | No | nextval('core_operations.trip_passenger_count_passenger_count_id_seq'::regclass) | Identificador único del conteo de pasajeros. |
| trip_id | bigint | No | Ninguna | Identificador del viaje al que pertenece el conteo de pasajeros. |
| stop_id | integer | Sí | Ninguna | Identificador de la parada donde se realiza el conteo de pasajeros. |
| count_timestamp | timestamp with time zone | No | now() | Fecha y hora exacta en que se realiza el conteo de pasajeros. |
| boarding_count | integer | No | 0 | Cantidad de pasajeros que suben al vehículo. |
| alighting_count | integer | No | 0 | Cantidad de pasajeros que bajan del vehículo. |
| current_load | integer | No | 0 | Cantidad actual de pasajeros en el vehículo. |
| detection_method | character varying(20) | Sí | Ninguna | Método utilizado para detectar el conteo de pasajeros. |
| created_at | timestamp with time zone | No | now() | Fecha y hora en que se crea el registro del conteo de pasajeros. |

**Clave primaria:** passenger_count_id  
**Claves foraneas:** Ninguna  
**Indices y restricciones:** Ninguna  
**Triggers:** Ninguno  
**Observaciones:** La tabla no tiene restricciones de integridad referencial, lo que significa que no se asegura que los valores de `trip_id` y `stop_id` correspondan a registros existentes en otras tablas.
