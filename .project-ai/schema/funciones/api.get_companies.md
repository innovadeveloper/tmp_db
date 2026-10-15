## api.get_companies
**Proposito:** Obtiene una lista de empresas filtradas por tenant, estado de la empresa y estado del vínculo, con opciones de paginación y búsqueda.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_companies_input | Objeto de entrada que contiene los parámetros de filtro y paginación |

**Retorna:** Un objeto `api.get_companies_result` que contiene la lista de empresas, metadatos de paginación y información de errores.

**Tablas que lee:** 
- `identity.tenant_company`
- `shared.company`

**Tablas que modifica (INSERT/UPDATE/DELETE):** Ninguna

**Funciones que invoca:** `NULLIF`, `TRIM`, `COALESCE`, `GREATEST`, `CEIL`

**Logica paso a paso:** 
1. Normaliza los parámetros de entrada.
2. Realiza validaciones básicas, como el `tenant_id` y la existencia del tenant.
3. Construye una consulta SQL que filtra las empresas según los criterios de búsqueda y estado.
4. Aplica paginación a los resultados.
5. Prepara el resultado final, incluyendo metadatos de paginación y la lista de empresas.

**Errores y excepciones:** 
- `MISSING_TENANT_ID`: El `tenant_id` es obligatorio.
- `TENANT_NOT_FOUND`: El `tenant_id` especificado no existe.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar con los privilegios del propietario de la función.
- La consulta SQL es dinámica y depende de los parámetros de entrada.
- La función maneja errores generales con `RAISE` y devuelve un objeto de error en el resultado.
