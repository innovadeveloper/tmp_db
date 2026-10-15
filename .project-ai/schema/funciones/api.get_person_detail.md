## api.get_person_detail
**Proposito:** Obtiene los detalles de una persona, incluyendo información personal, datos de cuenta de sistema, acceso al inquilino y roles activos.

**Parametros:**
| Nombre | Tipo | Descripcion |
|---|---|---|
| p_input | api.get_person_detail_input | Objeto de entrada que contiene el `person_id` y el `tenant_id`. |

**Retorna:** Un objeto `api.get_person_detail_result` que contiene los detalles de la persona, incluyendo información personal, datos de cuenta de sistema, acceso al inquilino y roles activos.

**Tablas que lee:** `hr.person`, `hr.personnel`, `hr.driver`, `identity."user"`, `identity.user_tenant_access`, `identity.user_role`, `identity.role`.

**Tablas que modifica (INSERT/UPDATE/DELETE):** No modifica ninguna tabla.

**Funciones que invoca:** No invoca ninguna función externa.

**Logica paso a paso:**
1. Valida que `person_id` y `tenant_id` no sean nulos.
2. Obtiene los detalles personales de la persona desde la tabla `hr.person`.
3. Determina el tipo de rol (PERSONNEL o DRIVER) y obtiene los detalles correspondientes.
4. Si la persona tiene cuenta en `identity."user"`, obtiene los detalles de la cuenta.
5. Verifica el acceso del usuario al inquilino especificado.
6. Obtiene los roles activos del usuario en el inquilino.
7. Asigna valores por defecto a los campos opcionales si no se proporcionan.
8. Devuelve el resultado con los detalles de la persona.

**Errores y excepciones:** 
- `MISSING_PERSON_ID`: Si `person_id` es nulo.
- `MISSING_TENANT_ID`: Si `tenant_id` es nulo.
- `PERSON_NOT_FOUND`: Si la persona no existe.
- `INTERNAL_ERROR`: Para cualquier otro error inesperado.

**Observaciones:** La función es `STABLE`, lo que significa que el resultado no cambia si los parámetros no cambian. No utiliza funciones dinámicas ni es definida como `SECURITY DEFINER`.
