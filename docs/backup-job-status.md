# Backup Job Status and Failed States

## English

## Objective

This document defines the standard backup job statuses and the expected operational response for each state.

## Backup Job Status

| Status | Description | Required Action |
|---|---|---|
| Successful | Backup completed without errors | No action required. Validate according to the regular checklist. |
| Failed | Backup job did not complete successfully | Investigate immediately and rerun the job if applicable. |
| Warning | Backup completed with non-critical issues | Review logs and validate whether the backup is usable. |
| Missed | Backup job did not start at the scheduled time | Check scheduler, permissions, service availability and dependencies. |
| Running | Backup job is currently in progress | Monitor duration and performance. |
| Canceled | Backup job was manually or automatically stopped | Validate the reason and reschedule if required. |
| Partial | Backup completed only for part of the workload | Identify missing components and execute corrective backup. |
| Expired | Backup exceeded the defined retention period | Confirm retention policy behavior. |
| Not Configured | System has no active backup policy assigned | Assign the workload to the correct backup policy. |

## Failed Backup Handling Process

When a backup job fails, the following process should be followed:

1. Identify the affected workload.
2. Review the backup job logs.
3. Confirm the failure reason.
4. Check storage capacity.
5. Validate network connectivity.
6. Validate permissions and credentials.
7. Check if the workload was available during the backup window.
8. Rerun the backup job if possible.
9. Escalate if the failure affects RPO compliance.
10. Document the incident and corrective action.

## Common Failure Causes

| Cause | Description | Possible Action |
|---|---|---|
| Storage full | Backup repository has insufficient capacity | Expand storage or clean expired backups |
| Permission denied | Backup service account lacks required permissions | Review IAM, RBAC or local permissions |
| Network failure | Backup service cannot reach the workload | Validate routing, firewall and DNS |
| Snapshot error | Snapshot creation failed | Check cloud provider or hypervisor logs |
| Database lock | Database was unavailable or locked | Coordinate with DBA or application team |
| Timeout | Backup exceeded the expected execution window | Review performance and backup size |
| Encryption error | Encryption key or certificate issue | Validate KMS, certificates or key permissions |
| Agent offline | Backup agent is not reachable | Restart or reinstall backup agent |
| Policy mismatch | Workload assigned to incorrect policy | Reassign backup policy |
| Retention conflict | Backup retention rule failed | Review lifecycle and retention configuration |

## Severity Classification

| Severity | Condition | Response Time |
|---|---|---|
| P1 | Critical system backup failed and RPO is at risk | Immediate |
| P2 | Important system backup failed | Same business day |
| P3 | Non-critical backup failed | Next business day |
| P4 | Warning or informational issue | Best effort |

## Escalation Criteria

Escalation is required when:

- A critical backup fails more than once.
- No valid backup exists within the defined RPO.
- Restore testing fails.
- Backup repository capacity exceeds 80%.
- Encryption or access control errors are detected.
- Multiple workloads fail in the same backup window.

## Example Backup Status Summary

| Workload | Status | Last Backup | RPO Compliance | Action |
|---|---|---|---|---|
| demo-critical-db | Successful | 2026-06-03 02:00 UTC | Compliant | No action |
| demo-app-server-01 | Warning | 2026-06-03 01:00 UTC | Compliant | Review logs |
| demo-file-repository | Failed | 2026-06-03 00:00 UTC | At Risk | Rerun backup |
| demo-monitoring-config | Missed | 2026-06-02 23:00 UTC | At Risk | Check scheduler |
| demo-test-environment | Not Configured | N/A | Not Compliant | Assign policy |

## Operational Notes

A failed backup does not always mean data loss, but it can mean that the recovery point objective is no longer being met.

For critical workloads, backup failures must be treated as operational risks and tracked until resolution.

---

# Estados de Jobs de Backup y Estados Fallidos

## Español

## Objetivo

Este documento define los estados estándar de los jobs de backup y la respuesta operativa esperada para cada estado.

## Estados del Job de Backup

| Estado | Descripción | Acción requerida |
|---|---|---|
| Successful | El backup finalizó sin errores | No requiere acción. Validar según el checklist regular. |
| Failed | El backup no finalizó correctamente | Investigar de inmediato y volver a ejecutar si corresponde. |
| Warning | El backup finalizó con advertencias no críticas | Revisar logs y validar si el backup es utilizable. |
| Missed | El backup no inició en el horario programado | Revisar scheduler, permisos, disponibilidad del servicio y dependencias. |
| Running | El backup está actualmente en ejecución | Monitorear duración y rendimiento. |
| Canceled | El backup fue detenido manual o automáticamente | Validar la causa y reprogramar si corresponde. |
| Partial | El backup se completó solo para una parte del workload | Identificar componentes faltantes y ejecutar backup correctivo. |
| Expired | El backup superó el período de retención definido | Confirmar el comportamiento de la política de retención. |
| Not Configured | El sistema no tiene una política de backup activa | Asignar el workload a la política correcta. |

## Proceso de Manejo de Backups Fallidos

Cuando un backup falla, se debe seguir este proceso:

1. Identificar el workload afectado.
2. Revisar los logs del job de backup.
3. Confirmar la causa de la falla.
4. Revisar capacidad de almacenamiento.
5. Validar conectividad de red.
6. Validar permisos y credenciales.
7. Confirmar si el workload estaba disponible durante la ventana de backup.
8. Reejecutar el backup si es posible.
9. Escalar si la falla afecta el cumplimiento del RPO.
10. Documentar el incidente y la acción correctiva.

## Causas Comunes de Falla

| Causa | Descripción | Posible acción |
|---|---|---|
| Storage full | El repositorio de backup no tiene capacidad suficiente | Expandir almacenamiento o limpiar backups expirados |
| Permission denied | La cuenta de servicio no tiene permisos suficientes | Revisar IAM, RBAC o permisos locales |
| Network failure | El servicio de backup no puede alcanzar el workload | Validar routing, firewall y DNS |
| Snapshot error | La creación del snapshot falló | Revisar logs del proveedor cloud o hipervisor |
| Database lock | La base de datos no estaba disponible o estaba bloqueada | Coordinar con DBA o equipo de aplicación |
| Timeout | El backup excedió la ventana esperada de ejecución | Revisar rendimiento y tamaño del backup |
| Encryption error | Problema con llave o certificado de cifrado | Validar KMS, certificados o permisos de llaves |
| Agent offline | El agente de backup no está disponible | Reiniciar o reinstalar el agente |
| Policy mismatch | El workload está asignado a una política incorrecta | Reasignar política de backup |
| Retention conflict | La regla de retención falló | Revisar configuración de ciclo de vida y retención |

## Clasificación de Severidad

| Severidad | Condición | Tiempo de respuesta |
|---|---|---|
| P1 | Backup de sistema crítico fallido y RPO en riesgo | Inmediato |
| P2 | Backup de sistema importante fallido | Mismo día hábil |
| P3 | Backup de sistema no crítico fallido | Siguiente día hábil |
| P4 | Advertencia o evento informativo | Best effort |

## Criterios de Escalación

Se requiere escalación cuando:

- Un backup crítico falla más de una vez.
- No existe un backup válido dentro del RPO definido.
- La prueba de restauración falla.
- La capacidad del repositorio de backup supera el 80%.
- Se detectan errores de cifrado o control de acceso.
- Múltiples workloads fallan en la misma ventana de backup.

## Ejemplo de Resumen de Estado

| Workload | Estado | Último Backup | Cumplimiento RPO | Acción |
|---|---|---|---|---|
| demo-critical-db | Successful | 2026-06-03 02:00 UTC | Cumple | Sin acción |
| demo-app-server-01 | Warning | 2026-06-03 01:00 UTC | Cumple | Revisar logs |
| demo-file-repository | Failed | 2026-06-03 00:00 UTC | En riesgo | Reejecutar backup |
| demo-monitoring-config | Missed | 2026-06-02 23:00 UTC | En riesgo | Revisar scheduler |
| demo-test-environment | Not Configured | N/A | No cumple | Asignar política |

## Notas Operativas

Un backup fallido no siempre significa pérdida de datos, pero puede significar que el objetivo de punto de recuperación ya no se está cumpliendo.

Para workloads críticos, las fallas de backup deben tratarse como riesgos operativos y deben ser gestionadas hasta su resolución.
