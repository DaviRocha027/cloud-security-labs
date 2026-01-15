Lab 01 — Azure Security Baseline

📌 Objetivo
Implementar uma base segura no Microsoft Azure aplicando boas práticas de Cloud Security.

 🧱 Arquitetura
- Resource Group: rg-sec-baseline
- VNet: vnet-sec (10.0.0.0/16)
- Subnets:
  - subnet-mgmt (10.0.1.0/24)
  - subnet-workload (10.0.2.0/24)
- NSG: nsg-sec-baseline (default deny)
- Log Analytics Workspace: law-sec-baseline (East US)

 🔐 RBAC
- Role: Reader
- Scope: Resource Group
- Principle: Least Privilege

 📊 Logs
Workspace criado com sucesso.
Envio de Activity Logs não concluído por limitação de permissão na assinatura.

 📚 Lessons Learned
- RG não impõe região
- Logs são nível de assinatura
- Segurança começa na arquitetura

---

====ENGLISH VERSION====

 Objective
Implement a secure Azure baseline following cloud security best practices.

 Architecture
- Resource Group: rg-sec-baseline
- VNet: vnet-sec
- Subnets: mgmt and workload
- NSG enforcing default deny
- Log Analytics Workspace

 Access Control
- Reader role at resource group scope

 Logging
Workspace validated.
Subscription activity logs limited by permissions.

 Lessons Learned
- Resource groups are logical containers
- Activity logs are subscription-level
- Security starts with design
