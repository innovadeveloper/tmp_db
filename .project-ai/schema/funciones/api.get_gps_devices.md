## api.get_gps_devices
**Proposito:** Función que devuelve una lista paginada de dispositivos GPS, incluyendo información del vehículo vinculado cuando está disponible. Permite filtrar por estado, tipo de dispositivo, compañía, operatividad y si tienen vehículo asociado.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_gps_devices_input | Objeto de entrada que contiene los filtros y configuración de la paginación. |

**Retorna:** Un objeto `api.get_gps_devices_result` que contiene la lista de dispositivos GPS, indicadores de paginación y mensajes de error.

**Tablas que lee:** `fleet.gps_device` y `fleet.vehicle`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida los parámetros de entrada (`status`, `device_type`, `page_size`).
2. Realiza una consulta SQL para obtener los dispositivos GPS filtrados y ordenados por `gps_device_id`.
3. Aplica la paginación, ajustando el tamaño de la página y detectando si hay una página siguiente.
4. Asigna los resultados a la estructura de salida `api.get_gps_devices_result`.
5. Maneja excepciones y errores, asignando mensajes de error y estableciendo el estado de éxito en `FALSE`.

**Errores y excepciones:** 
- `INVALID_STATUS`: Si el estado proporcionado no es válido.
- `INVALID_DEVICE_TYPE`: Si el tipo de dispositivo proporcionado no es válido.
- `INVALID_PAGE_SIZE`: Si el tamaño de la página no está entre 1 y 200.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza un cursor keyset sobre `gps_device_id` para una paginación eficiente.
- Los filtros son aplicados de manera segura y cortocircuitada.
- La función maneja correctamente los casos en los que no hay resultados o cuando el tamaño de la página es 0.
- La seguridad de la función se asegura mediante el uso de `STABLE` y la gestión de excepciones.
