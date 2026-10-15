## api.get_permissions
**Proposito:** Obtiene los permisos según los filtros proporcionados, como activos, módulos, recursos y acciones.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_permissions_input | Objeto de entrada con filtros para los permisos. |

**Retorna:** Un objeto `api.get_permissions_result` que contiene los permisos filtrados y detalles del filtro aplicado.

**Tablas que lee:** `identity.permission`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Normaliza los filtros proporcionados.
2. Valida los módulos si se proporcionan.
3. Realiza una consulta a la tabla `identity.permission` para obtener los permisos que coinciden con los filtros.
4. Construye el resultado con los permisos filtrados y detalles del filtro aplicado.

**Errores y excepciones:** 
- `INVALID_MODULE`: Si algún módulo proporcionado no es válido.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función. No utiliza SQL dinámico.
