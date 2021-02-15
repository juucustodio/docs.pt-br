---
description: 'Saiba mais sobre: transações de fluxo de trabalho'
title: Transações de fluxo de trabalho
ms.date: 03/30/2017
ms.assetid: 6081fb02-c0f2-483d-97b8-f3b7dc03011d
ms.openlocfilehash: 105876179bcfe685bc65b209f0fbacb1d6eae5bc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754869"
---
# <a name="workflow-transactions"></a>Transações de fluxo de trabalho

[!INCLUDE[wf1](../../../includes/wf1-md.md)] fornece suporte para participar de transações de <xref:System.Transactions> usando a atividade de <xref:System.Activities.Statements.TransactionScope> para definir o escopo uma unidade transacionada de trabalho. Quando <xref:System.Transactions.TransactionScope?displayProperty=nameWithType> deve ser explicitamente concluído chamadas de atividade de <xref:System.Activities.Statements.TransactionScope?displayProperty=nameWithType> implicitamente completos na transação em cima de conclusão com êxito. Todas as atividades que estão contidas em <xref:System.Activities.Statements.TransactionScope.Body%2A> de atividade de <xref:System.Activities.Statements.TransactionScope> participam na transação. WF pode passar transações em um fluxo de trabalho pelo uso de atividade de <xref:System.ServiceModel.Activities.TransactedReceiveScope> . Como a atividade de <xref:System.Activities.Statements.TransactionScope> , quaisquer atividades contida em <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> participa na transação. WF garante que as atividades dependentes em <xref:System.Transactions.Transaction.Current%2A?displayProperty=nameWithType> para trabalhar com <xref:System.Activities.Statements.TransactionScope> e <xref:System.ServiceModel.Activities.TransactedReceiveScope>. Se o sistema forneceu as atividades não endereçam todos os requisitos, as atividades personalizados podem ser criadas usando <xref:System.Activities.RuntimeTransactionHandle> para habilitar cenários avançados do controle de fluxo e de transação.  
  
No exemplo a seguir, um fluxo de trabalho é construído consistindo em uma <xref:System.Activities.Statements.Sequence> atividade que contém atividades filho, incluindo uma <xref:System.Activities.Statements.TransactionScope> atividade. As atividades de <xref:System.Activities.Statements.TransactionScope.Body%2A> de <xref:System.Activities.Statements.TransactionScope> executam sob a transação inicializada pela atividade de <xref:System.Activities.Statements.TransactionScope> .  
  
```csharp  
static Activity ScenarioOne()  
{  
    return new Sequence  
    {  
        Activities =  
        {  
            new WriteLine { Text = "    Begin workflow" },  
  
            new TransactionScope  
            {  
                Body = new Sequence  
                {  
                    Activities =
                    {  
                        new WriteLine { Text = "    Begin TransactionScope" },  
  
                        new PrintTransactionId(),  
  
                        new TransactionScopeTest(),  
  
                        new WriteLine { Text = "    End TransactionScope" },  
                    },  
                },  
            },  
  
            new WriteLine { Text = "    End workflow" },  
        }  
    };  
}  
```  
  
Para obter mais informações, consulte sobre como usar o <xref:System.ServiceModel.Activities.TransactedReceiveScope> , consulte [Transações de fluxo dentro e fora dos serviços de fluxo de trabalho](../wcf/feature-details/flowing-transactions-into-and-out-of-workflow-services.md).  
  
## <a name="see-also"></a>Confira também

- <xref:System.Activities.Statements.TransactionScope>
- <xref:System.Transactions.TransactionScope>
- <xref:System.Transactions.Transaction.Current%2A?displayProperty=nameWithType>
