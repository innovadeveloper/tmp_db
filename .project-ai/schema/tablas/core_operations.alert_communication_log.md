## core_operations.alert_communication_log
**Tipo:** tabla  
**Proposito:** Registra los detalles de las comunicaciones relacionadas con alertas.

| Columna | Tipo | Nulo | Por defecto | Descripcion |
|---|---|---|---|---|
| communication_id | bigint | No | Sí | Identificador único de la comunicación. |
| alert_id | bigint | No | Sí | Identificador de la alerta a la que pertenece la comunicación. |
| channel | character varying(20) | No | Sí | Canal por el cual se envió la comunicación (EMAIL, SMS, PUSH, WEBHOOK, WHATSAPP). |
| recipient_type | character varying(20) | No | Sí | Tipo de destinatario (por ejemplo, USER, GROUP). |
| recipient_id | bigint | Sí | Sí | Identificador del destinatario, dependiendo del tipo de destinatario. |
| sent_at | timestamp with time zone | Sí | now() | Fecha y hora en que se envió la comunicación. |
| delivered_at | timestamp with time zone | Sí | Sí | Fecha y hora en que se entregó la comunicación. |
| read_at | timestamp with time zone | Sí | Sí | Fecha y hora en que la comunicación fue leída. |
| status | character varying(20) | Sí | 'PENDING' | Estado actual de la comunicación (PENDING, SENT, DELIVERED, READ, FAILED). |
| error_message | text | Sí | Sí | Mensaje de error asociado a la comunicación, si es que ocurrió algún problema. |
| created_at | timestamp with time zone | Sí | now() | Fecha y hora en que se creó el registro de la comunicación. |

**Clave primaria:** communication_id  
**Claves foraneas:** alert_id -> core_operations.alerts.alert_id  
**Indices y restricciones:**  
- chk_comm_channel: Verifica que el canal de comunicación sea uno de los permitidos (EMAIL, SMS, PUSH, WEBHOOK, WHATSAPP).  
- chk_comm_status: Verifica que el estado de la comunicación sea uno de los permitidos (PENDING, SENT, DELIVERED, READ, FAILED).  
- idx_alert_comm_alert: Índice B-tree en alert_id y sent_at para mejorar la eficiencia de las consultas filtradas por alerta y fecha de envío.

**Triggers:**  
Por confirmar.

**Observaciones:**  
- La columna recipient_id es opcional y su valor depende del tipo de destinatario (recipient_type).
- El campo error_message solo se llena si ocurre un error durante el envío de la comunicación.
- El índice idx_alert_comm_alert puede ser útil para consultas que buscan comunicaciones recientes de una alerta específica.
