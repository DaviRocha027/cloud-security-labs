# 🔥 Lab 03 – Azure Firewall (Inbound/Outbound Control)

---

## 🇧🇷 Versão em Português (PT-BR)

## 📌 Visão Geral

Este laboratório demonstra a implantação e validação do **Azure Firewall** como camada central de controle de tráfego **inbound/outbound** em uma arquitetura com **sub-rede de workload** e **sub-rede de jump host**.

O foco é garantir que **todo o tráfego de saída (egress)** da sub-rede de workload passe obrigatoriamente pelo firewall, aplicando regras **Application** (FQDN) e **Network** (DNS).

Região utilizada: **East US**

---

## 🎯 Objetivos Técnicos

- Implantar o ambiente via **ARM template** (`template.json`)
- Implementar **Azure Firewall (SKU Standard)**
- Criar **rota default (0.0.0.0/0)** para forçar egress via firewall
- Configurar **Application Rule** permitindo apenas `www.bing.com` (HTTP/HTTPS)
- Configurar **Network Rule** permitindo consultas DNS externas (UDP/53)
- Configurar DNS customizado na NIC do workload para validar a regra de DNS
- Testar acesso permitido e bloqueado (allow/deny) via navegação web

---

## 🛠️ Tecnologias Utilizadas

- Microsoft Azure
- Azure Firewall (Standard) — Rules (classic)
- Azure Virtual Network (VNet), Subnets
- Route Table (UDR) / Custom Routes
- ARM Template Deployment
- Windows Server VMs (Jump + Workload)
- RDP (Remote Desktop)
- DNS (UDP/53)

---

## 🧪 Descrição das Atividades

### 🔹 Exercise 1 – Deploy e Teste do Azure Firewall

#### ✔ Task 1 – Deploy do ambiente via template (ARM)

- Template: `\Allfiles\Labs\08\template.json`
- Resource Group: `AZ500LAB08`
- Região: East US
- Observação: o template provisiona VNet e VMs (ex.: `Srv-Jump` e `Srv-Work`) e recursos associados.

---

#### ✔ Task 2 – Implantação do Azure Firewall

- Firewall: `Test-FW01`
- SKU: Standard
- Management: **Use Firewall rules (classic)**
- VNet existente: `Test-FW-VN`
- Public IP: `TEST-FW-PIP`
- Ação crítica: anotar o **Private IP** do firewall (usado na rota default).

---

#### ✔ Task 3 – Default Route (forçar egress via firewall)

- Route Table: `Firewall-route`
- Associada à Subnet: `Workload-SN` (essencial para o funcionamento)
- Rota criada:
  - Route name: `FW-DG`
  - Destination: `0.0.0.0/0`
  - Next hop type: `Virtual appliance`
  - Next hop address: **Private IP do Azure Firewall**

Resultado esperado: tráfego outbound da `Workload-SN` passa pelo firewall.

---

#### ✔ Task 4 – Application Rule (permitir apenas bing.com)

Rule Collection (Application):
- Name: `App-Coll01`
- Priority: `200`
- Action: `Allow`

Rule (Target FQDNs):
- Name: `AllowGH`
- Source: `10.0.2.0/24` (Workload subnet)
- Protocols: `http:80`, `https:443`
- Target FQDNs: `www.bing.com`

---

#### ✔ Task 5 – Network Rule (permitir DNS externo)

Rule Collection (Network):
- Name: `Net-Coll01`
- Priority: `200`
- Action: `Allow`

Rule:
- Name: `AllowDNS`
- Protocol: `UDP`
- Source: `10.0.2.0/24`
- Destination IPs: `209.244.0.3, 209.244.0.4`
- Destination Port: `53`

---

#### ✔ Task 6 – Configurar DNS na NIC do Workload

Na NIC da VM `Srv-Work`:
- DNS Servers: **Custom**
- Primary/Secondary: `209.244.0.3` e `209.244.0.4`
- Observação: a alteração reinicia automaticamente a VM.

Objetivo: garantir que a resolução DNS use os endereços permitidos pela regra de rede.

---

#### ✔ Task 7 – Testes (Allow/Deny)

Fluxo de acesso:
1. RDP em `Srv-Jump`
2. De `Srv-Jump`, RDP em `Srv-Work` (`mstsc /v:Srv-Work`)
3. Desabilitar IE Enhanced Security (para facilitar o teste)
4. Testar navegação:

✅ Permitido:
- `https://www.bing.com` (deve abrir)

❌ Bloqueado:
- `http://www.microsoft.com/` (deve negar, pois não há regra permitindo)

Mensagem esperada no bloqueio (conceito):
- **Action: Deny. No rule matched.**

---

## 🔐 Conceitos de Segurança Aplicados

- Centralização de controle de tráfego com **Azure Firewall**
- Egress control via **UDR (0.0.0.0/0)** forçando rota pelo firewall
- **Application rules** por FQDN (camada 7) para restringir destinos web
- **Network rules** (camada 3/4) para permitir DNS externo específico
- Princípio do **menor privilégio** aplicado a tráfego de saída

---

## ✅ Resultado

O laboratório valida que:

- O tráfego outbound da sub-rede de workload é forçado pelo firewall
- Apenas `www.bing.com` é permitido via regras de aplicação
- Consultas DNS externas são permitidas apenas para os IPs liberados
- Qualquer destino não previsto é bloqueado por padrão

---

## 🧹 Cleanup (Remoção de Recursos)

```powershell
Remove-AzResourceGroup -Name "AZ500LAB08" -Force -AsJob
```

---

## 📚 Referência

Material base: **Lab 03 – Azure Firewall (Student Lab Manual)**

---

---

## 🇺🇸 English Version (EN)

## 📌 Overview

This lab demonstrates the deployment and validation of **Azure Firewall** as a centralized layer to control **inbound and outbound** traffic in a design with a **workload subnet** and a **jump host subnet**.

The key goal is to enforce that **all workload egress traffic** must traverse the firewall, using **Application** (FQDN) and **Network** (DNS) rules.

Region used: **East US**

---

## 🎯 Technical Objectives

- Deploy the lab environment using an **ARM template** (`template.json`)
- Deploy **Azure Firewall (Standard SKU)**
- Create a **default route (0.0.0.0/0)** to force egress through the firewall
- Configure an **Application Rule** allowing only `www.bing.com` (HTTP/HTTPS)
- Configure a **Network Rule** allowing external DNS lookups (UDP/53)
- Configure custom DNS servers on the workload NIC to validate DNS rule enforcement
- Test allowed and denied traffic scenarios via web browsing

---

## 🛠️ Technologies Used

- Microsoft Azure
- Azure Firewall (Standard) — Rules (classic)
- Azure Virtual Network (VNet), Subnets
- Route Table (UDR) / Custom Routes
- ARM Template Deployment
- Windows Server VMs (Jump + Workload)
- RDP (Remote Desktop)
- DNS (UDP/53)

---

## 🧪 Lab Activities Breakdown

### 🔹 Exercise 1 – Deploy and Test Azure Firewall

#### ✔ Task 1 – Deploy environment via ARM template

- Template: `\Allfiles\Labs\08\template.json`
- Resource Group: `AZ500LAB08`
- Region: East US
- Note: Template provisions VNet + VMs (e.g., `Srv-Jump`, `Srv-Work`) and required resources.

---

#### ✔ Task 2 – Deploy Azure Firewall

- Firewall: `Test-FW01`
- SKU: Standard
- Management: **Use Firewall rules (classic)**
- Existing VNet: `Test-FW-VN`
- Public IP: `TEST-FW-PIP`
- Critical step: record the firewall **Private IP** (used in the default route).

---

#### ✔ Task 3 – Default Route (force egress through firewall)

- Route Table: `Firewall-route`
- Associated Subnet: `Workload-SN` (mandatory for correct behavior)
- Route:
  - Route name: `FW-DG`
  - Destination: `0.0.0.0/0`
  - Next hop type: `Virtual appliance`
  - Next hop address: **Azure Firewall private IP**

Expected outcome: workload outbound traffic is routed through the firewall.

---

#### ✔ Task 4 – Application Rule (allow only bing.com)

Application Rule Collection:
- Name: `App-Coll01`
- Priority: `200`
- Action: `Allow`

Rule (Target FQDNs):
- Name: `AllowGH`
- Source: `10.0.2.0/24`
- Protocols: `http:80`, `https:443`
- Target FQDNs: `www.bing.com`

---

#### ✔ Task 5 – Network Rule (allow external DNS)

Network Rule Collection:
- Name: `Net-Coll01`
- Priority: `200`
- Action: `Allow`

Rule:
- Name: `AllowDNS`
- Protocol: `UDP`
- Source: `10.0.2.0/24`
- Destination IPs: `209.244.0.3, 209.244.0.4`
- Destination Port: `53`

---

#### ✔ Task 6 – Configure DNS servers on Workload NIC

On `Srv-Work` NIC:
- DNS Servers: **Custom**
- Primary/Secondary: `209.244.0.3` and `209.244.0.4`
- Note: NIC DNS update triggers VM restart.

Goal: ensure DNS resolution uses the IPs explicitly allowed by the firewall network rule.

---

#### ✔ Task 7 – Testing (Allow/Deny)

Access flow:
1. RDP to `Srv-Jump`
2. From `Srv-Jump`, RDP to `Srv-Work` (`mstsc /v:Srv-Work`)
3. Disable IE Enhanced Security (for testing)
4. Browser tests:

✅ Allowed:
- `https://www.bing.com` (should load)

❌ Blocked:
- `http://www.microsoft.com/` (should be denied; no matching rule)

Expected deny concept:
- **Action: Deny. No rule matched.**

---

## 🔐 Security Concepts Applied

- Centralized traffic control using **Azure Firewall**
- Egress control via **UDR (0.0.0.0/0)** forcing route to firewall
- **Application rules** (L7) using FQDN allow-listing
- **Network rules** (L3/L4) to permit specific external DNS resolvers
- **Least privilege** applied to outbound traffic

---

## ✅ Outcome

This lab validates that:

- Workload subnet egress is forced through Azure Firewall
- Only `www.bing.com` is allowed by application rules
- DNS queries are allowed only to approved external resolvers
- Any non-explicit destination is denied by default

---

## 🧹 Cleanup

```powershell
Remove-AzResourceGroup -Name "AZ500LAB08" -Force -AsJob
```

---

## 📚 Reference

Base material: **Lab 03 – Azure Firewall (Student Lab Manual)**

---

Author: Davi Rocha Cardozo  
Focus: Azure Security / AZ-500 Lab Practice
