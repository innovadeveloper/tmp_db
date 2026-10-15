## utilities.get_user_permission
**Proposito:** Obtiene los permisos de un usuario para un código específico.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_user_id | integer | ID del usuario para el cual se obtienen los permisos. |
| p_code | text | Código del permiso que se busca. |

**Retorna:** Una tabla con los siguientes campos:
- `code`: Código del permiso.
- `company_id`: ID de la compañía asociada al permiso.
- `scope_id`: ID del ámbito asociado al permiso.
- `rol`: Nombre del rol que tiene el usuario para el permiso.

**Tablas que lee:** 
- `identity.user_role`
- `identity.role_permission`
- `identity.permission`
- `identity.role`
- `identity.role_permission_scope`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función.

**Logica paso a paso:**
1. Filtra los registros de `identity.user_role` donde el `user_id` coincide con `p_user_id`.
2. Filtra los registros de `identity.role_permission` donde el `permission_id` coincide con el `permission_id` del permiso cuyo código es `p_code`.
3. Realiza un `JOIN` entre `identity.role_permission` y `identity.permission` para obtener el código del permiso.
4. Realiza un `JOIN` entre `identity.user_role` y `identity.role` para obtener el nombre del rol.
5. Realiza un `LEFT JOIN` entre `identity.role_permission` y `identity.role_permission_scope` para obtener el `company_id` y `scope_id` asociados al permiso.
6. Devuelve los resultados filtrados y seleccionados.

**Errores y excepciones:** No se especifican excepciones en el código.

**Observaciones:** La función no realiza ninguna operación que pueda tener riesgos de seguridad o rendimiento significativo. No utiliza `SECURITY DEFINER` ni SQL dinámico.
