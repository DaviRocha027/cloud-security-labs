🔐 Lab 02 — IAM & Conditional Access (Microsoft Entra ID)
📌 Objetivo

Implementar e documentar controles de Identidade e Acesso (IAM) utilizando o Microsoft Entra ID, aplicando boas práticas de Zero Trust, Least Privilege e MFA, com foco em cenários corporativos reais.

Este laboratório faz parte da Fase 1 do plano de carreira em Cloud Security.
🧱 Escopo do Lab

Criação e organização de usuários

Gerenciamento de grupos de segurança

Estratégia de controle de acesso baseada em grupos

Validação de métodos de autenticação multifator (MFA)

Desenho conceitual de política de Acesso Condicional
👤 Usuários Criados

Foram criados usuários de teste para simular perfis distintos:

cloud.admin

Perfil: Administrador simulado

cloud.user

Perfil: Usuário padrão

Esses usuários permitem validar estratégias diferentes de acesso e controle.
👥 Grupos de Segurança

Foram criados os seguintes grupos:

cloud-admins

cloud-users

Associação

cloud.admin → cloud-admins

cloud.user → cloud-users

Essa abordagem segue boas práticas de controle de acesso baseado em grupos, evitando atribuições diretas a usuários.
🔐 Autenticação Multifator (MFA)

Os métodos de autenticação foram validados no Microsoft Entra ID, incluindo:

Microsoft Authenticator

Métodos alternativos (quando disponíveis)

O uso de MFA é considerado controle essencial para reduzir riscos de comprometimento de identidade.
🚫 Acesso Condicional — Limitação de Licença

A criação de políticas de Acesso Condicional (Conditional Access) não pôde ser realizada devido à ausência de licenciamento Microsoft Entra ID Premium (P1/P2) na assinatura utilizada.

⚠️ Essa limitação é comum em ambientes corporativos, onde nem todos os tenants possuem licenças premium disponíveis.
📐 Política de Acesso Condicional (Desenho Conceitual)

Mesmo sem a criação técnica da política, foi definido o seguinte desenho de segurança, alinhado às boas práticas:

"Policy Name: require-mfa-for-cloud-admins

Users:
- Included: cloud-admins
- Excluded: break-glass account

Cloud Apps:
- All cloud apps

Conditions:
- Any location

Access Controls:
- Require Multi-Factor Authentication

Mode:
- Report-only (recommended for initial validation)
"

*Decisões de Segurança*

Uso de grupos para simplificar governança de acesso

Separação clara entre usuários administrativos e comuns

MFA como requisito mínimo de segurança

Adoção de Zero Trust (não confiar implicitamente em localização ou usuário)

Consciência de limitações de licenciamento e permissões
*Lições Aprendidas*

Identity é o pilar central da Cloud Security

Conditional Access depende de licenciamento, não apenas de configuração

Ambientes reais possuem restrições que exigem decisões arquiteturais

Documentar o desenho de segurança é tão importante quanto implementá-lo

Grupos são fundamentais para escalar IAM com segurança

======ENGLISH======
🔐 Lab 02 — IAM & Conditional Access (Microsoft Entra ID)
📌 Objective

Implement and document Identity and Access Management (IAM) controls using Microsoft Entra ID, applying Zero Trust, Least Privilege, and MFA best practices in real-world enterprise scenarios.

This lab is part of Phase 1 of the Cloud Security career roadmap.

🧱 Lab Scope

User creation and organization

Security group management

Group-based access control strategy

Multi-Factor Authentication (MFA) validation

Conceptual design of Conditional Access policies

👤 Users Created

Test users were created to simulate different access profiles:

cloud.admin

Role: Simulated administrator

cloud.user

Role: Standard user

These users help validate access control strategies.

👥 Security Groups

The following security groups were created:

cloud-admins

cloud-users

Group Assignment

cloud.admin → cloud-admins

cloud.user → cloud-users

This approach follows group-based access control best practices.

🔐 Multi-Factor Authentication (MFA)

Authentication methods were validated within Microsoft Entra ID, including:

Microsoft Authenticator

Alternative methods (when available)

MFA is considered a baseline security control to reduce identity compromise risks.

🚫 Conditional Access — Licensing Limitation

The creation of Conditional Access policies was not possible due to the lack of Microsoft Entra ID Premium (P1/P2) licensing in the tenant.

*This limitation is common in enterprise environments, where premium licenses may be restricted.*

*Conditional Access Policy (Conceptual Design)*

Even without technical implementation, the following security policy design was defined according to best practices:

"Policy Name: require-mfa-for-cloud-admins

Users:
- Included: cloud-admins
- Excluded: break-glass account

Cloud Apps:
- All cloud apps

Conditions:
- Any location

Access Controls:
- Require Multi-Factor Authentication

Mode:
- Report-only (recommended for initial validation)
"

*Security Decisions*

Group-based identity management

Clear separation between admin and standard users

MFA as a mandatory security layer

Zero Trust mindset

Awareness of licensing and permission constraints

*Lessons Learned*

Identity is the core pillar of Cloud Security

Conditional Access requires proper licensing

Real environments involve organizational constraints

Security design documentation is as important as implementation

Groups are essential for scalable IAM governance

