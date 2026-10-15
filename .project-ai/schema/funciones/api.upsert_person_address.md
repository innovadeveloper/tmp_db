## api.upsert_person_address
**Proposito:** Inserta o actualiza una dirección de persona en la base de datos. Maneja tanto inserciones como actualizaciones, validando los datos y gestionando la dirección principal de la persona.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.upsert_person_address_input | Objeto de entrada que contiene los datos de la dirección a insertar o actualizar. |

**Retorna:** Un objeto `api.upsert_person_address_result` que indica el resultado de la operación, incluyendo el estado de éxito, el código de error, el mensaje de error, el estado del address, el ID del address, el ID de la persona, y detalles adicionales como la fecha de creación y actualización.

**Tablas que lee:** `hr.person_address`, `hr.person`

**Tablas que modifica (INSERT/UPDATE/DELETE):** `hr.person_address`

**Funciones que invoca:** `COALESCE`, `NULLIF`, `TRIM`, `NOW()`, `GET DIAGNOSTICS`

**Logica paso a paso:**
1. **Validación de entrada**: Verifica que los parámetros sean válidos y existan las referencias necesarias (como la persona y el tipo de dirección).
2. **Validación de coordenadas**: Asegura que las coordenadas sean válidas si se proporcionan.
3. **Detección de cambios**: Identifica si hay cambios significativos entre los datos proporcionados y los existentes.
4. **Gestión de dirección principal**: Si se marca una dirección como principal, se desmarca la dirección principal anterior de la persona.
5. **Operación INSERT/UPDATE**: Realiza la inserción o actualización de la dirección en la base de datos.
6. **Retorno de resultados**: Devuelve un objeto con el resultado de la operación, incluyendo detalles de la dirección y cualquier error que ocurra.

**Errores y excepciones:**
- `unique_violation`: Lanza un error si hay un conflicto de concurrencia al establecer una dirección principal.
- `OTHERS`: Lanza un error interno con el mensaje de error de PostgreSQL.

**Observaciones:** La función utiliza `SECURITY DEFINER` para ejecutarse con los privilegios del propietario de la función, lo que puede afectar la seguridad si no se gestiona adecuadamente. La función también puede generar consultas SQL dinámicas, lo que debe ser manejado con precaución para evitar inyecciones SQL.
