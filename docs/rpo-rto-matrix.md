# RPO and RTO Matrix

## English

## Objective

This document defines a sample RPO and RTO matrix for a generic AWS Backup strategy.

The matrix helps classify workloads by business criticality and define recovery expectations.

## Definitions

## RPO — Recovery Point Objective

RPO defines the maximum acceptable amount of data loss measured in time.

Example:  
If a system has an RPO of 4 hours, the organization accepts losing a maximum of 4 hours of data in the event of a disruption.

## RTO — Recovery Time Objective

RTO defines the maximum acceptable time to restore a service after a disruption.

Example:  
If a system has an RTO of 8 hours, the service should be restored within 8 hours after the incident begins.

## Workload Classification

| Tier | Criticality | Description | Example |
|---|---|---|---|
| Tier 1 | Critical | Systems with direct business or customer impact | Core database, customer-facing application |
| Tier 2 | High | Important operational systems | Application servers, middleware |
| Tier 3 | Medium | Internal support systems | File repositories, reports |
| Tier 4 | Low | Non-critical systems | Test environments, temporary workloads |

## RPO and RTO Matrix

| Workload Type | Criticality | Backup Frequency | RPO | RTO | Restore Priority |
|---|---|---:|---:|---:|---:|
| Core database | Critical | Every 4 hours | 4 hours | 4 hours | P1 |
| Customer-facing application | Critical | Every 4 hours | 4 hours | 8 hours | P1 |
| Application server | High | Daily | 24 hours | 8 hours | P2 |
| Middleware service | High | Daily | 24 hours | 12 hours | P2 |
| File repository | Medium | Daily | 24 hours | 24 hours | P3 |
| Reporting system | Medium | Daily | 24 hours | 48 hours | P3 |
| Monitoring configuration | Medium | Daily | 24 hours | 8 hours | P3 |
| Test environment | Low | Weekly | 7 days | Best effort | P4 |

## Restore Priority

| Priority | Description | Expected Response |
|---|---|---|
| P1 | Critical business impact | Immediate response and escalation |
| P2 | High operational impact | Same business day response |
| P3 | Medium or limited impact | Next business day response |
| P4 | Low impact or non-critical | Best effort |

## Compliance Validation

A workload is considered compliant when:

- Backup jobs are running according to the defined frequency.
- The last successful backup is within the defined RPO.
- Restore procedures are documented.
- Restore tests are executed periodically.
- Failed or missed backups are reviewed and tracked.

## Example Compliance Status

| Workload | Last Successful Backup | RPO | Status |
|---|---|---:|---|
| demo-critical-db | 2026-06-03 02:00 UTC | 4 hours | Compliant |
| demo-app-server-01 | 2026-06-03 01:00 UTC | 24 hours | Compliant |
| demo-file-repository | 2026-06-01 02:00 UTC | 24 hours | Not Compliant |
| demo-test-environment | 2026-05-29 02:00 UTC | 7 days | Compliant |

## Operational Notes

RPO and RTO values must be agreed with application owners, infrastructure teams, security teams and business stakeholders.

Backup frequency alone does not guarantee recoverability. Restore testing is required to validate that recovery objectives can be met.

---

# Matriz RPO y RTO

## Español

## Objetivo

Este documento define una matriz de ejemplo de RPO y RTO para una estrategia genérica de AWS Backup.

La matriz ayuda a clasificar workloads según criticidad de negocio y a definir expectativas de recuperación.

## Definiciones

## RPO — Recovery Point Objective

RPO define la cantidad máxima aceptable de pérdida de datos medida en tiempo.

Ejemplo:  
Si un sistema tiene un RPO de 4 horas, la organización acepta perder como máximo 4 horas de datos en caso de una interrupción.

## RTO — Recovery Time Objective

RTO define el tiempo máximo aceptable para restaurar un servicio después de una interrupción.

Ejemplo:  
Si un sistema tiene un RTO de 8 horas, el servicio debería restaurarse dentro de las 8 horas posteriores al inicio del incidente.

## Clasificación de Workloads

| Tier | Criticidad | Descripción | Ejemplo |
|---|---|---|---|
| Tier 1 | Crítico | Sistemas con impacto directo en negocio o clientes | Base de datos principal, aplicación expuesta a clientes |
| Tier 2 | Alta | Sistemas operativos importantes | Servidores de aplicación, middleware |
| Tier 3 | Media | Sistemas internos de soporte | Repositorios de archivos, reportes |
| Tier 4 | Baja | Sistemas no críticos | Ambientes de prueba, workloads temporales |

## Matriz RPO y RTO

| Tipo de Workload | Criticidad | Frecuencia de Backup | RPO | RTO | Prioridad de Restauración |
|---|---|---:|---:|---:|---:|
| Base de datos principal | Crítica | Cada 4 horas | 4 horas | 4 horas | P1 |
| Aplicación expuesta a clientes | Crítica | Cada 4 horas | 4 horas | 8 horas | P1 |
| Servidor de aplicación | Alta | Diario | 24 horas | 8 horas | P2 |
| Servicio middleware | Alta | Diario | 24 horas | 12 horas | P2 |
| Repositorio de archivos | Media | Diario | 24 horas | 24 horas | P3 |
| Sistema de reportes | Media | Diario | 24 horas | 48 horas | P3 |
| Configuración de monitoreo | Media | Diario | 24 horas | 8 horas | P3 |
| Ambiente de prueba | Baja | Semanal | 7 días | Best effort | P4 |

## Prioridad de Restauración

| Prioridad | Descripción | Respuesta esperada |
|---|---|---|
| P1 | Impacto crítico de negocio | Respuesta inmediata y escalación |
| P2 | Alto impacto operativo | Respuesta el mismo día hábil |
| P3 | Impacto medio o limitado | Respuesta al siguiente día hábil |
| P4 | Bajo impacto o no crítico | Best effort |

## Validación de Cumplimiento

Un workload se considera en cumplimiento cuando:

- Los jobs de backup se ejecutan según la frecuencia definida.
- El último backup exitoso está dentro del RPO definido.
- Los procedimientos de restauración están documentados.
- Las pruebas de restauración se ejecutan periódicamente.
- Los backups fallidos o no ejecutados son revisados y gestionados.

## Ejemplo de Estado de Cumplimiento

| Workload | Último Backup Exitoso | RPO | Estado |
|---|---|---:|---|
| demo-critical-db | 2026-06-03 02:00 UTC | 4 horas | Cumple |
| demo-app-server-01 | 2026-06-03 01:00 UTC | 24 horas | Cumple |
| demo-file-repository | 2026-06-01 02:00 UTC | 24 horas | No cumple |
| demo-test-environment | 2026-05-29 02:00 UTC | 7 días | Cumple |

## Notas Operativas

Los valores de RPO y RTO deben ser acordados con los dueños de aplicación, equipos de infraestructura, seguridad y áreas de negocio.

La frecuencia de backup por sí sola no garantiza recuperabilidad. Se requieren pruebas de restauración para validar que los objetivos de recuperación pueden cumplirse.
