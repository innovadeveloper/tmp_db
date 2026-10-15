## api.get_people
**Proposito:** Obtiene una lista paginada de personas filtradas por tenant, estado de activación y búsqueda.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| tenant_id | BIGINT | Identificador del tenant para el cual se filtran las personas. Obligatorio. |
| page_number | INT | Número de página a devolver. Por defecto 1. |
| page_size | INT | Tamaño de la página. Por defecto 20, con un máximo de 100. |
| search | TEXT | Cadena de búsqueda para filtrar personas por nombre completo, tax_id o username. |
| is_active | BOOLEAN | Estado de activación de las personas a filtrar. Opcional. |

**Retorna:** Un objeto `api.get_people_result` que contiene la lista de personas, metadatos de paginación y información de error.

**Tablas que lee:** `identity.tenant`, `identity.user`, `identity.user_tenant_access`, `hr.personnel`, `hr.driver`, `hr.person`, `identity.user_role`, `identity.role`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna.

**Funciones que invoca:** `NULLIF`, `TRIM`, `COALESCE`, `GREATEST`, `LEAST`, `CEIL`, `STRING_AGG`.

**Logica paso a paso:**
1. Normaliza los parámetros de entrada.
2. Valida que `tenant_id` no sea nulo y que exista en la tabla `identity.tenant`.
3. Construye una consulta principal (`base`) que filtra personas según los criterios de tenant, estado de activación y búsqueda.
4. Cuenta el total de registros que cumplen con los criterios.
5. Aplica la paginación a los resultados.
6. Formatea los resultados para devolverlos en el formato `api.person_row`.
7. Calcula los metadatos de paginación.
8. Devuelve el resultado en un objeto `api.get_people_result`.

**Errores y excepciones:** 
- `MISSING_TENANT_ID`: Si `tenant_id` es nulo.
- `TENANT_NOT_FOUND`: Si el `tenant_id` no existe en la tabla `identity.tenant`.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función. No utiliza SQL dinámico.
