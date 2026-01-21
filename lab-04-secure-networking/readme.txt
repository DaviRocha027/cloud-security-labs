# 🧪 Lab 04 — Secure Networking (Azure NSG & Network Segmentation)

## 📌 Objetivo
Projetar e implementar uma **arquitetura de rede segura no Microsoft Azure**, aplicando boas práticas de **segmentação**, **default deny** e **Zero Trust** no nível de rede, utilizando **Network Security Groups (NSG)**.

Este laboratório demonstra como reduzir a superfície de ataque através do controle explícito de fluxos entre camadas da aplicação.

---

## 🧱 Arquitetura do Lab

- **Resource Group:** rg-lab-04-secure-networking
- **Virtual Network:** vnet-secure-lab04
- **Address Space:** 10.10.0.0/16

### Subnets
| Subnet | CIDR | Finalidade |
|------|------|-----------|
| subnet-mgmt | 10.10.1.0/24 | Gerenciamento |
| subnet-app | 10.10.2.0/24 | Aplicação |
| subnet-data | 10.10.3.0/24 | Dados |

---

## 🔐 Network Security Groups (NSG)

Foram criados **NSGs dedicados por subnet**, garantindo isolamento lógico entre camadas.

### NSG — subnet-mgmt
- Apenas regras padrão
- Nenhuma exposição externa
- Gerenciamento não acessível pela Internet

### NSG — subnet-app
**Inbound**
- Allow: tráfego interno da VNet
- Deny: todo o restante (default deny)

**Outbound**
- Allow: VNet e Internet
- Deny: todo o restante

### NSG — subnet-data
**Inbound**
- Allow: tráfego proveniente da camada de aplicação
- Deny: todo o restante

**Outbound**
- Allow: tráfego interno necessário
- Deny: todo o restante

---

## 🔍 Validação Conceitual de Fluxo

- ❌ Internet → Mgmt: Bloqueado
- ❌ Internet → App: Bloqueado
- ❌ Internet → Data: Bloqueado
- ✔ Mgmt → App: Permitido
- ✔ App → Data: Permitido

Mesmo sem workloads (VMs), a **arquitetura comprova o controle de tráfego**.

---

## 🔐 Decisões de Segurança Aplicadas

- Segmentação por função
- Default deny como padrão
- Isolamento de camada de dados
- Redução da superfície de ataque
- Aplicação de princípios Zero Trust (network layer)

---

## 📚 Lições Aprendidas

- NSGs são avaliados por prioridade
- Regras padrão já implementam default deny
- Separar NSGs por subnet melhora governança
- Segurança de rede começa no design

---

## ✅ Status do Lab
✔ Concluído com sucesso  
✔ Arquitetura segura validada  
✔ Pronto para portfólio  

---

English

# 🧪 Lab 04 — Secure Networking (Azure NSG & Network Segmentation)

## 📌 Objective
Design and implement a **secure network architecture in Microsoft Azure**, applying **segmentation**, **default deny**, and **Zero Trust** principles at the network layer using **Network Security Groups (NSG)**.

This lab demonstrates how to reduce the attack surface through explicit traffic control between application layers.

---

## 🧱 Lab Architecture

- **Resource Group:** rg-lab-04-secure-networking
- **Virtual Network:** vnet-secure-lab04
- **Address Space:** 10.10.0.0/16

### Subnets
| Subnet | CIDR | Purpose |
|------|------|---------|
| subnet-mgmt | 10.10.1.0/24 | Management |
| subnet-app | 10.10.2.0/24 | Application |
| subnet-data | 10.10.3.0/24 | Data |

---

## 🔐 Network Security Groups (NSG)

Dedicated NSGs were created per subnet to enforce **layered security**.

### NSG — subnet-mgmt
- Default rules only
- No external exposure
- Management layer not accessible from the Internet

### NSG — subnet-app
**Inbound**
- Allow: traffic from inside the VNet
- Deny: all other traffic (default deny)

**Outbound**
- Allow: VNet and Internet
- Deny: all other traffic

### NSG — subnet-data
**Inbound**
- Allow: traffic from the application layer
- Deny: all other traffic

**Outbound**
- Allow: required internal traffic
- Deny: all other traffic

---

## 🔍 Conceptual Traffic Validation

- ❌ Internet → Mgmt: Blocked
- ❌ Internet → App: Blocked
- ❌ Internet → Data: Blocked
- ✔ Mgmt → App: Allowed
- ✔ App → Data: Allowed

Even without workloads, the **network design validates the security model**.

---

## 🔐 Security Decisions

- Function-based segmentation
- Default deny enforced
- Data layer isolation
- Reduced attack surface
- Zero Trust applied at network level

---

## 📚 Lessons Learned

- NSGs are evaluated by priority
- Default rules already enforce deny-all
- Per-subnet NSGs improve governance
- Network security starts at the design phase

---

## ✅ Lab Status
✔ Successfully completed  
✔ Secure architecture validated  
✔ Portfolio-ready  

---

