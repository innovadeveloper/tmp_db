## api.get_persons_by_type
**Proposito:** Obtiene una lista de personas filtradas por tipo (PERSON, DRIVER, OWNER), estado de activación, búsqueda y paginación.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| person_type | VARCHAR(20) | Tipo de persona a buscar. Valores válidos: PERSON, DRIVER, OWNER. Es obligatorio. |
| is_active | BOOLEAN | Estado de activación de las personas. Por defecto es TRUE. |
| search | TEXT | Cadena de búsqueda para filtrar por nombre completo o número de identificación. |
| company_ids | INT[] | Lista de IDs de empresas para filtrar. |
| only_base | BOOLEAN | Indica si solo se deben devolver personas que no son de otro tipo (DRIVER o OWNER). Por defecto es FALSE. |
| page_number | INT | Número de página para la paginación. Por defecto es 1. |
| page_size | INT | Tamaño de la página para la paginación. Por defecto es 20, con un máximo de 100. |

**Retorna:** Un objeto `api.get_persons_by_type_result` que contiene la lista de personas filtradas, metadatos de paginación y información de error si ocurre.

**Tablas que lee:** `hr.person`, `hr.driver`, `fleet.vehicle_owner`, `shared.company`, `fleet.vehicle_owner_share`, `identity."user"`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:** 
1. Valida el tipo de persona proporcionado.
2. Normaliza los parámetros de entrada.
3. Realiza una consulta SQL dependiendo del tipo de persona (PERSON, DRIVER, OWNER).
4. Aplica los filtros de estado de activación, búsqueda y empresa.
5. Pagina los resultados según los parámetros de página.
6. Calcula el total de registros y páginas.
7. Construye el resultado con los datos de las personas y los metadatos de paginación.
8. Maneja excepciones y devuelve un error si ocurre.

**Errores y excepciones:** 
- `MISSING_PERSON_TYPE`: El tipo de persona no se proporciona.
- `INVALID_PERSON_TYPE`: El tipo de persona proporcionado no es válido.
- `INTERNAL_ERROR`: Error interno inesperado.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutar con los privilegios del propietario de la función.
- La función utiliza SQL dinámico para construir las consultas según el tipo de persona.
- La función maneja la paginación y el cálculo de metadatos de paginación.
