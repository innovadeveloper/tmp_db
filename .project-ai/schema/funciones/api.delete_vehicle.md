## api.delete_vehicle
**Proposito:** Elimina un vehículo de la base de datos utilizando su número de placa y devuelve un resultado que indica si la operación fue exitosa o no.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_plate_number | character varying | Número de placa del vehículo a eliminar |

**Retorna:** `api.delete_vehicle_result` - Un objeto que contiene el resultado de la operación, incluyendo el éxito, el código de error, el mensaje de error y el número de placa del vehículo eliminado.

**Tablas que lee:** `fleet.vehicle` - La tabla de vehículos de la flota.

**Tablas que modifica (INSERT/UPDATE/DELETE):** `fleet.vehicle` - Se realiza una operación DELETE en esta tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Inicializa el resultado con `success` como `true` y `error_code` y `error_message` como `NULL`.
2. Intenta eliminar el vehículo con el número de placa proporcionado.
3. Si el vehículo no existe, lanza una excepción con el código de error `P0002` y el mensaje 'Vehículo con placa % no existe'.
4. Si el vehículo se elimina correctamente, almacena el número de placa en `v_deleted_plate`.
5. Devuelve el resultado con el número de placa del vehículo eliminado.

**Errores y excepciones:** 
- `WHEN OTHERS THEN`: Cualquier otro error que no se capture anteriormente lanza una excepción con el código de error `SQLSTATE` y el mensaje de error `SQLERRM`.

**Observaciones:** La función utiliza `RAISE EXCEPTION` para manejar errores específicos, lo que permite un control más preciso del flujo de la operación. La función no utiliza `SECURITY DEFINER` y no contiene SQL dinámico, por lo que no presenta riesgos adicionales en términos de seguridad o rendimiento.
