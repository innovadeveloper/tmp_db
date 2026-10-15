## core_operations.trip_stop
**Tipo:** tabla  
**Proposito:** Almacena información sobre los puntos de parada de los viajes, incluyendo detalles sobre el horario programado y real, demoras, y pasajeros que suben y bajan.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| trip_stop_id | bigint | No | nextval('core_operations.trip_stop_trip_stop_id_seq'::regclass) | Identificador único de la parada de viaje. |
| trip_id | bigint | No | Por confirmar | Identificador del viaje al que pertenece la parada. |
| scheduled_arrival_time | timestamp with time zone | Sí | Por confirmar | Hora programada de llegada al punto de parada. |
| actual_arrival_time | timestamp with time zone | Sí | Por confirmar | Hora real de llegada al punto de parada. |
| arrival_delay_seconds | integer | Sí | Por confirmar | Demora en segundos entre el horario programado y la llegada real. |
| scheduled_departure_time | timestamp with time zone | Sí | Por confirmar | Hora programada de salida del punto de parada. |
| actual_departure_time | timestamp with time zone | Sí | Por confirmar | Hora real de salida del punto de parada. |
| compliance_status | character varying(20) | Sí | Por confirmar | Estado de cumplimiento del viaje en el punto de parada (ON_TIME, EARLY, LATE, MISSED). |
| passengers_boarding | integer | Sí | Por confirmar | Número de pasajeros que suben en el punto de parada. |
| passengers_alighting | integer | Sí | Por confirmar | Número de pasajeros que bajan en el punto de parada. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro. |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización del registro. |
| checkpoint_id | integer | No | Por confirmar | Identificador del punto de control asociado con la parada. |

**Clave primaria:** trip_stop_id  
**Claves foraneas:** checkpoint_id -> core_operations.checkpoint.checkpoint_id  
**Indices y restricciones:**  
- chk_trip_stop_compliance: Comprueba que el estado de cumplimiento esté en el conjunto permitido (ON_TIME, EARLY, LATE, MISSED).  
- idx_trip_stop_checkpoint_id: Índice B-tree en checkpoint_id.  
- idx_trip_stop_trip_id: Índice B-tree en trip_id.  
**Triggers:** Ninguno  
**Observaciones:** Ninguna
