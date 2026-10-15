## hr.personnel
**Tipo:** tabla
**Proposito:** Almacena información detallada sobre los empleados de la empresa, incluyendo su código de empleado, título de trabajo, tipo de empleo, estado de empleo, salario base, horario de trabajo y notas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| personnel_id | integer | No | nextval('hr.personnel_personnel_id_seq'::regclass) | Identificador único del registro de personal. |
| person_id | integer | No | Ninguna | Identificador único del registro de la persona asociada. |
| company_id | integer | No | Ninguna | Identificador único del registro de la empresa a la que pertenece el personal. |
| user_id | bigint | Sí | Ninguna | Identificador único del registro del usuario asociado, puede ser nulo. |
| employee_code | character varying(20) | No | Ninguna | Código único del empleado. |
| job_title | character varying(100) | No | Ninguna | Título del trabajo del empleado. |
| department | character varying(100) | Sí | Ninguna | Nombre del departamento al que pertenece el empleado. |
| hire_date | date | No | Ninguna | Fecha en que el empleado fue contratado. |
| termination_date | date | Sí | Ninguna | Fecha en que el empleado fue despedido. |
| employment_type | character varying(20) | Sí | Ninguna | Tipo de empleo del empleado (FULL_TIME, PART_TIME, CONTRACT). |
| employment_status | character varying(20) | Sí | 'ACTIVE' | Estado actual del empleo del empleado. |
| base_salary | numeric(10,2) | Sí | Ninguna | Salario base del empleado. |
| work_schedule | character varying(50) | Sí | Ninguna | Horario de trabajo del empleado. |
| notes | text | Sí | Ninguna | Notas adicionales sobre el empleado. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora de creación del registro. |
| updated_at | timestamp with time zone | Sí | now() | Fecha y hora de la última actualización del registro. |

**Clave primaria:** personnel_id
**Claves foraneas:** 
- person_id -> hr.person(person_id)
- company_id -> shared.company(company_id)
- user_id -> identity."user"(user_id)
**Indices y restricciones:** 
- personnel_employee_code_key: UNIQUE (employee_code)
- personnel_person_id_key: UNIQUE (person_id)
- personnel_user_id_key: UNIQUE (user_id)
- chk_personnel_type: CHECK (((employment_type IS NULL) OR ((employment_type)::text = ANY ((ARRAY['FULL_TIME'::character varying, 'PART_TIME'::character varying, 'CONTRACT'::character varying])::text[]))))
- idx_personnel_code: B-tree (employee_code)
- idx_personnel_company: B-tree (company_id, employment_status)
- idx_personnel_job: B-tree (job_title, employment_status)
**Triggers:** Por confirmar
**Particionado:** Por confirmar
**Observaciones:** Ninguna
