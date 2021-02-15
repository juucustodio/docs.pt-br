---
description: 'Saiba mais sobre: ServiceSecurityAuditBehavior'
title: ServiceSecurityAuditBehavior
ms.date: 03/30/2017
ms.assetid: 2c5809e7-5364-44ce-bc71-848be4672e2a
ms.openlocfilehash: 5dfb3a70a80d5dea1ed360dcaf3a0db989bf671b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715464"
---
# <a name="servicesecurityauditbehavior"></a>ServiceSecurityAuditBehavior

ServiceSecurityAuditBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp  
class ServiceSecurityAuditBehavior : Behavior  
{  
  string AuditLogLocation;  
  string MessageAuthenticationAuditLevel;  
  string ServiceAuthorizationAuditLevel;  
  boolean SuppressAuditFailure;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceSecurityAuditBehavior não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceSecurityAuditBehavior tem as seguintes propriedades:  
  
### <a name="auditloglocation"></a>AuditLogLocation  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O local do log de auditoria.  
  
### <a name="messageauthenticationauditlevel"></a>MessageAuthenticationAuditLevel  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O tipo de nível de autenticação de mensagem que é usado para registrar em log eventos de auditoria.  
  
### <a name="serviceauthorizationauditlevel"></a>ServiceAuthorizationAuditLevel  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Os tipos de eventos de autorização que são registrados no log de auditoria.  
  
### <a name="suppressauditfailure"></a>SuppressAuditFailure  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica o comportamento para suprimir falhas de gravação no log de auditoria.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
