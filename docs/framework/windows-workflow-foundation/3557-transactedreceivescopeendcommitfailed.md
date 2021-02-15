---
description: 'Saiba mais sobre: 3557-TransactedReceiveScopeEndCommitFailed'
title: 3557 - TransactedReceiveScopeEndCommitFailed
ms.date: 03/30/2017
ms.assetid: 079f0188-8146-49ee-b6ae-a08f4e4d2b9b
ms.openlocfilehash: 7865ae27e7ce5b3f13b3567f3f8aeebd6edf3fd4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99777977"
---
# <a name="3557---transactedreceivescopeendcommitfailed"></a>3557 - TransactedReceiveScopeEndCommitFailed

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3557|  
|Palavras-chave|WFServices|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que a chamada a EndCommit em um CommittableTransaction apresentou um TransactionException.  
  
## <a name="message"></a>Mensagem  

 A chamada a EndCommit no CommittableTransaction com ID = “%1 " apresentou um TransactionException com a seguinte mensagem: “%2".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|TransactionId|xs:string|A identificação do CommittableTransaction.|  
|Exceção|xs:string|Os detalhes de exceção para a exceção|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
