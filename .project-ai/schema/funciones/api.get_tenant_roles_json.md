## api.get_tenant_roles_json
**Proposito:** Obtiene los roles y permisos asociados a un inquilino específico en formato JSON.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_tenant_id | integer | Identificador del inquilino para el cual se obtienen los roles y permisos |

**Retorna:** Un objeto JSONB que contiene la información del inquilino, sus roles, los permisos asociados a cada rol, y los usuarios y roles de los usuarios.

**Tablas que lee:** 
- identity.tenant
- identity.role
- identity.role_permission
- identity.permission
- identity."user"
- identity.user_role

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:** 
1. Verifica si el inquilino existe en la tabla identity.tenant.
2. Recupera los roles asociados al inquilino desde la tabla identity.role.
3. Para cada rol, recupera los permisos asociados desde la tabla identity.role_permission y identity.permission.
4. Construye un objeto JSONB con la información del inquilino, sus roles, los permisos de cada rol, y los usuarios y roles de los usuarios.

**Errores y excepciones:** 
- Si el inquilino no existe, lanza una excepción con el código de error 'P0002' y el mensaje 'Tenant no encontrado'.

**Observaciones:** 
- La función utiliza 'SECURITY DEFINER' para ejecutar con los privilegios del propietario de la función.
- La función utiliza SQL dinámico para construir la respuesta JSON.
