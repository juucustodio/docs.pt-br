---
description: 'Saiba mais sobre: exceções de transação'
title: Exceções de transações
ms.date: 03/30/2017
ms.assetid: 1d27ed51-7eda-477f-9eca-94fa129f3e07
ms.openlocfilehash: edea932ca12fcd05994c979555e7eb9c0d00e969
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686057"
---
# <a name="transaction-exceptions"></a>Exceções de transações

Este tópico lista todas as exceções geradas pela transação Windows Communication Foundation (WCF).  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|SFxCannotHaveDifferentTransactionProtocolsInOneBinding|As informações de política que estão sendo importadas de metadados especificam valores diferentes para TransactionProtocol entre as operações. Há suporte apenas para um único TransactionProtocol para cada ponto de extremidade.|  
|SFxTransactionAutoCompleteFalseAndInstanceContextMode|A TransactionAutoComplete não pode ser falsa, a menos que o InstanceContextmode do serviço seja PerSession. Foi encontrado um erro na implementação do contrato e da operação especificados.|  
|SFxTransactionInvalidSetTransactionComplete|OperationContext. SetTransactionComplete pode ser chamado em uma operação somente quando a TransactionAutoComplete está definida como false e a TransactionScopeRequired é definida como true. Este é um cenário inválido e a transação atual foi encerrada.|  
|TransactionFlowRequiredIssuedTokens|Para fluir uma transação, os tokens emitidos de fluxo também devem ter suporte.|  
|TrustDriverVersionDoesNotSupportIssuedTokens|A versão de confiança configurada não oferece suporte a tokens emitidos. Use WSTrustFeb2005 ou superior.|
