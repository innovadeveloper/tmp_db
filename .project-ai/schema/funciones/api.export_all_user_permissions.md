## api.export_all_user_permissions
**Proposito:** Exporta todas las permisiones de los usuarios activos, incluyendo los permisos por compañía.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| Ninguno |

**Retorna:** Un objeto JSONB que contiene las permisiones de cada usuario activo, organizadas por compañía.

**Tablas que lee:** 
- `identity."user"`
- `identity.user_tenant_access`
- `identity.user_role`
- `identity.role_permission`
- `identity.permission`
- `identity.role_permission_scope`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna.

**Funciones que invoca:** Ninguna.

**Logica paso a paso:**
1. Selecciona todos los usuarios activos y sus compañías asociadas.
2. Para cada usuario, recopila sus permisos activos y los agrupa por compañía.
3. Construye un objeto JSONB para cada usuario con sus permisos y compañías.
4. Combina todos los objetos JSONB en un solo objeto JSONB y lo retorna.

**Errores y excepciones:** 
- No se manejan excepciones específicas en el código proporcionado.

**Observaciones:** 
- La función es segura para definir (`SECURITY DEFINER`), lo que significa que puede ejecutarse con privilegios de usuario más altos.
- La función utiliza SQL dinámico para construir consultas internas, lo que puede afectar el rendimiento si no se optimiza adecuadamente.
