---
description: 'Saiba mais sobre: como criar um serviço transacional'
title: 'Como: criar um serviço transacional'
ms.date: 03/30/2017
ms.assetid: 1bd2e4ed-a557-43f9-ba98-4c70cb75c154
ms.openlocfilehash: 78ad922a7e1f174715be7bd1a8466572425411be
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99643430"
---
# <a name="how-to-create-a-transactional-service"></a>Como: criar um serviço transacional

Este exemplo demonstra vários aspectos da criação de um serviço transacional e o uso de uma transação iniciada pelo cliente para coordenar operações de serviço.  
  
### <a name="creating-a-transactional-service"></a>Criando um serviço transacional  
  
1. Crie um contrato de serviço e anote as operações com a configuração desejada da <xref:System.ServiceModel.TransactionFlowOption> enumeração para especificar os requisitos de transação de entrada. Observe que você também pode inserir o <xref:System.ServiceModel.TransactionFlowAttribute> na classe de serviço que está sendo implementada. Isso permite que uma única implementação de uma interface Use essas configurações de transação, em vez de cada implementação.  
  
    ```csharp
    [ServiceContract]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // Use this to require an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Mandatory)]  
        double Add(double n1, double n2);  
        [OperationContract]  
        // Use this to permit an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        double Subtract(double n1, double n2);  
    }  
    ```  
  
2. Crie uma classe de implementação e use o <xref:System.ServiceModel.ServiceBehaviorAttribute> para especificar opcionalmente um <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> e um <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> . Você deve observar que, em muitos casos, o padrão <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> de 60 segundos e o <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> padrão `Unspecified` são apropriados. Para cada operação, você pode usar o <xref:System.ServiceModel.OperationBehaviorAttribute> atributo para especificar se o trabalho executado dentro do método deve ocorrer dentro do escopo de um escopo de transação de acordo com o valor do <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> atributo. Nesse caso, a transação usada para o `Add` método é a mesma que a transação de entrada obrigatória que está fluindo do cliente e a transação usada para o `Subtract` método é a mesma que a transação de entrada, caso um tenha sido transmitido do cliente ou uma nova transação criada implicitamente e localmente.  
  
    ```csharp
    [ServiceBehavior(  
        TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
        TransactionTimeout = "00:00:45")]  
    public class CalculatorService : ICalculator  
    {  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n1} to {n2}");
            return n1 + n2;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n2} from {n1}");
            return n1 - n2;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
            // This is where the transaction provides specific benefit  
            // - changes to the database will be committed only when  
            // the transaction completes.  
        }  
    }  
    ```  
  
3. Configure as associações no arquivo de configuração, especificando que o contexto de transação deve ser fluído e os protocolos a serem usados para fazer isso. Para obter mais informações, consulte [configuração de transação de ServiceModel](servicemodel-transaction-configuration.md). Especificamente, o tipo de associação é especificado no atributo do elemento do ponto de extremidade `binding` . O [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) elemento contém um `bindingConfiguration` atributo que faz referência a uma configuração de associação denominada `transactionalOleTransactionsTcpBinding` , conforme mostrado na seguinte configuração de exemplo.  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     O fluxo de transações é habilitado no nível de configuração usando o `transactionFlow` atributo, e o protocolo de transação é especificado usando o `transactionProtocol` atributo, conforme mostrado na configuração a seguir.  
  
    ```xml  
    <bindings>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="supporting-multiple-transaction-protocols"></a>Oferecendo suporte a vários protocolos de transação  
  
1. Para obter um desempenho ideal, você deve usar o protocolo OleTransactions para cenários que envolvem um cliente e um serviço gravados usando Windows Communication Foundation (WCF). No entanto, o protocolo WS-AtomicTransaction (WS-AT) é útil para cenários em que a interoperabilidade com pilhas de protocolos de terceiros é necessária. Você pode configurar os serviços WCF para aceitar os dois protocolos fornecendo vários pontos de extremidade com associações específicas de protocolo apropriadas, conforme mostrado na configuração de exemplo a seguir.  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="http://localhost:8000/CalcService"  
        binding="wsHttpBinding"  
        bindingConfiguration="transactionalWsatHttpBinding"  
        contract="ICalculator"  
        name="WSAtomicTransaction_endpoint" />  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     O protocolo de transação é especificado usando o `transactionProtocol` atributo. No entanto, esse atributo está ausente do fornecido pelo sistema `wsHttpBinding` , pois essa associação só pode usar o protocolo WS-AT.  
  
    ```xml  
    <bindings>  
      <wsHttpBinding>  
        <binding name="transactionalWsatHttpBinding"  
          transactionFlow="true" />  
      </wsHttpBinding>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="controlling-the-completion-of-a-transaction"></a>Controlando a conclusão de uma transação  
  
1. Por padrão, as operações do WCF automaticamente concluem transações se nenhuma exceção sem tratamento for lançada. Você pode modificar esse comportamento usando a <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> propriedade e o <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> método. Quando uma operação é necessária para ocorrer na mesma transação que outra operação (por exemplo, uma operação de débito e crédito), você pode desabilitar o comportamento de preenchimento automático definindo a <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> propriedade `false` como, conforme mostrado no exemplo de operação a seguir `Debit` . A transação `Debit` usada pela operação não é concluída até que um método com a <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> propriedade definida `true` seja chamado, conforme mostrado na operação `Credit1` , ou quando o <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> método é chamado para marcar explicitamente a transação como concluída, conforme mostrado na operação `Credit2` . Observe que as duas operações de crédito são mostradas para fins de ilustração e que uma única operação de crédito seria mais típica.  
  
    ```csharp
    [ServiceBehavior]  
    public class CalculatorService : IAccount  
    {  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Debit(double n)  
        {  
            // Perform debit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = true)]  
        public void Credit1(double n)  
        {  
            // Perform credit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Credit2(double n)  
        {  
            // Perform alternate credit operation  
  
            OperationContext.Current.SetTransactionComplete();  
            return;  
        }  
    }  
    ```  
  
2. Para fins de correlação de transações, definir a <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> propriedade como `false` requer o uso de uma associação de sessão. Esse requisito é especificado com a `SessionMode` propriedade no <xref:System.ServiceModel.ServiceContractAttribute> .  
  
    ```csharp
    [ServiceContract(SessionMode = SessionMode.Required)]  
    public interface IAccount  
    {  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Debit(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit1(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit2(double n);  
    }  
    ```  
  
### <a name="controlling-the-lifetime-of-a-transactional-service-instance"></a>Controlando o tempo de vida de uma instância de serviço transacional  
  
1. O WCF usa a <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> propriedade para especificar se a instância de serviço subjacente é liberada quando uma transação é concluída. Como esse padrão é `true` , a menos que configurado de outra forma, o WCF exibe um comportamento de ativação "Just-in-time" eficiente e previsível. As chamadas para um serviço em uma transação subsequente são garantidas como uma nova instância de serviço sem vestígios do estado da transação anterior. Embora isso seja geralmente útil, às vezes você pode desejar manter o estado dentro da instância do serviço além da conclusão da transação. Exemplos disso seriam quando o estado ou os identificadores necessários para os recursos forem caros de recuperar ou reconstituir. Você pode fazer isso definindo a <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> propriedade como `false` . Com essa configuração, a instância e qualquer estado associado estarão disponíveis em chamadas subsequentes. Ao usar isso, dê uma consideração cuidadosa sobre quando e como o estado e as transações serão limpos e concluídos. O exemplo a seguir demonstra como fazer isso mantendo a instância com a `runningTotal` variável.  
  
    ```csharp
    [ServiceBehavior(TransactionIsolationLevel = [ServiceBehavior(  
        ReleaseServiceInstanceOnTransactionComplete = false)]  
    public class CalculatorService : ICalculator  
    {  
        double runningTotal = 0;  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n} to {runningTotal}");
            runningTotal = runningTotal + n;  
            return runningTotal;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n} from {runningTotal}");
            runningTotal = runningTotal - n;  
            return runningTotal;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
        }  
    }  
    ```  
  
    > [!NOTE]
    > Como o tempo de vida da instância é um comportamento que é interno ao serviço e controlado por meio da <xref:System.ServiceModel.ServiceBehaviorAttribute> propriedade, nenhuma modificação na configuração do serviço ou no contrato de serviço é necessária para definir o comportamento da instância. Além disso, a transmissão não conterá nenhuma representação.
