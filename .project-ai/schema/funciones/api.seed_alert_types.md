## api.seed_alert_types
**Proposito:** La función `api.seed_alert_types` se encarga de inicializar o actualizar los tipos de alertas en la base de datos. Es idempotente, lo que significa que puede ser ejecutada múltiples veces sin causar cambios adicionales en los datos existentes.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.seed_alert_types_input | Un objeto que contiene un array de objetos `api.alert_type_item` que representan los tipos de alerta a inicializar o actualizar. |

**Retorna:** Un objeto `api.seed_alert_types_result` que contiene el resultado de la operación, incluyendo el número de ítems procesados, insertados, actualizados y errores.

**Tablas que lee:** `core_operations.alert_type`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `core_operations.alert_type`

**Funciones que invoca:** `unnest`

**Logica paso a paso:**
1. Verifica si el array `items` en `p_input` está vacío. Si lo está, devuelve un resultado de error.
2. Recorre cada ítem en el array `items`.
3. Realiza varias validaciones para cada ítem:
   - `code` y `name` son obligatorios.
   - `severity` debe estar dentro del dominio permitido.
   - `category` debe estar dentro del dominio permitido si se proporciona.
   - `notification_channels` debe contener solo canales válidos.
   - `auto_close_after_min` debe ser mayor que 0 si se proporciona.
4. Realiza un `INSERT` o `UPDATE` en la tabla `core_operations.alert_type` basado en el `code` del ítem.
5. Almacena el resultado de cada operación (insertado, actualizado, omitido por error) en un array `v_item_results`.
6. Calcula el resultado global basado en el número de errores.
7. Devuelve el resultado global.

**Errores y excepciones:**
- `EMPTY_ITEMS`: El array `items` está vacío.
- `MISSING_CODE`: El campo `code` es obligatorio.
- `MISSING_NAME`: El campo `name` es obligatorio.
- `INVALID_SEVERITY`: El valor de `severity` no es válido.
- `INVALID_CATEGORY`: El valor de `category` no es válido.
- `INVALID_NOTIFICATION_CHANNEL`: Uno de los canales de notificación no es válido.
- `INVALID_AUTO_CLOSE_MIN`: El valor de `auto_close_after_min` debe ser mayor que 0.
- `DB_ERROR`: Error en la base de datos durante la operación.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** La función es idempotente debido al uso de `ON CONFLICT (code) DO UPDATE`. No se actualiza el campo `is_active` en los `UPDATE` para preservar desactivaciones manuales.
