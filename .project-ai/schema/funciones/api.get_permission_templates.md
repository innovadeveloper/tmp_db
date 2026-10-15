## api.get_permission_templates
**Proposito:** Obtiene una lista de plantillas de permisos con sus detalles, aplicando filtros de actividad, tipo de rol y nombre.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_permission_templates_input | Objeto de entrada que contiene los filtros para la consulta. Por defecto, filtra solo las plantillas activas. |

**Retorna:** Un objeto `api.get_permission_templates_result` que contiene la lista de plantillas de permisos, los filtros aplicados y el total de resultados.

**Tablas que lee:** `identity.permission_template`, `identity.permission_template_detail`, `identity.permission`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** `NULL`

**Logica paso a paso:**
1. Normaliza los filtros de entrada (`is_active`, `role_type`, `name_search`).
2. Valida los tipos de rol proporcionados.
3. Filtra las plantillas de permisos según los filtros.
4. Agrupa los permisos por plantilla en un solo escaneo.
5. Construye el resultado final con los detalles de las plantillas y sus permisos.

**Errores y excepciones:** 
- `INVALID_ROLE_TYPE`: Se lanza si algún tipo de rol proporcionado no es válido.
- `INTERNAL_ERROR`: Se lanza en caso de cualquier otro error inesperado.

**Observaciones:** 
- La función utiliza una consulta con CTEs (Common Table Expressions) para optimizar el rendimiento al filtrar y agrupar los datos en dos pasos.
- La función no modifica ninguna tabla, solo realiza consultas de lectura.
- La función utiliza `COALESCE` y `NULLIF` para manejar valores nulos y vacíos de manera segura.
