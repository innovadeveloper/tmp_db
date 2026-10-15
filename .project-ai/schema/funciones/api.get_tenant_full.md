## api.get_tenant_full
**Proposito:** Obtiene la información detallada de un inquilino, incluyendo sus empresas asociadas.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_tenant_id | integer | Identificador del inquilino a consultar. |

**Retorna:** Un registro de tipo `api.result_get_tenant_full_api` que contiene la información del inquilino y sus empresas.

**Tablas que lee:** 
- `identity.tenant`
- `identity.tenant_company`
- `shared.company`

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Inicializa el resultado con `success` como `true` y `error_code` y `error_message` como `NULL`.
2. Busca el inquilino con el `tenant_id` proporcionado.
3. Si el inquilino no se encuentra, lanza una excepción con el código de error `P0002` y el mensaje 'Tenant no encontrado'.
4. Si el inquilino se encuentra, asigna los valores del inquilino al resultado.
5. Obtiene las empresas asociadas al inquilino y las almacena en un array de tipos compuestos `api.tenant_company_detail`.
6. Devuelve el resultado.

**Errores y excepciones:**
- `no_data_found`: Si el inquilino no se encuentra, lanza una excepción con el código de error `P0002` y el mensaje 'Tenant no encontrado'.
- `OTHERS`: Captura cualquier otra excepción y establece `success` como `false`, `error_code` como el código de estado de la excepción, y `error_message` como el mensaje de la excepción.

**Observaciones:** 
- La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función.
- La función utiliza SQL dinámico para construir el array de empresas.
