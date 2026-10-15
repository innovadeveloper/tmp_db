## api.ingest_gps_raw_event
**Proposito:** Procesa un evento GPS crudo y lo ingiere en la base de datos, validando los datos y actualizando el estado del dispositivo.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.ingest_gps_raw_event_input | Objeto de entrada con los datos del evento GPS |

**Retorna:** api.ingest_gps_raw_event_result
**Tablas que lee:** fleet.gps_device, fleet.gps_raw_event
**Tablas que modifica (INSERT/UPDATE/DELETE):** fleet.gps_raw_event, fleet.gps_device
**Funciones que invoca:** Por confirmar
**Logica paso a paso:**
1. Inicializa los flags de resultado.
2. Valida los campos obligatorios: device_id, latitude, longitude, gps_timestamp.
3. Valida los rangos de coordenadas, velocidad, encabezado y nivel de batería.
4. Rechaza eventos con timestamps en el futuro.
5. Descarta eventos con timestamps demasiado antiguos.
6. Resuelve el dispositivo GPS por device_id.
7. Inserta el evento en fleet.gps_raw_event.
8. Actualiza el heartbeat del dispositivo.
9. Pobla y retorna el resultado.
**Errores y excepciones:** 
- check_violation: Violación de constraint en gps_raw_event.
- Otros errores: Error interno.
**Observaciones:** 
- La función es de seguridad definida (SECURITY DEFINER).
- La evaluación de alertas se delega a api.evaluate_gps_alerts del Grupo G, invocada de forma asíncrona.
