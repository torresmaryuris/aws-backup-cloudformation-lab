# Backup Validation Checklist

## English

## Objective

This checklist provides a standard operational control for validating AWS Backup jobs, backup vault configuration, backup plans, recovery points and restore readiness.

## Daily Validation

- [ ] Backup jobs completed successfully.
- [ ] No failed critical backup jobs remain unresolved.
- [ ] Backup jobs were triggered according to schedule.
- [ ] Backup duration is within the expected range.
- [ ] Backup vault is available.
- [ ] Recovery points were created.
- [ ] Critical workloads meet the defined RPO.
- [ ] Failed or missed jobs were reviewed.
- [ ] Backup alerts were checked.
- [ ] Backup logs were reviewed.

## Weekly Validation

- [ ] Backup plans are correctly assigned.
- [ ] Tag-based backup selection is working.
- [ ] Required resources have the correct backup tag.
- [ ] Backup retention policies are being applied.
- [ ] Recovery points older than retention policy are removed.
- [ ] Backup vault access permissions were reviewed.
- [ ] IAM role used by AWS Backup is valid.
- [ ] Backup monitoring dashboards were reviewed.
- [ ] Open backup incidents were updated.
- [ ] Corrective actions were assigned if required.

## Monthly Validation

- [ ] Restore test was completed for selected workloads.
- [ ] Restore test result was documented.
- [ ] RPO and RTO matrix was reviewed.
- [ ] Backup scope was reviewed.
- [ ] New workloads were added to the backup plan if required.
- [ ] Decommissioned workloads were removed.
- [ ] Backup costs were reviewed.
- [ ] Backup storage consumption was reviewed.
- [ ] Security and access controls were reviewed.
- [ ] Documentation was updated.

## Restore Readiness Validation

- [ ] Restore permissions are available.
- [ ] Restore procedure is documented.
- [ ] Recovery owner is identified.
- [ ] Restore target environment is defined.
- [ ] Application validation steps are documented.
- [ ] Database validation steps are documented.
- [ ] Monitoring validation steps are documented.
- [ ] Communication path is defined.
- [ ] Escalation path is defined.

## Security Validation

- [ ] Backup vault is not publicly accessible.
- [ ] Backup data is encrypted.
- [ ] IAM permissions follow least privilege.
- [ ] No production credentials are stored in documentation.
- [ ] No access keys are committed to the repository.
- [ ] No real AWS account IDs are committed to the repository.
- [ ] No real ARNs are committed to the repository.
- [ ] Backup operators have only required permissions.
- [ ] Restore actions are auditable.

## Backup Job Failure Review

For every failed backup job, validate:

- [ ] Affected workload was identified.
- [ ] Failure reason was reviewed.
- [ ] Logs were checked.
- [ ] Storage capacity was checked.
- [ ] Network connectivity was checked.
- [ ] IAM permissions were checked.
- [ ] Backup job was rerun if applicable.
- [ ] RPO impact was evaluated.
- [ ] Incident was escalated if required.
- [ ] Corrective action was documented.

## Evidence to Collect

Recommended evidence for operational review:

- Screenshot or export of backup job status.
- Backup job ID.
- Backup plan name.
- Backup vault name.
- Last successful backup timestamp.
- Failed job logs, if applicable.
- Restore test result.
- Recovery point details.
- Corrective action record.

## Completion Criteria

The backup validation is considered completed when:

- Critical backups are successful.
- Failed jobs are reviewed.
- RPO compliance is confirmed.
- Backup vault and backup plan are healthy.
- Recovery points are available.
- Required incidents or tasks are documented.
- Restore readiness is confirmed.

---

# Checklist de Validación de Backup

## Español

## Objetivo

Este checklist proporciona un control operativo estándar para validar jobs de AWS Backup, configuración del backup vault, backup plans, recovery points y preparación para restauración.

## Validación Diaria

- [ ] Los jobs de backup finalizaron correctamente.
- [ ] No quedan jobs críticos fallidos sin resolver.
- [ ] Los jobs de backup se ejecutaron según la programación.
- [ ] La duración del backup está dentro del rango esperado.
- [ ] El backup vault está disponible.
- [ ] Los recovery points fueron creados.
- [ ] Los workloads críticos cumplen el RPO definido.
- [ ] Los jobs fallidos o no ejecutados fueron revisados.
- [ ] Las alertas de backup fueron revisadas.
- [ ] Los logs de backup fueron revisados.

## Validación Semanal

- [ ] Los backup plans están correctamente asignados.
- [ ] La selección de backup basada en tags funciona correctamente.
- [ ] Los recursos requeridos tienen el tag correcto de backup.
- [ ] Las políticas de retención se están aplicando.
- [ ] Los recovery points antiguos se eliminan según la política de retención.
- [ ] Los permisos de acceso al backup vault fueron revisados.
- [ ] El rol IAM usado por AWS Backup es válido.
- [ ] Los dashboards de monitoreo de backup fueron revisados.
- [ ] Los incidentes abiertos de backup fueron actualizados.
- [ ] Las acciones correctivas fueron asignadas si corresponde.

## Validación Mensual

- [ ] Se completó una prueba de restauración para workloads seleccionados.
- [ ] El resultado de la prueba de restauración fue documentado.
- [ ] La matriz RPO y RTO fue revisada.
- [ ] El alcance del backup fue revisado.
- [ ] Nuevos workloads fueron agregados al backup plan si corresponde.
- [ ] Workloads decomisionados fueron removidos.
- [ ] Los costos de backup fueron revisados.
- [ ] El consumo de almacenamiento de backup fue revisado.
- [ ] Los controles de seguridad y acceso fueron revisados.
- [ ] La documentación fue actualizada.

## Validación de Preparación para Restauración

- [ ] Los permisos para restauración están disponibles.
- [ ] El procedimiento de restauración está documentado.
- [ ] El responsable de recuperación está identificado.
- [ ] El ambiente destino de restauración está definido.
- [ ] Los pasos de validación de aplicación están documentados.
- [ ] Los pasos de validación de base de datos están documentados.
- [ ] Los pasos de validación de monitoreo están documentados.
- [ ] La ruta de comunicación está definida.
- [ ] La ruta de escalación está definida.

## Validación de Seguridad

- [ ] El backup vault no es públicamente accesible.
- [ ] Los datos de backup están cifrados.
- [ ] Los permisos IAM siguen el principio de mínimo privilegio.
- [ ] No hay credenciales productivas en la documentación.
- [ ] No hay access keys subidas al repositorio.
- [ ] No hay IDs reales de cuentas AWS subidos al repositorio.
- [ ] No hay ARNs reales subidos al repositorio.
- [ ] Los operadores de backup tienen solo los permisos requeridos.
- [ ] Las acciones de restauración son auditables.

## Revisión de Job de Backup Fallido

Para cada job de backup fallido, validar:

- [ ] El workload afectado fue identificado.
- [ ] La causa de la falla fue revisada.
- [ ] Los logs fueron revisados.
- [ ] La capacidad de almacenamiento fue revisada.
- [ ] La conectividad de red fue revisada.
- [ ] Los permisos IAM fueron revisados.
- [ ] El job de backup fue reejecutado si corresponde.
- [ ] El impacto en RPO fue evaluado.
- [ ] El incidente fue escalado si corresponde.
- [ ] La acción correctiva fue documentada.

## Evidencia a Recolectar

Evidencia recomendada para revisión operativa:

- Captura o export del estado del job de backup.
- ID del job de backup.
- Nombre del backup plan.
- Nombre del backup vault.
- Fecha y hora del último backup exitoso.
- Logs del job fallido, si corresponde.
- Resultado de prueba de restauración.
- Detalles del recovery point.
- Registro de acción correctiva.

## Criterio de Finalización

La validación de backup se considera completada cuando:

- Los backups críticos están exitosos.
- Los jobs fallidos fueron revisados.
- El cumplimiento de RPO fue confirmado.
- El backup vault y el backup plan están saludables.
- Los recovery points están disponibles.
- Los incidentes o tareas requeridas fueron documentados.
- La preparación para restauración fue confirmada.
