## api.get_roles
**Proposito:** Obtiene una lista de roles para un tenant específico, aplicando filtros opcionales como activos, nombre de búsqueda y módulo de permiso.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_roles_input_v2 | Objeto de entrada que contiene los parámetros de filtro y configuración. |

**Retorna:** Un objeto `api.get_roles_result_v2` que contiene la lista de roles filtrados y los detalles de la consulta.

**Tablas que lee:** `identity.tenant`, `identity.role`, `identity.role_permission`, `identity.permission`, `identity.role_permission_scope`, `identity.scope_type`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que el `tenant_id` esté presente y exista en la tabla `identity.tenant`.
2. Normaliza los filtros proporcionados: `is_active`, `name_search`, `permission_module`, y `include_empty_roles`.
3. Valida el `permission_module` si se proporciona.
4. Utiliza CTEs anidados para filtrar roles, obtener sus permisos y scopes, y agrupar los resultados.
5. Construye la respuesta final en un array de objetos `api.role_list_item_v2`.

**Errores y excepciones:** 
- `MISSING_TENANT_ID`: Si el `tenant_id` no se proporciona.
- `TENANT_NOT_FOUND`: Si el `tenant_id` no existe.
- `INVALID_PERMISSION_MODULE`: Si el `permission_module` proporcionado no es válido.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza CTEs para optimizar el rendimiento al minimizar el número de escaneos de la base de datos.
- La función maneja errores y devuelve un objeto de resultado con detalles del error si ocurren excepciones.
