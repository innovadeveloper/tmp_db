## identity.tenant_company
**Tipo:** tabla
**Proposito:** Relación N:N entre tenants y empresas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| tenant_company_id | bigint | No | nextval('identity.tenant_company_tenant_company_id_seq'::regclass) | Identificador único de la relación entre tenant y empresa. |
| tenant_id | bigint | No | Por confirmar | Identificador del tenant. |
| company_id | integer | No | Por confirmar | Identificador de la empresa. |
| is_active | boolean | Sí | true | Indica si la relación está activa. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación de la relación. |

**Clave primaria:** tenant_company_id
**Claves foraneas:** tenant_company_tenant_id_fkey -> identity.tenant(tenant_id), tenant_company_company_id_fkey -> shared.company(company_id)
**Indices y restricciones:** tenant_company_pkey, uq_tenant_company, idx_tenant_company_company, idx_tenant_company_tenant
**Triggers:** Por confirmar
**Particionado:** Ninguna
**Observaciones:** Ninguna
