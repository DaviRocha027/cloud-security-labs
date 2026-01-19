# 🧪 Lab 03 — Logging & Monitoring (Azure Monitor + Log Analytics)

 🇧🇷 Português

 Objetivo
Implementar e validar a centralização de logs no Azure utilizando Azure Monitor e Log Analytics, com foco em auditoria, segurança e observabilidade.

Escopo
- Log Analytics Workspace
- Diagnostic Settings no nível da Subscription
- Consultas KQL (AzureActivity)

A ingestão de logs foi validada com sucesso através da consulta:
```kql
AzureActivity
| limit 10
```

## 🇺🇸 English

Objective
Implement and validate centralized logging in Azure using Azure Monitor and Log Analytics, focusing on auditability, security, and observability.

 Scope
- Log Analytics Workspace
- Subscription-level Diagnostic Settings
- KQL queries (AzureActivity)


Log ingestion was successfully validated using:
```kql
AzureActivity
| limit 10
```
