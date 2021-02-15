---
description: 'Saiba mais sobre: não AppDomain'
title: ServiceAppDomain
ms.date: 03/30/2017
ms.assetid: f28e5186-a66d-46c1-abe9-b50e07f8cb4f
ms.openlocfilehash: 1ac32b1fbd88518ffb260be9dd3ed2adb88d211c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715633"
---
# <a name="serviceappdomain"></a>ServiceAppDomain

Mapeia um serviço para um domínio de aplicativo.  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceAppDomain  
{  
  Service ref;  
  AppDomainInfo ref;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe imappdomain não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe imappdomain tem as seguintes propriedades:  
  
### <a name="ref"></a>ref  

 Tipo de dados: serviço  
Qualificadores: Chave  
  
 Tipo de acesso: Somente leitura  
  
 O serviço deste domínio de aplicativo.  
  
### <a name="ref"></a>ref  

 Tipo de dados: AppDomainInfo  
Qualificadores: Chave  
  
 Tipo de acesso: Somente leitura  
  
 Contém as propriedades do domínio do aplicativo.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|
