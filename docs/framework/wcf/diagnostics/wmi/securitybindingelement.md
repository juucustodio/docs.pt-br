---
description: 'Saiba mais sobre: SecurityBindingElement'
title: SecurityBindingElement
ms.date: 03/30/2017
ms.assetid: ef93b6e6-3524-48a8-94d3-c8837f1872f9
ms.openlocfilehash: bc9a519978a9cccccd80a58abb8d109fa9bc9337
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743805"
---
# <a name="securitybindingelement"></a>SecurityBindingElement

SecurityBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class SecurityBindingElement : BindingElement  
{  
  string DefaultAlgorithmSuite;  
  boolean IncludeTimestamp;  
  string KeyEntropyMode;  
  LocalServiceSecuritySettings LocalServiceSecuritySettings;  
  string MessageSecurityVersion;  
  string SecurityHeaderLayout;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe SecurityBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe SecurityBindingElement tem as seguintes propriedades:  
  
### <a name="defaultalgorithmsuite"></a>DefaultAlgorithmSuite  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Especifica os algoritmos a serem usados com a associação.  
  
### <a name="includetimestamp"></a>IncludeTimestamp  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se cada mensagem contém um carimbo de data/hora.  
  
### <a name="keyentropymode"></a>Keyentropiamode  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A fonte de entropia usada para criar chaves.  
  
### <a name="localservicesecuritysettings"></a>LocalServiceSecuritySettings  

 Tipo de dados: LocalServiceSecuritySettings  
  
 Tipo de acesso: Somente leitura  
  
 As propriedades de segurança específicas de associação para o serviço local.  
  
### <a name="messagesecurityversion"></a>MessageSecurityVersion  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A versão usada para segurança de mensagem.  
  
### <a name="securityheaderlayout"></a>SecurityHeaderLayout  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A ordem dos elementos no cabeçalho de segurança para essa associação.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.SecurityBindingElement>
