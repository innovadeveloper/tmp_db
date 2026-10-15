## identity.tenant
**Tipo:** tabla
**Proposito:** Contenedor lógico principal (empresa u organización matriz)

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| tenant_id | bigint | No | nextval('identity.tenant_tenant_id_seq'::regclass) | Identificador único del inquilino |
| name | character varying(255) | No | Por confirmar | Nombre del inquilino |
| is_active | boolean | Sí | true | Indica si el inquilino está activo |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del inquilino |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización del inquilino |

**Clave primaria:** tenant_id
**Claves foraneas:** Ninguna
**Indices y restricciones:** idx_tenant_active (btree en is_active)
**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** La columna `name` no tiene un valor por defecto definido explícitamente en el SQL proporcionado.
