---
description: 'Saiba mais sobre: ServiceAuthorizationBehavior'
title: ServiceAuthorizationBehavior
ms.date: 03/30/2017
ms.assetid: 77dad8e8-fea4-4d1c-b366-2f01a2a87f78
ms.openlocfilehash: dc398621103774a04934aa23ae3d7208f4389717
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715581"
---
# <a name="serviceauthorizationbehavior"></a>ServiceAuthorizationBehavior

ServiceAuthorizationBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceAuthorizationBehavior : Behavior  
{  
  boolean ImpersonateCallerForAllOperations;  
  string PrincipalPermissionMode;  
  string RoleProvider;  
  string ServiceAuthorizationManager;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceAuthorizationBehavior não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceAuthorizationBehavior tem as seguintes propriedades:  
  
### <a name="impersonatecallerforalloperations"></a>ImpersonateCallerForAllOperations  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que controla se o serviço tenta representar usando as credenciais fornecidas pela mensagem de entrada.  
  
### <a name="principalpermissionmode"></a>PrincipalPermissionMode  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A entidade de segurança usada para executar operações no servidor.  
  
### <a name="roleprovider"></a>RoleProvider  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome do provedor de função ASP.NET.  
  
### <a name="serviceauthorizationmanager"></a>Objectauthorizationmanager  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O Gerenciador de autorização usado para autorização personalizada.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
