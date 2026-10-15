## api.deactivate_route
**Proposito:** Desactiva una ruta y todas sus paradas asociadas, registrando el cambio en el log de actividades.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.deactivate_route_input | Objeto de entrada que contiene los parámetros necesarios para desactivar la ruta. |

**Retorna:** api.deactivate_route_result
**Tablas que lee:** core_operations.route, core_operations.route_stop, identity."user"
**Tablas que modifica (INSERT/UPDATE/DELETE):** core_operations.route, core_operations.route_stop, identity.activity_log
**Funciones que invoca:** Por confirmar
**Logica paso a paso:**
1. Valida que el `route_id` no sea nulo.
2. Valida que la ruta exista en la base de datos.
3. Valida que el `deactivated_by` sea un usuario activo si se proporciona.
4. Si la ruta ya está inactiva, devuelve un aviso sin realizar cambios.
5. Desactiva la ruta y todas sus paradas activas.
6. Construye un snapshot JSONB con los cambios realizados.
7. Registra el cambio en el log de actividades.
8. Devuelve los detalles de la ruta desactivada y el log de actividad.
**Errores y excepciones:** 
- `MISSING_ROUTE_ID`: El `route_id` es obligatorio.
- `ROUTE_NOT_FOUND`: La ruta no existe.
- `USER_NOT_FOUND`: El usuario indicado en `deactivated_by` no existe o está inactivo.
- `INTERNAL_ERROR`: Error interno inesperado.
**Observaciones:** La función es segura para definir (`SECURITY DEFINER`). No se utiliza SQL dinámico.
