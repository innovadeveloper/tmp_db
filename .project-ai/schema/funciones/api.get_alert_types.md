## api.get_alert_types
**Proposito:** La función `api.get_alert_types` devuelve una lista de tipos de alertas, filtrada opcionalmente por categoría y estado de actividad.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_only_active | boolean | Indica si solo se deben devolver los tipos de alerta activos. El valor por defecto es `true`. |
| p_category | character varying | Filtra los tipos de alerta por categoría. Las categorías válidas son 'TRACKER', 'PANIC', 'VEHICLE', 'DISPATCH', 'DRIVER', 'SYSTEM'. Si no se proporciona, no se aplica ningún filtro por categoría. |

**Retorna:** Un objeto `api.get_alert_types_result` que contiene la lista de tipos de alerta, el total de elementos, y información de éxito o error.

**Tablas que lee:** `core_operations.alert_type`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida si la categoría proporcionada es válida. Si no lo es, devuelve un error.
2. Realiza una consulta para obtener los tipos de alerta filtrados por la categoría y el estado de actividad.
3. Normaliza el resultado en caso de que no haya filas.
4. Devuelve el resultado en un objeto `api.get_alert_types_result`.

**Errores y excepciones:** 
- `INVALID_CATEGORY`: Se lanza si la categoría proporcionada no es válida.
- `INTERNAL_ERROR`: Se lanza en caso de cualquier otro error inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para permitir el acceso a usuarios con privilegios elevados. No utiliza SQL dinámico.
