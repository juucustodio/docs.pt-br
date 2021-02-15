---
description: 'Saiba mais sobre: LocalServiceSecuritySettings'
title: LocalServiceSecuritySettings
ms.date: 03/30/2017
ms.assetid: 490aa0e5-5242-4f8d-b505-5ec6287633b4
ms.openlocfilehash: f7220e8253c6ab218414c1be7ed90e5d593b4692
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743935"
---
# <a name="localservicesecuritysettings"></a>LocalServiceSecuritySettings

LocalServiceSecuritySettings  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class LocalServiceSecuritySettings  
{  
  boolean DetectReplays;  
  datetime InactivityTimeout;  
  datetime IssuedCookieLifetime;  
  sint32 MaxCachedCookies;  
  datetime MaxClockSkew;  
  sint32 MaxPendingSessions;  
  sint32 MaxStatefulNegotiations;  
  datetime NegotiationTimeout;  
  boolean ReconnectTransportOnFailure;  
  sint32 ReplayCacheSize;  
  datetime ReplayWindow;  
  datetime SessionKeyRenewalInterval;  
  datetime SessionKeyRolloverInterval;  
  datetime TimestampValidityDuration;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe LocalServiceSecuritySettings não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe LocalServiceSecuritySettings tem as seguintes propriedades:  
  
### <a name="detectreplays"></a>DetectReplays  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se os ataques de repetição no canal são detectados e tratados automaticamente.  
  
### <a name="inactivitytimeout"></a>InactivityTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de sessões de segurança pendentes às quais o serviço dá suporte.  
  
### <a name="issuedcookielifetime"></a>IssuedCookieLifetime  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica o tempo de vida emitido para todos os novos cookies de segurança.  
  
### <a name="maxcachedcookies"></a>MaxCachedCookies  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de cookies que podem ser armazenados em cache.  
  
### <a name="maxclockskew"></a>MaxClockSkew  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica a diferença máxima de tempo entre os relógios do sistema das duas partes que se comunicam.  
  
### <a name="maxpendingsessions"></a>MaxPendingSessions  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de conexões pendentes no serviço.  
  
### <a name="maxstatefulnegotiations"></a>MaxStatefulNegotiations  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número de negociações de segurança que podem estar ativas simultaneamente.  
  
### <a name="negotiationtimeout"></a>NegotiationTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica a duração máxima da fase de negociação de segurança entre o servidor e o cliente.  
  
### <a name="reconnecttransportonfailure"></a>ReconnectTransportOnFailure  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se as conexões que usam WS-Reliable sistema de mensagens tentam se reconectar após falhas de transporte.  
  
### <a name="replaycachesize"></a>ReplayCacheSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número de nonces em cache usados para detecção de reprodução.  
  
### <a name="replaywindow"></a>ReplayWindow  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica a duração em que os nonces de mensagem individuais são válidos.  
  
### <a name="sessionkeyrenewalinterval"></a>SessionKeyRenewalInterval  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica a duração após a qual o iniciador renova a chave para a sessão de segurança.  
  
### <a name="sessionkeyrolloverinterval"></a>SessionKeyRolloverInterval  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica o intervalo de tempo que uma chave de sessão anterior é válida em mensagens de entrada durante uma renovação de chave.  
  
### <a name="timestampvalidityduration"></a>TimestampValidityDuration  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 Um TimeSpan que especifica a duração em que um carimbo de data/hora é válido.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
