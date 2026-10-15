## api.upsert_tenant
**Proposito:** Inserta o actualiza un inquilino (tenant) en la base de datos, y sincroniza sus vínculos con compañías (companies). Maneja tanto inserciones como actualizaciones, y permite desvincular compañías que ya no están en el payload.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_tenant_input | Objeto de entrada que contiene los datos del inquilino y los IDs de las compañías a vincular. |

**Retorna:** api.upsert_tenant_result
**Tablas que lee:** identity.tenant, shared.company, identity.tenant_company
**Tablas que modifica (INSERT/UPDATE/DELETE):** identity.tenant, identity.tenant_company
**Funciones que invoca:** Por confirmar
**Logica paso a paso:** 
1. Valida que el nombre del inquilino no esté vacío al crear un nuevo inquilino.
2. Si el inquilino existe, verifica si hay cambios en los datos y actualiza si es necesario.
3. Si el inquilino no existe, lo inserta.
4. Sincroniza los vínculos con las compañías proporcionadas en el payload:
   - Valida que los IDs de las compañías no estén duplicados.
   - Valida que las compañías existan.
   - Vincula las compañías que no están vinculadas.
   - Desvincula las compañías que ya no están en el payload.
5. Retorna un resultado que incluye el estado del inquilino, el número de compañías vinculadas, desvinculadas y con errores.

**Errores y excepciones:** 
- 'MISSING_TENANT_NAME': El nombre del inquilino es obligatorio al crear un nuevo inquilino.
- 'TENANT_NOT_FOUND': El inquilino con el ID proporcionado no existe.
- 'DUPLICATE_COMPANY_ID_IN_BATCH': Un ID de compañía aparece más de una vez en el array.
- 'COMPANY_NOT_FOUND': Una de las compañías proporcionadas no existe.
- 'INTERNAL_ERROR': Error interno inesperado.

**Observaciones:** 
- La función es definida como SECURITY DEFINER, lo que significa que ejecuta con los privilegios del propietario de la función, no del usuario que la invoca.
- La función utiliza SQL dinámico para manejar diferentes escenarios de inserción y actualización.
