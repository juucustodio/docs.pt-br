---
description: 'Saiba mais sobre: atributos de transação ServiceModel'
title: Atributos de transação de ServiceModel
ms.date: 03/30/2017
helpviewer_keywords:
- transactions [WCF], ServiceModel attributes
ms.assetid: 1e0d2436-6ae5-439b-9765-a448d6f60000
ms.openlocfilehash: 0b443fc6b9503007574608afe03c5e0508f666d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793474"
---
# <a name="servicemodel-transaction-attributes"></a>Atributos de transação de ServiceModel

Windows Communication Foundation (WCF) fornece propriedades em três <xref:System.ServiceModel> atributos padrão que permitem que você configure o comportamento das transações para um serviço WCF:

- <xref:System.ServiceModel.TransactionFlowAttribute>

- <xref:System.ServiceModel.ServiceBehaviorAttribute>

- <xref:System.ServiceModel.OperationBehaviorAttribute>

## <a name="transactionflowattribute"></a>TransactionFlowAttribute

O <xref:System.ServiceModel.TransactionFlowAttribute> atributo especifica a disposição de uma operação em um contrato de serviço para aceitar as transações de entrada de um cliente. O atributo fornece esse controle com a seguinte propriedade: as transações usam a <xref:System.ServiceModel.TransactionFlowOption> enumeração para especificar se uma transação de entrada é <xref:System.ServiceModel.TransactionFlowOption.Mandatory> , <xref:System.ServiceModel.TransactionFlowOption.Allowed> ou <xref:System.ServiceModel.TransactionFlowOption.NotAllowed> .

Esse é o único atributo que relaciona as operações de serviço a interações externas com um cliente. Os atributos descritos nas seções a seguir estão relacionados ao uso de transações dentro da execução da operação.

## <a name="servicebehaviorattribute"></a>ServiceBehaviorAttribute

O <xref:System.ServiceModel.ServiceBehaviorAttribute> atributo especifica o comportamento de execução interno de uma implementação de contrato de serviço. As propriedades específicas da transação desse atributo incluem:

- <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionAutoCompleteOnSessionClose%2A> Especifica se uma transação não concluída será concluída quando a sessão for fechada. O valor padrão desta propriedade é `false`. Se essa propriedade for `true` , e a sessão de entrada for desligada normalmente, em vez de fechar devido a falhas de rede ou de cliente, qualquer transação não concluída será concluída com êxito. Caso contrário, se essa propriedade for `false` ou se a sessão não tiver sido fechada normalmente, qualquer transação não concluída será revertida quando a sessão for fechada. Se essa propriedade for `true` , o canal de entrada deverá ser baseado em sessão.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> Especifica se a instância de serviço subjacente é liberada quando uma transação é concluída. O valor padrão desta propriedade é `true`. A próxima mensagem de entrada faz com que uma nova instância subjacente seja criada, descartando qualquer estado por transação que a instância anterior possa ter mantido. A liberação de uma instância de serviço é uma ação interna que o serviço usa e não tem impacto sobre as conexões ou sessões existentes que os clientes podem ter estabelecido. Essa funcionalidade é equivalente ao recurso de ativação Just-in-time que o COM+ fornece. Se a propriedade for `true` , <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> deve ser igual a <xref:System.ServiceModel.ConcurrencyMode.Single> . Caso contrário, o serviço lançará uma exceção de validação de configuração inválida durante a inicialização.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> Especifica o nível de isolamento a ser usado para transações dentro do serviço; Essa propriedade usa um dos <xref:System.Transactions.IsolationLevel> valores. Se a propriedade de nível de isolamento local for algo diferente <xref:System.Transactions.IsolationLevel.Unspecified> , o nível de isolamento de uma transação de entrada deverá corresponder à configuração dessa propriedade local. Caso contrário, a transação de entrada será rejeitada e uma falha será enviada de volta ao cliente. Se <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> for `true` , e nenhuma transação estiver fluindo, essa propriedade determinará o <xref:System.Transactions.IsolationLevel> valor a ser usado para a transação criada localmente. Se <xref:System.Transactions.IsolationLevel> é definido como <xref:System.Transactions.IsolationLevel.Unspecified> , <xref:System.Transactions.IsolationLevel> <xref:System.Transactions.IsolationLevel.Serializable> é usado.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> Especifica o período de tempo no qual uma nova transação criada no serviço deve ser concluída. Se esse tempo for atingido e a transação não tiver sido concluída, ela será anulada. O <xref:System.TimeSpan> é usado como o <xref:System.Transactions.TransactionScope> tempo limite para qualquer operação que tenha <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> sido definida para `true` e para a qual uma nova transação foi criada. O tempo limite é a duração máxima permitida desde a criação da transação até a conclusão da fase 1 no protocolo de confirmação de duas fases. O valor de tempo limite usado é sempre o valor mais baixo entre a <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> propriedade e a `transactionTimeout` definição de configuração.

## <a name="operationbehaviorattribute"></a>OperationBehaviorAttribute

O <xref:System.ServiceModel.OperationBehaviorAttribute> atributo especifica os comportamentos dos métodos na implementação do serviço. Você pode usá-lo para indicar o comportamento de execução específico da operação. As propriedades desse atributo não afetam a descrição da linguagem WSDL do contrato de serviço e são puramente elementos do modelo de programação do WCF que permitem recursos comuns que os desenvolvedores precisam implementar.

Este atributo tem as seguintes propriedades específicas de transação:

- <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> Especifica se um método deve ser executado em um escopo de transação ativo. O padrão é `false`. Se o <xref:System.ServiceModel.OperationBehaviorAttribute> atributo não estiver definido para um método, ele também implica que o método não será executado em uma transação. Se um escopo de transação não for necessário para uma operação, qualquer transação que esteja presente no cabeçalho da mensagem não será ativada e permanecerá como um elemento do <xref:System.ServiceModel.OperationContext.IncomingMessageProperties%2A> do <xref:System.ServiceModel.OperationContext> . Se um escopo de transação for necessário para uma operação, a origem da transação será derivada de um dos seguintes:

  - Se uma transação fluir do cliente, o método será executado em um escopo de transação criado usando essa transação distribuída.

  - Com um transporte em fila, a transação usada para remover a fila da mensagem é usada. Observe que a transação usada não é uma transação fluida, pois ela não foi fornecida pelo remetente original da mensagem.

  - Um transporte personalizado pode fornecer uma transação por meio do uso do `TransportTransactionProperty` .

  - Se nenhuma das opções acima fornecer uma origem externa para uma transação, uma nova <xref:System.Transactions.Transaction> instância será criada imediatamente antes de chamar o método.

- <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> Especifica se a transação na qual o método é executado será concluída automaticamente se nenhuma exceção não tratada for gerada. Se essa propriedade for `true` , a infraestrutura de chamada marcará automaticamente a transação como "concluída" se o método de usuário retornar sem gerar uma exceção. Se essa propriedade for `false` , a transação será anexada à instância e será marcada apenas como "concluída" se o cliente chamar um método subsequente que está marcado com essa propriedade igual a `true` ou se um método subsequente chamar explicitamente <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> . A falha em executar um desses resultados na transação nunca está sendo "concluída" e o trabalho contido não é confirmado, a menos que a <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionAutoCompleteOnSessionClose%2A> Propriedade esteja definida como `true` . Se essa propriedade for definida como `true` , você deverá usar um canal com uma sessão e <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> deverá ser definida como <xref:System.ServiceModel.InstanceContextMode.PerSession> .
