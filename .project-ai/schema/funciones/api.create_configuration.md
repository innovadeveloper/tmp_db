## api.create_configuration
**Proposito:** Crea o actualiza una configuración en la base de datos, dependiendo si la clave ya existe. Si la clave existe y `allow_update` es `FALSE`, la operación fallará. Si la clave existe y `allow_update` es `TRUE`, la configuración se actualizará. Si la clave no existe, se insertará una nueva configuración.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.create_configuration_input | Objeto de entrada que contiene la configuración a crear o actualizar. |

**Retorna:** Un objeto `api.create_configuration_result` que indica el éxito o el fracaso de la operación, el código de error, el mensaje de error, la operación realizada (INSERTED o UPDATED), y los detalles de la configuración.

**Tablas que lee:** `shared.configuration`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `shared.configuration`

**Funciones que invoca:** `RAISE`

**Logica paso a paso:**
1. Valida el `data_type` proporcionado. Debe ser uno de 'STRING', 'INTEGER', 'BOOLEAN', 'JSON', o 'DECIMAL'.
2. Valida que el valor proporcionado sea compatible con el `data_type` declarado.
3. Verifica si la clave ya existe en la tabla `shared.configuration`.
4. Si la clave existe:
   - Si `allow_update` es `FALSE`, la operación falla.
   - Si `allow_update` es `TRUE` y la configuración es editable, se actualiza la configuración.
5. Si la clave no existe, se inserta una nueva configuración.
6. Devuelve el resultado de la operación.

**Errores y excepciones:**
- `UNKNOWN_DATA_TYPE`: El `data_type` proporcionado no es válido.
- `INVALID_DATA_TYPE_VALUE`: El valor proporcionado no es compatible con el `data_type`.
- `DUPLICATE_CONFIG_KEY`: La clave ya existe y `allow_update` es `FALSE`.
- `CONFIG_NOT_EDITABLE`: La configuración es editable y no puede ser modificada.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función utiliza `RAISE` para manejar errores. La operación es sensible a la seguridad, ya que puede modificar o insertar datos en la tabla `shared.configuration`.
