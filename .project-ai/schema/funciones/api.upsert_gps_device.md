## api.upsert_gps_device
**Proposito:** Inserta o actualiza un dispositivo GPS en la base de datos, validando los datos y gestionando las relaciones con vehículos y compañías.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_gps_device_input | Objeto de entrada con los datos del dispositivo GPS a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_gps_device_result` que indica el éxito o fracaso de la operación, el estado del dispositivo y los detalles del dispositivo.

**Tablas que lee:** 
- `fleet.gps_device`
- `fleet.vehicle`
- `shared.company`
- `identity."user"`

**Tablas que modifica (INSERT/UPDATE/DELETE):** 
- `fleet.gps_device`

**Funciones que invoca:** 
- `NOTA`: No se invocan funciones externas en este código.

**Logica paso a paso:** 
1. Si `gps_device_id` es `NULL`, se intenta insertar un nuevo dispositivo.
2. Si `gps_device_id` no es `NULL`, se intenta actualizar un dispositivo existente.
3. Se realizan validaciones de unicidad para `device_id` y `imei`.
4. Se validan los tipos de dispositivo y el estado.
5. Se gestionan los cambios en el `vehicle_id`, asegurando que el vehículo no tenga otro GPS activo.
6. Se actualizan o insertan los datos del dispositivo según la operación.
7. Se devuelven los detalles del dispositivo actualizado o insertado.

**Errores y excepciones:** 
- `unique_violation`: Conflicto de unicidad por concurrencia (device_id o IMEI duplicado).
- `check_violation`: Violación de constraint en `gps_device`.
- `OTHERS`: Cualquier otro error interno.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para permitir operaciones que requieren privilegios adicionales.
- La función maneja transacciones implícitas para asegurar la consistencia de los datos.
- La función utiliza `RAISE` para manejar errores y devolver mensajes de error descriptivos.
