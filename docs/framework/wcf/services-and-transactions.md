---
description: 'Saiba mais sobre: serviços e transações'
title: Serviços e transações
ms.date: 03/30/2017
helpviewer_keywords:
- service contracts [WCF], designing services and transactions
ms.assetid: 864813ff-2709-4376-912d-f5c8d318c460
ms.openlocfilehash: 4126ca139bd2097aeaaff756de694d0ff0061b5d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792967"
---
# <a name="services-and-transactions"></a>Serviços e transações

Os aplicativos Windows Communication Foundation (WCF) podem iniciar uma transação de dentro de um cliente e coordenar a transação dentro da operação de serviço. Os clientes podem iniciar uma transação e invocar várias operações de serviço e garantir que as operações de serviço sejam confirmadas ou revertidas como uma única unidade.  
  
 Você pode habilitar o comportamento da transação no contrato de serviço especificando um <xref:System.ServiceModel.ServiceBehaviorAttribute> e definindo suas <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> Propriedades e para operações de serviço que exigem transações do cliente. O <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> parâmetro especifica se a transação na qual o método é executado será automaticamente concluída se nenhuma exceção não tratada for lançada. Para obter mais informações sobre esses atributos, consulte [ServiceModel Transaction Attributes](./feature-details/servicemodel-transaction-attributes.md).  
  
 O trabalho executado nas operações de serviço e gerenciado por um Gerenciador de recursos, como registro em log de atualizações de banco de dados, faz parte da transação do cliente.  
  
 O exemplo a seguir demonstra o uso <xref:System.ServiceModel.ServiceBehaviorAttribute> dos <xref:System.ServiceModel.OperationBehaviorAttribute> atributos e para controlar o comportamento da transação no lado do serviço.  
  
```csharp
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CalculatorService: ICalculatorLog  
{  
    [OperationBehavior(TransactionScopeRequired = true,  
                           TransactionAutoComplete = true)]  
    public double Add(double n1, double n2)  
    {  
        recordToLog($"Added {n1} to {n2}");
        return n1 + n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,
                               TransactionAutoComplete = true)]  
    public double Subtract(double n1, double n2)  
    {  
        recordToLog($"Subtracted {n1} from {n2}");
        return n1 - n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,
                                       TransactionAutoComplete = true)]  
    public double Multiply(double n1, double n2)  
    {  
        recordToLog($"Multiplied {n1} by {n2}");
        return n1 * n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,
                                       TransactionAutoComplete = true)]  
    public double Divide(double n1, double n2)  
    {  
        recordToLog($"Divided {n1} by {n2}", n1, n2);
        return n1 / n2;  
    }  
  
}  
```  
  
 Você pode habilitar transações e fluxo de transações configurando as associações de cliente e serviço para usar o protocolo WS-AtomicTransaction e definindo o [\<transactionFlow>](../configure-apps/file-schema/wcf/transactionflow.md) elemento como `true` , conforme mostrado na seguinte configuração de exemplo.  
  
```xml  
<client>  
    <endpoint address="net.tcp://localhost/ServiceModelSamples/service"
          binding="netTcpBinding"
          bindingConfiguration="netTcpBindingWSAT"
          contract="Microsoft.ServiceModel.Samples.ICalculatorLog" />  
</client>  
  
<bindings>  
    <netTcpBinding>  
        <binding name="netTcpBindingWSAT"  
                transactionFlow="true"  
                transactionProtocol="WSAtomicTransactionOctober2004" />  
     </netTcpBinding>  
</bindings>  
```  
  
 Os clientes podem iniciar uma transação criando uma <xref:System.Transactions.TransactionScope> e invocando operações de serviço dentro do escopo da transação.  
  
```csharp
using (TransactionScope ts = new TransactionScope(TransactionScopeOption.RequiresNew))  
{  
    //Do work here  
    ts.Complete();  
}  
```  
  
## <a name="see-also"></a>Consulte também

- [Suporte transacional em System.ServiceModel](./feature-details/transactional-support-in-system-servicemodel.md)
- [Modelos de transação](./feature-details/transaction-models.md)
- [Fluxo de transação WS](./samples/ws-transaction-flow.md)
