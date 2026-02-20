# 🔐 Lab 02 -- Network Security Groups (NSG) & Application Security Groups (ASG) on Azure

------------------------------------------------------------------------

## 🇧🇷 Versão em Português (PT-BR)

## 📌 Visão Geral

Este laboratório demonstra a implementação prática de segmentação de
rede e controle de tráfego no Microsoft Azure utilizando:

-   Virtual Network (VNet)
-   Sub-rede
-   Network Security Group (NSG)
-   Application Security Groups (ASG)
-   Máquinas Virtuais Windows Server

Objetivo: validar controle de acesso baseado em regras de rede aplicando
o princípio do menor privilégio entre servidores Web e servidores de
Gerenciamento.

Região utilizada: **East US**

------------------------------------------------------------------------

## 🎯 Objetivos Técnicos

-   Criar Virtual Network com sub-rede dedicada
-   Criar dois Application Security Groups (Web e Management)
-   Criar e associar Network Security Group
-   Configurar regras de entrada (Inbound Rules)
-   Implantar máquinas virtuais
-   Associar NICs aos respectivos ASGs
-   Validar filtragem de tráfego (RDP e HTTP/HTTPS)

------------------------------------------------------------------------

## 🛠️ Tecnologias Utilizadas

-   Microsoft Azure
-   Azure Virtual Network
-   Azure Network Security Group (NSG)
-   Azure Application Security Group (ASG)
-   Windows Server 2022
-   PowerShell

------------------------------------------------------------------------

## 🧪 Descrição das Atividades

### 🔹 Exercise 1 -- Infraestrutura de Rede

✔ Virtual Network: `myVirtualNetwork`\
✔ Address Space: `10.0.0.0/16`\
✔ Sub-rede: `10.0.0.0/24`

✔ ASGs criados: - `myAsgWebServers` - `myAsgMgmtServers`

✔ NSG criado: `myNsg`\
✔ Associado à sub-rede `default`

### 🔐 Regras de Entrada

**Allow-Web-All** - Destino: ASG `myAsgWebServers` - Protocolo: TCP -
Portas: 80,443 - Prioridade: 100 - Ação: Allow

**Allow-RDP-All** - Destino: ASG `myAsgMgmtServers` - Protocolo: TCP -
Porta: 3389 - Prioridade: 110 - Ação: Allow

------------------------------------------------------------------------

### 🔹 Exercise 2 -- Máquinas Virtuais

✔ Web Server -- `myVMWeb` - Windows Server 2022 - Standard D2s v3 -
Associado ao ASG Web

Instalação do IIS:

``` powershell
Install-WindowsFeature -Name Web-Server -IncludeManagementTools
```

✔ Management Server -- `myVMMgmt` - Windows Server 2022 - Standard D2s
v3 - Associado ao ASG de Gerenciamento

------------------------------------------------------------------------

## 🧪 Validação

✔ RDP permitido apenas para `myVMMgmt`\
✔ RDP bloqueado para `myVMWeb`\
✔ Acesso HTTP exibindo página padrão do IIS\
✔ Segmentação validada com sucesso

------------------------------------------------------------------------

## 🔐 Conceitos de Segurança Aplicados

-   Network segmentation
-   Application Security Groups (abstração lógica)
-   NSG associado à sub-rede
-   Princípio do menor privilégio
-   Separação entre camada Web e Gerenciamento

------------------------------------------------------------------------

## 🇺🇸 English Version (EN)

## 📌 Overview

This lab demonstrates practical implementation of network segmentation
and traffic filtering in Microsoft Azure using:

-   Virtual Network (VNet)
-   Subnet
-   Network Security Group (NSG)
-   Application Security Groups (ASG)
-   Windows Server Virtual Machines

Objective: validate inbound filtering between Web and Management tiers
following the Principle of Least Privilege.

Region used: **East US**

------------------------------------------------------------------------

## 🎯 Technical Objectives

-   Deploy a Virtual Network with dedicated subnet
-   Create two Application Security Groups
-   Create and associate Network Security Group
-   Configure inbound security rules
-   Deploy virtual machines
-   Associate NICs to ASGs
-   Validate traffic filtering (RDP and HTTP/HTTPS)

------------------------------------------------------------------------

## 🛠️ Technologies Used

-   Microsoft Azure
-   Azure Virtual Network
-   Azure Network Security Group (NSG)
-   Azure Application Security Group (ASG)
-   Windows Server 2022
-   PowerShell

------------------------------------------------------------------------

## 🧪 Lab Breakdown

### 🔹 Exercise 1 -- Networking Infrastructure

-   VNet: `myVirtualNetwork`
-   Address Space: `10.0.0.0/16`
-   Subnet: `10.0.0.0/24`
-   NSG: `myNsg` (Associated at subnet level)

Inbound Rules:

**Allow-Web-All** - Destination: `myAsgWebServers` - TCP 80,443 -
Priority 100

**Allow-RDP-All** - Destination: `myAsgMgmtServers` - TCP 3389 -
Priority 110

------------------------------------------------------------------------

### 🔹 Exercise 2 -- Virtual Machines

✔ Web Server -- `myVMWeb` ✔ Management Server -- `myVMMgmt`

IIS installed via PowerShell command.

------------------------------------------------------------------------

## 🧪 Validation

-   RDP allowed only to Management Server
-   RDP blocked to Web Server
-   HTTP access successfully displayed IIS default page
-   NSG + ASG integration validated

------------------------------------------------------------------------

Author: Davi Rocha Cardozo\
Focus: Azure Security / AZ-500 Lab Practice
