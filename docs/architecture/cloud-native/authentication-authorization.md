---
title: Autenticação e autorização em aplicativos nativos de nuvem
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Autenticação e autorização em aplicativos nativos de nuvem
ms.date: 05/13/2020
ms.openlocfilehash: bbd2df110dd7a7dc7363e9c07d87f1fa12f4e464
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91161133"
---
# <a name="authentication-and-authorization-in-cloud-native-apps"></a>Autenticação e autorização nos aplicativos nativos de nuvem

A *autenticação* é o processo de determinar a identidade de uma entidade de segurança. A *autorização* é o ato de conceder uma permissão de entidade autenticada para executar uma ação ou acessar um recurso. Às vezes, a autenticação é reduzida para `AuthN` e a autorização é reduzida para `AuthZ` . Os aplicativos nativos de nuvem precisam contar com protocolos abertos baseados em HTTP para autenticar entidades de segurança, já que os clientes e aplicativos podem estar em execução em qualquer lugar do mundo em qualquer plataforma ou dispositivo. O único fator comum é HTTP.

Muitas organizações ainda dependem de serviços de autenticação local como o Serviços de Federação do Active Directory (AD FS) (ADFS). Embora essa abordagem tradicionalmente tenha atendido às organizações para as necessidades de autenticação local, os aplicativos nativos de nuvem se beneficiam de sistemas projetados especificamente para a nuvem. Uma recente consultoria de 2019 do Reino Unido National Cyber Security Centre (NCSC) informa que "as organizações que usam o Azure AD como sua fonte de autenticação primária reduzirão seu risco em comparação com o ADFS". Alguns motivos descritos nesta [análise](https://oxfordcomputergroup.com/resources/o365-security-native-cloud-authentication/) incluem:

- Acesso ao conjunto completo de tecnologias de proteção de credenciais da Microsoft.
- A maioria das organizações já confia no Azure AD até certo ponto.
- O hash duplo de hashes NTLM garante que o comprometimento não permitirá credenciais que funcionem no Active Directory local.

## <a name="references"></a>Referências

- [Noções básicas de autenticação](/azure/active-directory/develop/authentication-scenarios)
- [Tokens e declarações de acesso](/azure/active-directory/develop/access-tokens)
- [Pode ser hora de eliminar seus serviços de autenticação locais](https://oxfordcomputergroup.com/resources/o365-security-native-cloud-authentication/)

>[!div class="step-by-step"]
>[Anterior](identity.md) 
> [Avançar](azure-active-directory.md)
