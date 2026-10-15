## api.sync_permission_templates
**Proposito:** Sincroniza las plantillas de permisos en la base de datos, insertando, actualizando y eliminando según los datos proporcionados en el input.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.sync_permission_templates_input | Objeto que contiene el array de plantillas a sincronizar |

**Retorna:** api.sync_permission_templates_result
**Tablas que lee:** identity.permission_template, identity.permission_template_detail, identity.permission
**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.permission_template, identity.permission_template_detail
**Funciones que invoca:** No invoca ninguna función externa.
**Logica paso a paso:** 
1. Valida que el array de plantillas no sea NULL.
2. Recorre cada plantilla en el array.
3. Valida duplicidades de `template_id` y `name` en el batch.
4. Valida que el `role_type` sea válido si se proporciona.
5. Valida que todos los `permission_ids` existan y estén activos.
6. Para cada plantilla, verifica si es una inserción o una actualización.
7. Sincroniza los detalles de la plantilla, insertando nuevos permisos, eliminando ausentes y marcando los existentes como 'KEPT'.
8. Registra el resultado de cada plantilla en el array de resultados.
9. Devuelve el resultado global con estadísticas de inserciones, actualizaciones, errores, etc.
**Errores y excepciones:** 
- `NULL_TEMPLATES_ARRAY`: El array de plantillas es NULL.
- `DUPLICATE_TEMPLATE_ID_IN_BATCH`: `template_id` aparece más de una vez en el lote.
- `MISSING_TEMPLATE_NAME`: `name` es obligatorio al crear una plantilla.
- `DUPLICATE_NAME_IN_BATCH`: `name` aparece más de una vez en el lote.
- `DUPLICATE_TEMPLATE_NAME`: Ya existe una plantilla con el mismo `name`.
- `INVALID_ROLE_TYPE`: `role_type` inválido.
- `INVALID_PERMISSION_IDS`: `permission_ids` contiene uno o más ids que no existen.
- `DUPLICATE_PERMISSION_IDS`: `permission_ids` contiene valores duplicados.
- `TEMPLATE_NOT_FOUND`: `template_id` no existe.
- `INTERNAL_ERROR`: Error interno inesperado.
**Observaciones:** La función es segura para la definición del usuario (`SECURITY DEFINER`). No utiliza SQL dinámico.
