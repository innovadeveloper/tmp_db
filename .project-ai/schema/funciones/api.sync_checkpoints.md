## api.sync_checkpoints
**Proposito:** Sincroniza los puntos de control (checkpoints) para una ruta específica, realizando inserciones, actualizaciones y eliminaciones según los datos proporcionados.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.sync_checkpoints_input | Objeto de entrada que contiene la ruta y los puntos de control a sincronizar. |

**Retorna:** api.sync_checkpoints_result
**Tablas que lee:** core_operations.route, core_operations.checkpoint, core_operations.route_control, core_operations.trip_stop
**Tablas que modifica (INSERT/UPDATE/DELETE):** core_operations.checkpoint
**Funciones que invoca:** No invoca funciones externas.
**Logica paso a paso:** 
1. Valida que la ruta exista y esté activa.
2. Valida que el array de puntos de control no sea NULL.
3. Valida el conteo de puntos de control por dirección.
4. Realiza un bucle para procesar cada punto de control:
   - Valida los campos obligatorios y sus rangos.
   - Busca el punto de control existente o lo inserta si no existe.
   - Realiza la actualización o inserción según sea necesario.
5. Elimina los puntos de control que no están en el payload.
6. Genera el resultado global con los detalles de la operación.
**Errores y excepciones:** 
- RAISE para errores internos.
- Valida errores específicos como puntos de control duplicados, coordenadas fuera de rango, etc.
**Observaciones:** 
- La función es de tipo SECURITY DEFINER, lo que significa que ejecuta con los privilegios del propietario de la función.
- La función utiliza SQL dinámico para manejar los errores y retornar detalles detallados.
