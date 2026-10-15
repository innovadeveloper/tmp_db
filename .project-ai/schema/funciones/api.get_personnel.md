## api.get_personnel

**Proposito:** Obtiene una lista paginada de personal de un tenant específico, filtrando por diversos criterios como estado activo, tipo de empleo, estado de empleo y búsqueda.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_personnel_input | Objeto de entrada que contiene los parámetros de la consulta, incluyendo tenant_id, número de página, tamaño de página, estado activo, tipo de empleo, estado de empleo y búsqueda. |

**Retorna:** Un objeto `api.get_personnel_result` que contiene la lista de personal, metadatos de paginación y información de error.

**Tablas que lee:** `hr.personnel`, `identity.tenant_company`, `hr.person`, `identity."user"`, `identity.user_role`, `identity.role`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** `NULLIF`, `TRIM`, `COALESCE`, `GREATEST`, `LEAST`, `CEIL`, `ARRAY_AGG`, `STRING_AGG`.

**Logica paso a paso:**
1. Normaliza los parámetros de entrada.
2. Realiza validaciones, como el tenant_id y la existencia del tenant.
3. Construye una consulta principal que filtra el personal según los criterios proporcionados.
4. Calcula el total de registros y la página actual.
5. Aplica la paginación a los resultados.
6. Formatea los resultados para incluir el nombre completo y los roles activos.
7. Devuelve el resultado en un objeto `api.get_personnel_result`.

**Errores y excepciones:** Captura cualquier error interno y devuelve un código de error y un mensaje de error.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutar con los privilegios del propietario de la función. No utiliza SQL dinámico.
