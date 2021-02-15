---
description: 'Saiba mais sobre: classe de operação'
title: Classe de operação
ms.date: 03/30/2017
ms.assetid: b19d1496-ef06-4d0c-b2ae-e728ec00cca0
ms.openlocfilehash: 035c02bc05b7a64c5d15538001dbdcf2ec0b135b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803068"
---
# <a name="operation-class"></a>Classe de operação

Operação  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class Operation  
{  
  string Action;  
  boolean AsyncPattern;  
  Behavior Behaviors[];  
  boolean IsCallback;  
  boolean IsInitiating;  
  boolean IsOneWay;  
  boolean IsTerminating;  
  string MethodSignature;  
  string Name;  
  string ParameterTypes[];  
  string ReplyAction;  
  string ReturnType;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe Operation não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe Operation tem as seguintes propriedades:  
  
### <a name="action"></a>Ação  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A ação de WS-Addressing da mensagem de solicitação.  
  
### <a name="asyncpattern"></a>AsyncPattern  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica que uma operação é implementada de forma assíncrona usando um `Begin` par de método [colchetes de abertura/fechamento] e `End` [colchetes de abertura/fechamento] em um contrato de serviço.  
  
### <a name="behaviors"></a>Comportamentos  

 Tipo de dados: matriz de comportamento  
  
 Tipo de acesso: Somente leitura  
  
 Os comportamentos associados a esta operação.  
  
### <a name="iscallback"></a>IsCallback  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 True quando a operação for uma operação de retorno de chamada.  
  
### <a name="isinitiating"></a>IsInitiating  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se o método implementa uma operação que pode iniciar uma sessão no servidor.  
  
### <a name="isoneway"></a>IsOneWay  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se uma operação retorna uma mensagem de resposta.  
  
### <a name="isterminating"></a>IsTerminating  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se uma operação retorna uma mensagem de resposta.  
  
### <a name="methodsignature"></a>MethodSignature  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A assinatura do método da operação.  
  
### <a name="name"></a>Nome  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome da operação.  
  
### <a name="parametertypes"></a>ParameterTypes  

 Tipo de dados: matriz de cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Os tipos dos parâmetros da operação.  
  
### <a name="replyaction"></a>ReplyAction  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O valor da ação SOAP para a mensagem de resposta da operação.  
  
### <a name="returntype"></a>Tipoderetorno  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O tipo de retorno da operação.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.OperationDescription>
