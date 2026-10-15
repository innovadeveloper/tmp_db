## api.sync_role_permissions
**Proposito:** Sincroniza los permisos asignados a un rol, insertando, actualizando y desactivando según los permisos proporcionados en el payload.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.sync_role_permissions_input | Objeto de entrada que contiene el role_id y el array de permisos a sincronizar. |

**Retorna:** api.sync_role_permissions_result
**Tablas que lee:** identity.role, identity.permission, identity.role_permission
**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.role_permission
**Funciones que invoca:** Por confirmar
**Logica paso a paso:** 
1. Valida que el role_id no sea NULL.
2. Valida que el rol exista y esté activo.
3. Valida que el array de permisos no sea NULL.
4. Upsert cada permiso en el array:
   - Valida que el permission_id no sea NULL.
   - Valida que el permission_id no sea duplicado en el batch.
   - Valida que el permiso exista en el catálogo y esté activo.
   - Si el permiso ya existe, actualiza el is_active solo si cambia.
   - Si el permiso no existe, lo inserta.
5. Desactiva los permisos activos que no están en el payload.
**Errores y excepciones:** 
- RAISE en caso de error interno.
- Valida que el role_id no sea NULL.
- Valida que el rol exista y esté activo.
- Valida que el array de permisos no sea NULL.
- Valida que el permission_id no sea NULL.
- Valida que el permission_id no sea duplicado en el batch.
- Valida que el permiso exista en el catálogo y esté activo.
**Observaciones:** 
- La función es de tipo SECURITY DEFINER, lo que significa que se ejecuta con los privilegios del usuario que la invoca.
- La función utiliza SQL dinámico para construir y ejecutar consultas SQL.
