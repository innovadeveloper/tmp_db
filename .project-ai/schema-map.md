# Schema map

> Fuente: `full_schema_bscm_v11.sql`

## Tablas (49)

### `activity_log`
Columnas: `log_id`, `user_id`, `action`, `resource_type`, `resource_id`, `ip_address` … (+5)  

### `alert`
Columnas: `alert_id`, `alert_type_id`, `entity_type`, `entity_id`, `trip_id`, `vehicle_id` … (+9)  

### `alert_communication_log`
Columnas: `communication_id`, `alert_id`, `channel`, `recipient_type`, `recipient_id`, `sent_at` … (+5)  

### `alert_daily_summary`
Columnas: `summary_id`, `summary_date`, `total_alerts`, `critical_count`, `high_count`, `medium_count` … (+9)  

### `alert_type`
Columnas: `alert_type_id`, `code`, `name`, `description`, `category`, `severity` … (+6)  

### `catalog`
Columnas: `catalog_id`, `category`, `code`, `name`, `description`, `display_order` … (+2)  

### `checkpoint`
Columnas: `checkpoint_id`, `route_id`, `checkpoint_code`, `name`, `checkpoint_type`, `is_route_endpoint` … (+9)  

### `company`
Columnas: `company_id`, `tax_id`, `legal_name`, `trade_name`, `address`, `phone` … (+5)  

### `configuration`
Columnas: `config_id`, `key`, `value`, `data_type`, `description`, `is_editable` … (+2)  

### `document_type`
Columnas: `document_type_id`, `code`, `name`, `description`, `is_mandatory`, `requires_expiry` … (+5)  

### `driver`
Columnas: `driver_id`, `person_id`, `user_id`, `company_id`, `driver_code`, `hire_date` … (+9)  

### `file_storage`
Columnas: `file_id`, `original_filename`, `stored_filename`, `file_path`, `file_size_bytes`, `mime_type` … (+5)  

### `flyway_schema_history`
Columnas: `installed_rank`, `version`, `description`, `type`, `script`, `checksum` … (+4)  

### `gps_device`
Columnas: `gps_device_id`, `device_id`, `device_type`, `company_id`, `imei`, `serial_number` … (+9)  

### `gps_raw_event`
Columnas: `raw_event_id`, `gps_device_id`, `vehicle_id`, `beacon_mac_address`, `latitude`, `longitude` … (+9)  

### `incident`
Columnas: `incident_id`, `incident_type_id`, `trip_id`, `vehicle_id`, `driver_id`, `route_id` … (+9)  

### `incident_type`
Columnas: `incident_type_id`, `code`, `name`, `description`, `category`, `default_severity` … (+4)  

### `login_attempt`
Columnas: `attempt_id`, `username`, `ip_address`, `user_agent`, `success`, `failure_reason` … (+1)  

### `permission`
Columnas: `permission_id`, `code`, `description`, `module`, `is_active`, `created_at` … (+2)  

### `permission_template`
Columnas: `template_id`, `name`, `description`, `role_type`, `is_active`, `created_at`  

### `permission_template_detail`
Columnas: `template_detail_id`, `template_id`, `permission_id`, `created_at`  

### `person`
Columnas: `person_id`, `tax_id`, `full_name`, `gender`, `birth_date`, `nationality` … (+9)  

### `person_address`
Columnas: `address_id`, `person_id`, `address_type`, `address_line1`, `address_line2`, `district` … (+9)  

### `person_document`
Columnas: `person_document_id`, `person_id`, `document_type_id`, `document_number`, `issuing_entity`, `issue_date` … (+8)  

### `personnel`
Columnas: `personnel_id`, `person_id`, `company_id`, `user_id`, `employee_code`, `job_title` … (+9)  

### `role`
Columnas: `role_id`, `tenant_id`, `name`, `description`, `is_active`, `created_by` … (+2)  

### `role_permission`
Columnas: `role_permission_id`, `role_id`, `permission_id`, `is_active`, `created_at`  

### `role_permission_scope`
Columnas: `role_permission_scope_id`, `role_permission_id`, `scope_type_id`, `scope_id`, `company_id`, `is_active` … (+1)  

### `route`
Columnas: `route_id`, `company_id`, `code`, `name`, `route_type`, `total_distance_km` … (+4)  

### `route_control`
Columnas: `control_id`, `route_id`, `sequence_number`, `min_time_minutes`, `max_time_minutes`, `tolerance_minutes` … (+3)  

### `route_polyline`
Columnas: `polyline_id`, `route_id`, `direction`, `coordinates`, `encoded_polyline`, `total_points` … (+2)  

### `scope_type`
Columnas: `scope_type_id`, `code`, `description`  

### `tenant`
Columnas: `tenant_id`, `name`, `is_active`, `created_at`, `updated_at`  

### `tenant_company`
Columnas: `tenant_company_id`, `tenant_id`, `company_id`, `is_active`, `created_at`  

### `trip_event`
Columnas: `trip_event_id`, `trip_id`, `event_type`, `event_subtype`, `event_timestamp`, `latitude` … (+6)  

### `trip_location`
Columnas: `location_id`, `trip_id`, `gps_timestamp`, `latitude`, `longitude`, `speed_kmh` … (+3)  

### `trip_passenger_count`
Columnas: `passenger_count_id`, `trip_id`, `stop_id`, `count_timestamp`, `boarding_count`, `alighting_count` … (+3)  

### `trip_speed_event`
Columnas: `speed_event_id`, `trip_id`, `event_timestamp`, `latitude`, `longitude`, `speed_kmh` … (+5)  

### `trip_stop`
Columnas: `trip_stop_id`, `trip_id`, `scheduled_arrival_time`, `actual_arrival_time`, `arrival_delay_seconds`, `scheduled_departure_time` … (+7)  

### `user`
Columnas: `user_id`, `external_id`, `username`, `email`, `full_name`, `is_active` … (+3)  

### `user_permission`
Columnas: `user_permission_id`, `user_id`, `company_id`, `permission_id`, `granted_by`, `granted_at` … (+3)  

### `user_role`
Columnas: `user_role_id`, `user_id`, `role_id`, `tenant_id`, `is_active`, `assigned_by` … (+2)  

### `user_session`
Columnas: `session_id`, `user_id`, `token`, `ip_address`, `user_agent`, `started_at` … (+4)  

### `user_tenant_access`
Columnas: `user_tenant_access_id`, `user_id`, `tenant_id`, `is_active`, `granted_by`, `granted_at`  

### `vehicle`
Columnas: `vehicle_id`, `plate_number`, `internal_code`, `company_id`, `brand`, `model` … (+9)  

### `vehicle_assignment`
Columnas: `assignment_id`, `vehicle_id`, `driver_id`, `assigned_at`, `unassigned_at`, `assignment_type` … (+5)  

### `vehicle_document`
Columnas: `vehicle_document_id`, `vehicle_id`, `document_type_id`, `document_number`, `issuing_entity`, `issue_date` … (+8)  

### `vehicle_owner`
Columnas: `vehicle_owner_id`, `person_id`, `tax_id`, `full_name`, `bank_account`, `is_active` … (+2)  

### `vehicle_owner_share`
Columnas: `share_id`, `vehicle_id`, `vehicle_owner_id`, `ownership_percentage`, `valid_from`, `valid_until` … (+3)  

## Funciones y procedimientos (99)

- `_dispatch_alert_notifications` (function)
- `_generate_driver_code` (function)
- `_generate_employee_code` (function)
- `_generate_vehicle_code` (function)
- `acknowledge_alert` (function)
- `assign_role_to_user` (function)
- `assign_roles_to_user` (function)
- `assign_vehicle_to_driver` (function)
- `audit_type` (function)
- `auto_close_stale_alerts` (function)
- `create_alert` (function)
- `create_configuration` (function)
- `create_gps_partition` (function)
- `create_monthly_partitions` (function)
- `create_user_session` (function)
- `create_weekly_partitions` (function)
- `deactivate_route` (function)
- `deduct_license_points` (function)
- `delete_gps_device` (function)
- `delete_vehicle` (function)
- `describe_type` (function)
- `evaluate_gps_alerts` (function)
- `export_all_user_permissions` (function)
- `find_active_sessions` (function)
- `find_composite_types` (function)
- `find_current_pid` (function)
- `find_function_details` (function)
- `find_functions_by_schema` (function)
- `find_functions_returning_type` (function)
- `find_functions_using_type` (function)
- `find_functions_with_type_parameter` (function)
- `find_idle_in_transaction` (function)
- `find_idle_listeners` (function)
- `find_listen_process` (function)
- `find_notification_queue_status` (function)
- `find_queue_usage` (function)
- `find_terminate_backend` (function)
- `find_types_by_name` (function)
- `get_alert_types` (function)
- `get_alerts` (function)
- `get_catalog` (function)
- `get_checkpoints` (function)
- `get_companies` (function)
- `get_document_types` (function)
- `get_drivers` (function)
- `get_gps_devices` (function)
- `get_people` (function)
- `get_permission_templates` (function)
- `get_permissions` (function)
- `get_person_detail` (function)
- `get_personnel` (function)
- `get_persons_by_type` (function)
- `get_roles` (function)
- `get_routes` (function)
- `get_tenant_full` (function)
- `get_tenant_roles_json` (function)
- `get_user_permission` (function)
- `get_user_session` (function)
- `get_vehicle_documents` (function)
- `get_vehicle_owners` (function)
- `get_vehicles` (function)
- `get_vehicles_last_position` (function)
- `ingest_gps_raw_event` (function)
- `invalidate_user_session` (function)
- `kill_session` (function)
- `log_login_attempt` (function)
- `notify_permission_change` (function)
- `rebuild_alert_daily_summary` (function)
- `register_gps_raw_event` (function)
- `reset_sequence` (function)
- `resolve_alert` (function)
- `seed_alert_types` (function)
- `seed_catalog` (function)
- `seed_document_type` (function)
- `set_vehicle_ownership_share` (function)
- `sync_checkpoints` (function)
- `sync_permission_templates` (function)
- `sync_permissions` (function)
- `sync_role_permission_scopes` (function)
- `sync_role_permissions` (function)
- `sync_route_control_points` (function)
- `unassign_vehicle_from_driver` (function)
- `update_driver_status` (function)
- `update_gps_device_heartbeat` (function)
- `upsert_companies` (function)
- `upsert_driver` (function)
- `upsert_gps_device` (function)
- `upsert_person` (function)
- `upsert_person_address` (function)
- `upsert_person_document` (function)
- `upsert_personnel` (function)
- `upsert_role` (function)
- `upsert_route` (function)
- `upsert_route_polyline` (function)
- `upsert_tenant` (function)
- `upsert_users` (function)
- `upsert_vehicle` (function)
- `upsert_vehicle_document` (function)
- `upsert_vehicle_owner` (function)
