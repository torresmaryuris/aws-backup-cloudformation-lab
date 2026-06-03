# Deployment Guide

## English

## Objective

This guide explains how to deploy the demo AWS Backup CloudFormation template included in this repository.

The deployment creates:

- AWS Backup Vault
- AWS Backup Plan
- Backup Rule
- IAM Role for AWS Backup
- Tag-based Backup Selection

This is a generic and anonymized lab. It does not contain real production data, real AWS account IDs, internal company names, proprietary tags or confidential information.

## Repository Files

aws-backup-cloudformation-lab/
├── templates/
│   └── aws-backup-plan.yaml
├── parameters/
│   └── parameters-demo.json
└── docs/
    └── deployment-guide.md

## Prerequisites

Before deploying, confirm that you have:

- An AWS account for lab or demo purposes.
- AWS CLI installed.
- AWS CLI configured with a valid profile.
- Permissions to create AWS Backup resources.
- Permissions to create IAM roles.
- Permissions to deploy CloudFormation stacks.

## Validate AWS CLI Access

Run:

aws sts get-caller-identity

Expected result:

{
  "UserId": "EXAMPLEUSERID",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/demo-user"
}

Do not commit real AWS account IDs or ARNs to this repository.

## Validate the CloudFormation Template

Run:

aws cloudformation validate-template \
  --template-body file://templates/aws-backup-plan.yaml

## Deploy the Stack

Run:

aws cloudformation deploy \
  --template-file templates/aws-backup-plan.yaml \
  --stack-name demo-aws-backup-stack \
  --parameter-overrides file://parameters/parameters-demo.json \
  --capabilities CAPABILITY_NAMED_IAM

## Important Note About IAM

This template creates an IAM role for AWS Backup.

For that reason, the deployment requires:

--capabilities CAPABILITY_NAMED_IAM

## Backup Resource Selection

This template selects resources for backup using tags.

Only resources with this tag will be included:

Backup = Enabled

Example:

Key: Backup
Value: Enabled

## Backup Schedule

The default schedule is:

cron(0 2 * * ? *)

This means the backup runs every day at 02:00 UTC.

## Retention

Default retention configuration:

| Setting | Value |
|---|---:|
| Move to cold storage after | 7 days |
| Delete recovery point after | 35 days |

## Verify the Deployment

After deployment, validate the following resources in AWS Console:

1. Go to AWS Backup.
2. Open Backup vaults.
3. Confirm that `demo-backup-vault` exists.
4. Open Backup plans.
5. Confirm that `demo-backup-plan` exists.
6. Review the backup rule.
7. Review the tag-based resource selection.
8. Confirm that the IAM role was created.

## Delete the Stack

To remove the demo stack, run:

aws cloudformation delete-stack \
  --stack-name demo-aws-backup-stack

Then check the stack status:

aws cloudformation describe-stacks \
  --stack-name demo-aws-backup-stack

## Operational Validation

After deployment, validate:

- Backup plan exists.
- Backup vault exists.
- IAM role exists.
- Backup selection is configured.
- Target resources have the required tag.
- Backup jobs are running according to schedule.
- Failed or missed backup jobs are reviewed.
- Recovery points follow the defined retention policy.

## Security Notes

Do not upload or commit:

- Real AWS account IDs
- Real ARNs
- Company names
- Customer names
- Internal project names
- Production tags
- Credentials
- Access keys
- Secrets
- Real KMS keys
- Internal documentation

Use only demo values such as:

- demo
- sample
- example
- lab
- test

---

# Guía de Despliegue

## Español

## Objetivo

Esta guía explica cómo desplegar el template demo de AWS Backup con CloudFormation incluido en este repositorio.

El despliegue crea:

- AWS Backup Vault
- AWS Backup Plan
- Regla de backup
- Rol IAM para AWS Backup
- Selección de recursos basada en tags

Este es un laboratorio genérico y anonimizado. No contiene datos reales de producción, IDs reales de cuentas AWS, nombres internos de empresas, tags propietarios ni información confidencial.

## Archivos del Repositorio

aws-backup-cloudformation-lab/
├── templates/
│   └── aws-backup-plan.yaml
├── parameters/
│   └── parameters-demo.json
└── docs/
    └── deployment-guide.md

## Prerrequisitos

Antes de desplegar, confirma que tienes:

- Una cuenta AWS para laboratorio o demostración.
- AWS CLI instalado.
- AWS CLI configurado con un perfil válido.
- Permisos para crear recursos de AWS Backup.
- Permisos para crear roles IAM.
- Permisos para desplegar stacks de CloudFormation.

## Validar Acceso con AWS CLI

Ejecuta:

aws sts get-caller-identity

Resultado esperado:

{
  "UserId": "EXAMPLEUSERID",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/demo-user"
}

No subas ni guardes IDs reales de cuentas AWS o ARNs reales en este repositorio.

## Validar el Template de CloudFormation

Ejecuta:

aws cloudformation validate-template \
  --template-body file://templates/aws-backup-plan.yaml

## Desplegar el Stack

Ejecuta:

aws cloudformation deploy \
  --template-file templates/aws-backup-plan.yaml \
  --stack-name demo-aws-backup-stack \
  --parameter-overrides file://parameters/parameters-demo.json \
  --capabilities CAPABILITY_NAMED_IAM

## Nota Importante sobre IAM

Este template crea un rol IAM para AWS Backup.

Por eso, el despliegue requiere:

--capabilities CAPABILITY_NAMED_IAM

## Selección de Recursos para Backup

Este template selecciona recursos para backup mediante tags.

Solo se incluirán los recursos que tengan este tag:

Backup = Enabled

Ejemplo:

Key: Backup
Value: Enabled

## Programación del Backup

La programación por defecto es:

cron(0 2 * * ? *)

Esto significa que el backup se ejecuta todos los días a las 02:00 UTC.

## Retención

Configuración de retención por defecto:

| Configuración | Valor |
|---|---:|
| Mover a cold storage después de | 7 días |
| Eliminar recovery point después de | 35 días |

## Verificar el Despliegue

Después del despliegue, valida los siguientes recursos en la consola de AWS:

1. Ve a AWS Backup.
2. Abre Backup vaults.
3. Confirma que existe `demo-backup-vault`.
4. Abre Backup plans.
5. Confirma que existe `demo-backup-plan`.
6. Revisa la regla de backup.
7. Revisa la selección de recursos basada en tags.
8. Confirma que el rol IAM fue creado.

## Eliminar el Stack

Para eliminar el stack demo, ejecuta:

aws cloudformation delete-stack \
  --stack-name demo-aws-backup-stack

Luego revisa el estado del stack:

aws cloudformation describe-stacks \
  --stack-name demo-aws-backup-stack

## Validación Operativa

Después del despliegue, valida:

- El backup plan existe.
- El backup vault existe.
- El rol IAM existe.
- La selección de backup está configurada.
- Los recursos objetivo tienen el tag requerido.
- Los jobs de backup se ejecutan según la programación.
- Los jobs fallidos o no ejecutados son revisados.
- Los recovery points cumplen la política de retención definida.

## Notas de Seguridad

No subas ni hagas commit de:

- IDs reales de cuentas AWS
- ARNs reales
- Nombres de empresas
- Nombres de clientes
- Nombres internos de proyectos
- Tags productivos
- Credenciales
- Access keys
- Secrets
- Llaves KMS reales
- Documentación interna

Usa solo valores demo como:

- demo
- sample
- example
- lab
- test
