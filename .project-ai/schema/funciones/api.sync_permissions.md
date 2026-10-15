## api.sync_permissions
**Proposito:** Sincroniza los permisos en la base de datos `identity.permission` según los datos proporcionados en el parámetro de entrada.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.sync_permissions_input | Objeto de entrada que contiene un array de permisos a sincronizar. |

**Retorna:** Un objeto `api.sync_permissions_result` que contiene el resultado de la operación, incluyendo detalles de cada permiso procesado.

**Tablas que lee:** `identity.permission`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `identity.permission`

**Funciones que invoca:** Ninguna

**Logica paso a paso:**
1. Valida que el array de permisos no sea `NULL`.
2. Procesa cada permiso en el array:
   - Valida que el código del permiso no sea `NULL` ni vacío.
   - Valida que el formato del código sea correcto (`module.resource.action`).
   - Valida que el código no esté duplicado en el lote.
   - Resuelve o valida el módulo del permiso.
   - Busca si el permiso ya existe en la base de datos.
   - Si el permiso existe, detecta cambios y actualiza o marca como omitido.
   - Si el permiso no existe, lo inserta.
3. Desactiva los permisos activos que no están presentes en el payload.
4. Devuelve un objeto de resultado con los detalles de la operación.

**Errores y excepciones:** 
- `NULL_PERMISSIONS_ARRAY`: Si el array de permisos es `NULL`.
- `MISSING_CODE`: Si el código del permiso es `NULL` o vacío.
- `INVALID_CODE_FORMAT`: Si el formato del código no es correcto.
- `DUPLICATE_CODE_IN_BATCH`: Si el código aparece más de una vez en el lote.
- `INVALID_MODULE`: Si el módulo del permiso es inválido.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** 
- La función es segura (`SECURITY DEFINER`).
- Maneja operaciones de inserción, actualización y desactivación de forma segura.
- Utiliza arrays para evitar duplicados y para la fase de desactivación.
