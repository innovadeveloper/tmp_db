## api.set_vehicle_ownership_share
**Proposito:** Actualiza o inserta la participación de un propietario en un vehículo, validando la existencia del vehículo y del propietario, el rango del porcentaje, la coherencia de las fechas y el solapamiento de períodos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.set_vehicle_ownership_share_input | Objeto de entrada con los datos de la participación del propietario en el vehículo. |

**Retorna:** api.set_vehicle_ownership_share_result
**Tablas que lee:** fleet.vehicle, fleet.vehicle_owner, fleet.vehicle_owner_share
**Tablas que modifica (INSERT/UPDATE/DELETE):** fleet.vehicle_owner_share
**Funciones que invoca:** Por confirmar
**Logica paso a paso:** 
1. Valida la existencia del vehículo.
2. Valida la existencia y estado del propietario.
3. Valida el rango del porcentaje de participación.
4. Valida la fecha de inicio.
5. Valida la coherencia de las fechas.
6. Valida el solapamiento de períodos para el mismo propietario.
7. Valida que la suma de porcentajes no supere el 100%.
8. Realiza un UPSERT en la tabla fleet.vehicle_owner_share.
9. Calcula el total final de porcentajes.
10. Llena el resultado con los datos de la participación actualizada o insertada.

**Errores y excepciones:** 
- RAISE check_violation: Si ocurre una violación de constraint en la tabla fleet.vehicle_owner_share.
- RAISE OTHERS: Para cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza un bloque EXCEPTION para manejar errores y devolver un resultado adecuado.
- La función es definida con SECURITY DEFINER, lo que permite que cualquier usuario que la invoque tenga los mismos privilegios que el propietario de la función.
