---
description: 'Saiba mais sobre: compensação'
title: Compensação
ms.date: 03/30/2017
ms.assetid: 722e9766-48d7-456c-9496-d7c5c8f0fa76
ms.openlocfilehash: d2c57a248939d0485075a5cbf57d91789f58d01a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792785"
---
# <a name="compensation"></a>Compensação

A compensação no Windows Workflow Foundation (WF) é o mecanismo pelo qual o trabalho concluído anteriormente pode ser desfeito ou compensado (seguindo a lógica definida pelo aplicativo) quando ocorre uma falha subsequente. Esta seção descreve como usar a compensação em fluxos de trabalho.  
  
## <a name="compensation-vs-transactions"></a>Remuneração versus transações  

 Uma transação permite que você combine várias operações em uma única unidade de trabalho. Usar uma transação fornece ao aplicativo a capacidade de nulo () para reverter as alterações executadas dentro de transação se qualquer erro ocorre durante qualquer parte do processo de transação. No entanto, usar transações pode não ser adequado se o trabalho é longo. Por exemplo, um aplicativo de planejamento de traço é implementado como um fluxo de trabalho. As etapas de fluxo de trabalho podem consistir registrar um voo, uma aprovação de espera gerente e em seguida, pagar por voo. Esse processo pode levar muitos dias e não é prático para as etapas do registro e pagar por voo para participar na mesma transação. Em um cenário como isso, a compensação pode ser usada para desfazer a etapa de registro de fluxo de trabalho se houver uma falha posteriormente no processamento.  
  
> [!NOTE]
> Este tópico aborda a compensação em fluxos de trabalho. Para obter mais informações sobre transações em fluxos de trabalho, consulte [Transações](workflow-transactions.md) e <xref:System.Activities.Statements.TransactionScope> . Para obter mais informações sobre transações, consulte <xref:System.Transactions?displayProperty=nameWithType> e <xref:System.Transactions.Transaction?displayProperty=nameWithType> .  
  
## <a name="using-compensableactivity"></a>Usando CompensableActivity  

 <xref:System.Activities.Statements.CompensableActivity> é a atividade de compensação central em [!INCLUDE[wf1](../../../includes/wf1-md.md)]. Todas as atividades que executa o trabalho que precise ser compensado são colocadas em <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity>. Nesse exemplo, a etapa de retorno de comprar um voo é colocada em <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity> e cancelar de fallback é colocado em <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>. Imediatamente depois de <xref:System.Activities.Statements.CompensableActivity> no fluxo de trabalho são duas atividades aguardando a aprovação gerente e conclua a etapa de compra de voo. Se uma condição de erro faz com que o fluxo de trabalho a ser cancelado após <xref:System.Activities.Statements.CompensableActivity> terminou com êxito, então as atividades no manipulador de <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> são agendadas e o voo é cancelado.  
  
 [!code-csharp[CFX_CompensationExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#1)]  
  
 O exemplo a seguir é o fluxo de trabalho em XAML.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 Quando o fluxo de trabalho é chamado, a saída a seguir são exibidas no console.  
  
 **ReserveFlight: A permissão é permitido.**  
**ManagerApproval: aprovação do gerente recebida.** 
 **PurchaseFlight: o tíquete é comprado.** 
 **Fluxo de trabalho concluído com êxito com o status: fechado.**
> [!NOTE]
> As atividades de exemplo neste tópico como `ReserveFlight` exibem seu nome e finalidade no console ajudar a ilustrar a ordem em que as atividades são executadas quando a compensação ocorre.  
  
### <a name="default-workflow-compensation"></a>Compensação padrão de fluxo de trabalho  

 Por padrão, se o fluxo de trabalho é cancelado, a lógica de compensação é executada para quaisquer atividades compensável que tenha êxito completamente e não tem sido confirmada ou não foi compensada.  
  
> [!NOTE]
> Quando uma <xref:System.Activities.Statements.CompensableActivity> é *confirmada*, a compensação da atividade não pode mais ser invocada. O processo de confirmação é descrito posteriormente nesta seção.  
  
 Nesse exemplo, uma exceção é lançada após o voo é reservado mas antes da etapa de aprovação do gerenciador.  
  
 [!code-csharp[CFX_CompensationExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#2)]  
  
 Este exemplo é o fluxo de trabalho em XAML.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:SimulatedErrorCondition />  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 [!code-csharp[CFX_CompensationExample#100](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#100)]  
  
 Quando o fluxo de trabalho é chamado, a exceção simulada de condição de erro é tratada pelo aplicativo host em <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>, o fluxo de trabalho é cancelado, e a lógica de compensação é chamada.  
  
 **ReserveFlight: A permissão é permitido.**  
**SimulatedErrorCondition: gerando uma ApplicationException.** 
 **Exceção sem tratamento do fluxo de trabalho:** 
 **System. ApplicationException: condição de erro simulada no fluxo de trabalho.** 
 **CancelFlight: o tíquete foi cancelado.** 
 **Fluxo de trabalho concluído com êxito com o status: cancelado.**

### <a name="cancellation-and-compensableactivity"></a>Cancelar e CompensableActivity  

 Se as atividades em <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity> não foram concluídas e a atividade é cancelada, as atividades em <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> são executadas.  
  
> [!NOTE]
> <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> é invocado apenas se as atividades em <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity> não foram concluídas e a atividade é cancelada. <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> é executado somente se as atividades em <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity> eles concluíram com êxito e a compensação está chamada posteriormente na atividade.  
  
 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> fornece a autores de fluxo de trabalho a oportunidade de fornecer qualquer lógica apropriada cancelar. No exemplo a seguir, uma exceção é lançada durante a execução de <xref:System.Activities.Statements.CompensableActivity.Body%2A>, e <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> é chamado em seguida.  
  
```csharp  
Activity wf = new Sequence()  
{  
    Activities =  
    {  
        new CompensableActivity  
        {  
            Body = new Sequence  
            {  
                Activities =
                {  
                    new ChargeCreditCard(),  
                    new SimulatedErrorCondition(),  
                    new ReserveFlight()  
                }  
            },  
            CompensationHandler = new CancelFlight(),  
            CancellationHandler = new CancelCreditCard()  
        },  
        new ManagerApproval(),  
        new PurchaseFlight()  
    }  
};  
```  
  
 Este exemplo é o fluxo de trabalho em XAML  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <Sequence>  
      <c:ChargeCreditCard />  
      <c:SimulatedErrorCondition />  
      <c:ReserveFlight />  
    </Sequence>  
    <CompensableActivity.CancellationHandler>  
      <c:CancelCreditCard />  
    </CompensableActivity.CancellationHandler>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 Quando o fluxo de trabalho é chamado, a exceção simulada de condição de erro é tratada pelo aplicativo host em <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>, o fluxo de trabalho é cancelado, e a lógica de cancelamento de <xref:System.Activities.Statements.CompensableActivity> é chamada. Nesse exemplo, a lógica de compensação e a lógica de cancelamento metas têm diferentes. Se <xref:System.Activities.Statements.CompensableActivity.Body%2A> concluída com êxito, então isso significa que o cartão de crédito foi carregado e o voo registrado, então a compensação devem desfazer as duas etapas. (Neste exemplo, cancelar o vôo cancela automaticamente os encargos do cartão de crédito.) No entanto, se o <xref:System.Activities.Statements.CompensableActivity> for cancelado, isso significa que o <xref:System.Activities.Statements.CompensableActivity.Body%2A> não foi concluído e, portanto, a lógica do <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> precisa ser capaz de determinar como lidar melhor com o cancelamento. Nesse exemplo, <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> cancela a carga de cartão de crédito, mas como `ReserveFlight` era a atividade a mais recente em <xref:System.Activities.Statements.CompensableActivity.Body%2A>, não tenta cancelar o voo. Desde que foi `ReserveFlight` a atividade a mais recente em <xref:System.Activities.Statements.CompensableActivity.Body%2A>, se tiver terminado com êxito em <xref:System.Activities.Statements.CompensableActivity.Body%2A> concluiria e nenhum cancelar seria possível.  
  
 **ChargeCreditCard: Cartão de crédito de carregamento para o voo.**  
**SimulatedErrorCondition: gerando uma ApplicationException.** 
 **Exceção sem tratamento do fluxo de trabalho:** 
 **System. ApplicationException: condição de erro simulada no fluxo de trabalho.** 
 **CancelCreditCard: cancelar cobranças de cartão de crédito.** 
 **Fluxo de trabalho concluído com êxito com o status: cancelado.**  Para obter mais informações sobre cancelamento, consulte [cancelamento](modeling-cancellation-behavior-in-workflows.md).  
  
### <a name="explicit-compensation-using-the-compensate-activity"></a>Compensação explícita usando a atividade de compesação  

 Na seção anterior, a compensação implícita foi abordada. A compensação implícita pode ser adequado para cenários simples, mas se um controle mais explícito é necessário sobre programação de compensação que manipula a atividade de <xref:System.Activities.Statements.Compensate> pode ser usada. Para iniciar o processo de compensação pela atividade de <xref:System.Activities.Statements.Compensate> , <xref:System.Activities.Statements.CompensationToken> de <xref:System.Activities.Statements.CompensableActivity> para que a compensação é desejada é usado. A atividade de <xref:System.Activities.Statements.Compensate> pode ser usada para iniciar a compensação em qualquer <xref:System.Activities.Statements.CompensableActivity> concluído que não foi confirmada ou não foi compensada. Por exemplo, uma atividade de <xref:System.Activities.Statements.Compensate> pode ser usada na seção de <xref:System.Activities.Statements.TryCatch.Catches%2A> de uma atividade de <xref:System.Activities.Statements.TryCatch> , ou após <xref:System.Activities.Statements.CompensableActivity> tiver concluído em qualquer momento que. Nesse exemplo, a atividade de <xref:System.Activities.Statements.Compensate> é usada na seção de <xref:System.Activities.Statements.TryCatch.Catches%2A> de uma atividade de <xref:System.Activities.Statements.TryCatch> para reverter a ação de <xref:System.Activities.Statements.CompensableActivity>.  
  
 [!code-csharp[CFX_CompensationExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#3)]  
  
 Este exemplo é o fluxo de trabalho em XAML.  
  
```xaml  
<TryCatch  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:s="clr-namespace:System;assembly=mscorlib"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <TryCatch.Variables>  
    <Variable  
       x:TypeArguments="CompensationToken"  
       x:Name="__ReferenceID0"  
       Name="token1" />  
  </TryCatch.Variables>  
  <TryCatch.Try>  
    <Sequence>  
      <CompensableActivity>  
        <CompensableActivity.Result>  
          <OutArgument  
             x:TypeArguments="CompensationToken">  
            <VariableReference  
               x:TypeArguments="CompensationToken"  
               Variable="{x:Reference __ReferenceID0}">  
              <VariableReference.Result>  
                <OutArgument  
                   x:TypeArguments="Location(CompensationToken)" />  
              </VariableReference.Result>  
            </VariableReference>  
          </OutArgument>  
        </CompensableActivity.Result>  
        <CompensableActivity.CompensationHandler>  
          <c:CancelFlight />  
        </CompensableActivity.CompensationHandler>  
        <CompensableActivity.ConfirmationHandler>  
          <c:ConfirmFlight />  
        </CompensableActivity.ConfirmationHandler>  
        <c:ReserveFlight />  
      </CompensableActivity>  
      <c:SimulatedErrorCondition />  
      <c:ManagerApproval />  
      <c:PurchaseFlight />  
    </Sequence>  
  </TryCatch.Try>  
  <TryCatch.Catches>  
    <Catch  
       x:TypeArguments="s:ApplicationException">  
      <ActivityAction  
         x:TypeArguments="s:ApplicationException">  
        <Compensate>  
          <Compensate.Target>  
            <InArgument  
               x:TypeArguments="CompensationToken">  
              <VariableValue  
                 x:TypeArguments="CompensationToken"  
                 Variable="{x:Reference __ReferenceID0}">  
                <VariableValue.Result>  
                  <OutArgument  
                     x:TypeArguments="CompensationToken" />  
                </VariableValue.Result>  
              </VariableValue>  
            </InArgument>  
          </Compensate.Target>  
        </Compensate>  
      </ActivityAction>  
    </Catch>  
  </TryCatch.Catches>  
</TryCatch>  
```  
  
 Quando o fluxo de trabalho é chamado, a saída a seguir são exibidas no console.  
  
 **ReserveFlight: A permissão é permitido.**  
**SimulatedErrorCondition: gerando uma ApplicationException.** 
 **CancelFlight: o tíquete foi cancelado.** 
 **Fluxo de trabalho concluído com êxito com o status: fechado.**

### <a name="confirming-compensation"></a>Compensação de confirmação  

 Por padrão, as atividades compensáveis podem ser compensadas em qualquer momento que depois que terminar. Em alguns cenários isso pode não ser adequado. No exemplo anterior a compensação para permitir a permissão foi cancelar a reserva. No entanto, depois que o voo foi concluído essa etapa de compensação não é mais válido. Confirmando a atividade compensável chama a atividade especificada por <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>. Um uso possível para este é permitir todos os recursos que são necessários para executar a compensação a ser liberada. Depois que uma atividade compensável é confirmada não é possível que ele ser compensado, e se esta é tentada uma exceção de <xref:System.InvalidOperationException> é lançada. Quando um fluxo de trabalho concluída com sucesso, as atividades compensáveis qualquer não confirmadas e não compensadas que eles concluíram com êxito são confirmadas em ordem inversa de conclusão. Nesse exemplo o voo é reservado, comprado, e concluído, e a atividade é confirmada em compensável. Para confirmar <xref:System.Activities.Statements.CompensableActivity>, use a atividade de <xref:System.Activities.Statements.Confirm> e especificar <xref:System.Activities.Statements.CompensationToken> de <xref:System.Activities.Statements.CompensableActivity> para confirmar.  
  
 [!code-csharp[CFX_CompensationExample#4](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#4)]  
  
 Este exemplo é o fluxo de trabalho em XAML.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <x:Reference>__ReferenceID0</x:Reference>  
  </Sequence.Variables>  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken">  
        <VariableReference  
           x:TypeArguments="CompensationToken">  
          <VariableReference.Result>  
            <OutArgument  
               x:TypeArguments="Location(CompensationToken)" />  
          </VariableReference.Result>  
          <VariableReference.Variable>  
            <Variable  
               x:TypeArguments="CompensationToken"  
               x:Name="__ReferenceID0"  
               Name="token1" />  
          </VariableReference.Variable>  
        </VariableReference>  
      </OutArgument>  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <CompensableActivity.ConfirmationHandler>  
      <c:ConfirmFlight />  
    </CompensableActivity.ConfirmationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
  <c:TakeFlight />  
  <Confirm>  
    <Confirm.Target>  
      <InArgument  
         x:TypeArguments="CompensationToken">  
        <VariableValue  
           x:TypeArguments="CompensationToken"  
           Variable="{x:Reference __ReferenceID0}">  
          <VariableValue.Result>  
            <OutArgument  
               x:TypeArguments="CompensationToken" />  
          </VariableValue.Result>  
        </VariableValue>  
      </InArgument>  
    </Confirm.Target>  
  </Confirm>  
</Sequence>  
```  
  
Quando o fluxo de trabalho é chamado, a saída a seguir são exibidas no console.  
  
**ReserveFlight: A permissão é permitido.**  
**ManagerApproval: aprovação do gerente recebida.** 
 **PurchaseFlight: o tíquete é comprado.** 
 **TakeFlight: o vôo foi concluído.** 
 **ConfirmFlight: o vôo foi tirado, nenhuma compensação é possível.** 
 **Fluxo de trabalho concluído com êxito com o status: fechado.**

## <a name="nesting-compensation-activities"></a>Atividades de compensação de aninhamento  

<xref:System.Activities.Statements.CompensableActivity> pode ser colocado na seção de <xref:System.Activities.Statements.CompensableActivity.Body%2A> de outro <xref:System.Activities.Statements.CompensableActivity>. <xref:System.Activities.Statements.CompensableActivity> não pode ser colocado em um manipulador de outro <xref:System.Activities.Statements.CompensableActivity>. É responsabilidade de um pai <xref:System.Activities.Statements.CompensableActivity> garantir que quando é cancelado, confirmado, ou compensado, todas as atividades compensáveis filhos que eles concluíram com êxito e não foram confirmadas ou não foram compensadas deve ser compensado ou confirmadas antes que o pai conclua o cancelar, confirmação, ou a compensação. Se isso não é modelado explicitamente <xref:System.Activities.Statements.CompensableActivity> pai compensará implicitamente atividades compensáveis filho se o pai recebeu o cancelamento ou compensa o sinal. Se o pai recebeu o sinal de confirmação o pai confirmará implicitamente atividades compensáveis filhos. Se a lógica para manipular cancelamento, confirmação, ou a compensação é modelada explicitamente no manipulador de <xref:System.Activities.Statements.CompensableActivity>pai, qualquer filho tratado não explicitamente será confirmado implicitamente.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Activities.Statements.CompensableActivity>
- <xref:System.Activities.Statements.Compensate>
- <xref:System.Activities.Statements.Confirm>
- <xref:System.Activities.Statements.CompensationToken>
