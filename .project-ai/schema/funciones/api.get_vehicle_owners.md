## api.get_vehicle_owners
**Propósito:** Obtiene una lista paginada de propietarios de vehículos y sus participaciones vinculadas a un tenant, con soporte para filtrado por empresa, búsqueda textual y visualización de registros históricos.

**Parámetros:**
| Nombre | Tipo | Descripción |
|---|---|---|
| `p_input` | `api.get_vehicle_owners_input` | Tipo compuesto que agrupa: `tenant_id` (obligatorio), `company_id` (opcional), `page_number` (default 1), `page_size` (default 20, máx 100), `search` (texto), `include_history` (booleano, default FALSE). |

**Retorna:** `api.get_vehicle_owners_result` (tipo compuesto con: `success`, `error_code`, `error_message`, `page_number`, `page_size`, `total_records`, `total_pages`, `has_next_page`, `has_prev_page`, `owners` como array de `api.vehicle_owner_share_row`).
**Tablas que lee:** `identity.tenant`, `identity.tenant_company`, `fleet.vehicle`, `fleet.vehicle_owner_share`, `fleet.vehicle_owner`, `hr.person`.
**Tablas que modifica:** Ninguna.
**Lógica paso a paso:**
1. Normaliza parámetros (límites de paginación, limpieza de búsqueda, valores por defecto).
2. Valida existencia del `tenant_id` en `identity.tenant`.
3. Si se provee `company_id`, verifica su pertenencia activa al tenant en `identity.tenant_company`.
4. Construye CTEs (`base`, `counted`, `paged`) que unen tablas de tenants, empresas, vehículos, acciones y personas, aplicando filtros de vigencia y búsqueda (`ILIKE`).
5. Calcula el total de registros y aplica paginación (`LIMIT`/`OFFSET`) ordenando por nombre, placa y fecha.
6. Agrupa los resultados paginados en un array del tipo `api.vehicle_owner_share_row`.
7. Calcula metadatos de paginación y retorna la estructura de éxito o captura excepciones.
**Observaciones:**
- Declarada como `STABLE` y sin `SECURITY DEFINER` (ejecuta con privilegios del usuario invocador).
- Uso de `CURRENT_DATE` asegura consistencia de fechas dentro de la transacción.
- Paginación con `OFFSET` tiene costo O(N) en tablas grandes; considerar paginación por cursor para escalabilidad.
- Búsqueda con `ILIKE` sin índices específicos puede generar escaneos completos; evaluar extensión `pg_trgm` si el volumen lo requiere.
- El bloque `EXCEPTION` captura cualquier error y lo devuelve en la respuesta, evitando fallos silenciosos en la aplicación cliente.
