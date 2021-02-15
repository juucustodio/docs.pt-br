---
description: 'Saiba mais sobre: início rápido de solução de problemas do WCF'
title: Início rápido de solução de problemas do WCF
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], troubleshooting
- Windows Communication Foundation [WCF], troubleshooting
ms.assetid: a9ea7a53-f31a-46eb-806e-898e465a4992
ms.openlocfilehash: 686b008752704ed54700d9c49e2df71f9fc3fd98
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631652"
---
# <a name="wcf-troubleshooting-quickstart"></a>Início rápido de solução de problemas do WCF

Este tópico lista vários problemas conhecidos que os clientes têm ao desenvolver serviços e clientes WCF. Se o problema no qual você está executando não estiver nesta lista, recomendamos que você configure o rastreamento para seu serviço. Isso irá gerar um arquivo de rastreamento que você pode exibir com o Visualizador do arquivo de rastreamento e obter informações detalhadas sobre as exceções que podem estar ocorrendo dentro do serviço. Para obter mais informações sobre como configurar o rastreamento, consulte: [Configurando o rastreamento](./diagnostics/tracing/configuring-tracing.md). Para obter mais informações sobre o Visualizador de arquivos de rastreamento, consulte: [Service Trace Viewer Tool (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md).  
  
1. [Depois de instalar o Windows 7 e o IIS, quando tento navegar até um serviço WCF, obtenho a seguinte mensagem de erro: erro HTTP 404,3 – não encontrado](#bkmk_0)  
  
     Erro HTTP 404,3 – a página não FoundThe que você está solicitando não pode ser servida devido à configuração da extensão. Se a página for um script, adicione um manipulador. Se o arquivo deve ser baixado, adicione um mapa MIME. Erro detalhado InformationModule StaticFileModule.  
  
2. [Às vezes, recebo um MessageSecurityException na segunda solicitação se meu cliente estiver ocioso por um tempo após a primeira solicitação. O que está acontecendo?](#BKMK_q1)  
  
3. [Meu serviço começa a rejeitar novos clientes depois de cerca de 10 clientes interagindo com ele. O que está acontecendo?](#BKMK_q2)  
  
4. [Posso carregar minha configuração de serviço de algum lugar além do arquivo de configuração do aplicativo WCF?](#BKMK_q3)  
  
5. [Meu serviço e cliente funcionam muito bem, mas não posso fazer com que eles funcionem quando o cliente está em outro computador? O que está acontecendo?](#BKMK_q4)  
  
6. [Quando lanço uma FaultException \<Exception> em que o tipo é uma exceção, sempre recebi um tipo FaultException geral no cliente e não no tipo genérico. O que está acontecendo?](#BKMK_q5)  
  
7. [Parece que as operações unidirecionais e de solicitação-resposta retornam com aproximadamente a mesma velocidade quando a resposta não contém dados. O que está acontecendo?](#BKMK_q6)  
  
8. [Estou usando um certificado X. 509 com meu serviço e obtenho um System. Security. Cryptography. CryptographicException. O que está acontecendo?](#BKMK_q77)  
  
9. [Alterei o primeiro parâmetro de uma operação de maiúscula para minúscula; Agora, meu cliente gera uma exceção. O que está acontecendo?](#BKMK_q88)  
  
10. [Estou usando uma das minhas ferramentas de rastreamento e obtenho um EndpointNotFoundException. O que está acontecendo?](#BKMK_q99)  
  
11. [Ao chamar um aplicativo Web HTTP WCF de um aplicativo SOAP do WCF, o serviço retorna o seguinte erro: método 405 não permitido](#BK_MK99)  
  
 [Qual é o endereço base? Como ele se relaciona a um endereço de ponto de extremidade?](#BKMK_q10)  
  
<a name="bkmk_0"></a>

## <a name="after-installing-windows-7-and-iis-when-i-attempt-to-browse-to-a-wcf-service-i-get-the-following-error-message-http-error-4043--not-found"></a>Depois de instalar o Windows 7 e o IIS, quando tento navegar até um serviço WCF, obtenho a seguinte mensagem de erro: erro HTTP 404,3 – não encontrado  

 A mensagem de erro completa é:  
  
 Erro HTTP 404,3 – a página não FoundThe que você está solicitando não pode ser servida devido à configuração da extensão. Se a página for um script, adicione um manipulador. Se o arquivo deve ser baixado, adicione um mapa MIME. Erro detalhado InformationModule StaticFileModule.  
  
 Essa mensagem de erro ocorre quando "Windows Communication Foundation ativação HTTP" não é definida explicitamente no painel de controle. Para definir isso, vá para o painel de controle, clique em programas no canto inferior esquerdo da janela. Clique em ativar ou desativar recursos do Windows. Expanda Microsoft .NET Framework 3.5.1 e selecione Windows Communication Foundation ativação HTTP.  
  
<a name="BKMK_q1"></a>

## <a name="sometimes-i-receive-a-messagesecurityexception-on-the-second-request-if-my-client-is-idle-for-a-while-after-the-first-request-what-is-happening"></a>Às vezes, recebo um MessageSecurityException na segunda solicitação se meu cliente estiver ocioso por um tempo após a primeira solicitação. O que está acontecendo?  

 A segunda solicitação pode falhar principalmente por dois motivos: (1) a sessão atingiu o tempo limite ou (2) o servidor Web que está hospedando o serviço é reciclado. No primeiro caso, a sessão é válida até que o serviço expire. Quando o serviço não recebe uma solicitação do cliente no período de tempo especificado na associação do serviço ( <xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A> ), o serviço encerra a sessão de segurança. As mensagens de cliente subsequentes resultam no <xref:System.ServiceModel.Security.MessageSecurityException> . O cliente deve restabelecer uma sessão segura com o serviço para enviar mensagens futuras ou usar um token de contexto de segurança com estado. Tokens de contexto de segurança com estado também permitem que uma sessão segura sobreviver a um servidor Web sendo reciclado. Para obter mais informações sobre como usar tokens de contexto seguro com estado em uma sessão segura, consulte [como: criar um token de contexto de segurança para uma sessão segura](./feature-details/how-to-create-a-security-context-token-for-a-secure-session.md). Como alternativa, você pode desabilitar sessões seguras. Ao usar a [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) associação, você pode definir a `establishSecurityContext` propriedade como `false` para desabilitar as sessões seguras. Para desabilitar sessões seguras para outras associações, você deve criar uma associação personalizada. Para obter detalhes sobre como criar uma associação personalizada, consulte [como: criar uma associação personalizada usando o SecurityBindingElement](./feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md). Antes de aplicar qualquer uma dessas opções, você deve entender os requisitos de segurança do aplicativo.  
  
<a name="BKMK_q2"></a>

## <a name="my-service-starts-to-reject-new-clients-after-about-10-clients-are-interacting-with-it-what-is-happening"></a>Meu serviço começa a rejeitar novos clientes depois de cerca de 10 clientes interagindo com ele. O que está acontecendo?  

 Por padrão, os serviços podem ter apenas 10 sessões simultâneas. Portanto, se as associações de serviço usarem sessões, o serviço aceitará novas conexões de cliente até atingir esse número, após a qual ele recusará novas conexões de cliente até que uma das sessões atuais termine. Você pode dar suporte a mais clientes de várias maneiras. Se o serviço não exigir sessões, não use uma associação de sessão. (Para obter mais informações, consulte [usando sessões](using-sessions.md).) Outra opção é aumentar o limite da sessão alterando o valor da <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> propriedade para o número apropriado à sua circunstância.  
  
<a name="BKMK_q3"></a>

## <a name="can-i-load-my-service-configuration-from-somewhere-other-than-the-wcf-applications-configuration-file"></a>Posso carregar minha configuração de serviço de algum lugar além do arquivo de configuração do aplicativo WCF?  

 Sim, no entanto, você precisa criar uma <xref:System.ServiceModel.ServiceHost> classe personalizada que substitua o <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> método. Dentro desse método, você pode chamar a base para carregar a configuração primeiro (se desejar carregar as informações de configuração padrão também), mas também pode substituir totalmente o sistema de carregamento da configuração. Se você deseja carregar a configuração de um arquivo de configuração diferente do arquivo de configuração do aplicativo, você deve analisar o arquivo de configuração por conta própria e carregar a configuração.  
  
 O exemplo de código a seguir mostra como substituir o <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> método e configurar diretamente um ponto de extremidade.  
  
```csharp
public class MyServiceHost : ServiceHost  
{  
    public MyServiceHost(Type serviceType, params Uri[] baseAddresses)
      : base(serviceType, baseAddresses)  
    {
        Console.WriteLine("MyServiceHost Constructor");
    }  
  
    protected override void ApplyConfiguration()  
    {  
        string straddress = GetAddress();  
        Uri address = new Uri(straddress);  
        Binding binding = GetBinding();  
        base.AddServiceEndpoint(typeof(IData), binding, address);  
    }  
  
    string GetAddress()  
    {
        return "http://MyMachine:7777/MyEndpointAddress/";
    }  
  
    Binding GetBinding()  
    {  
        WSHttpBinding binding = new WSHttpBinding();  
        binding.Security.Mode = SecurityMode.None;  
        return binding;  
    }  
}  
```  
  
<a name="BKMK_q4"></a>

## <a name="my-service-and-client-work-great-but-i-cant-get-them-to-work-when-the-client-is-on-another-computer-whats-happening"></a>Meu serviço e cliente funcionam muito bem, mas não posso fazer com que eles funcionem quando o cliente está em outro computador? O que está acontecendo?  

 Dependendo da exceção, pode haver vários problemas:  
  
- Talvez seja necessário alterar os endereços do ponto de extremidade do cliente para o nome do host e não para "localhost".  
  
- Talvez seja necessário abrir a porta para o aplicativo. Para obter detalhes, consulte as [instruções de firewall](./samples/firewall-instructions.md) das amostras do SDK.  
  
- Para outros problemas possíveis, consulte o tópico de exemplos [executando os exemplos de Windows Communication Foundation](./samples/running-the-samples.md).  
  
- Se o cliente estiver usando credenciais do Windows e a exceção for a <xref:System.ServiceModel.Security.SecurityNegotiationException> , configure o Kerberos da seguinte maneira.  
  
    1. Adicione as credenciais de identidade ao elemento de ponto de extremidade no arquivo de App.config do cliente:  
  
        ```xml
        <endpoint
          address="http://MyServer:8000/MyService/"
          binding="wsHttpBinding"
          bindingConfiguration="WSHttpBinding_IServiceExample"
          contract="IServiceExample"
          behaviorConfiguration="ClientCredBehavior"
          name="WSHttpBinding_IServiceExample">  
          <identity>  
            <userPrincipalName value="name@corp.contoso.com"/>  
          </identity>  
        </endpoint>  
        ```  
  
    2. Execute o serviço auto-hospedado na conta sistema ou NetworkService. Você pode executar este comando para criar uma janela de comando na conta do sistema:  
  
        ```console
        at 12:36 /interactive "cmd.exe"  
        ```  
  
    3. Hospede o serviço em Serviços de Informações da Internet (IIS), que, por padrão, usa a conta SPN (nome da entidade de serviço).  
  
    4. Registre um novo SPN com o domínio usando SetSPN. Você precisa ser um administrador de domínio para fazer isso.  
  
 Para obter mais informações sobre o protocolo Kerberos, consulte [conceitos de segurança usados no WCF](./feature-details/security-concepts-used-in-wcf.md) e:  
  
- [Depurando erros de autenticação do Windows](./feature-details/debugging-windows-authentication-errors.md)  
  
- [Registrando nomes da entidade de serviço Kerberos usando Http.sys](/previous-versions/sql/sql-server-2008-r2/ms178119(v=sql.105))  
  
- [Explicações Kerberos](/previous-versions/windows/it-pro/windows-2000-server/bb742516(v=technet.10))  
  
<a name="BKMK_q5"></a>

## <a name="when-i-throw-a-faultexceptionexception-where-the-type-is-an-exception-i-always-receive-a-general-faultexception-type-on-the-client-and-not-the-generic-type-whats-happening"></a>Quando lanço uma FaultException \<Exception> em que o tipo é uma exceção, sempre recebi um tipo FaultException geral no cliente e não no tipo genérico. O que está acontecendo?  

 É altamente recomendável que você crie seu próprio tipo de dados de erro personalizado e declare-o como o tipo de detalhe em seu contrato de falha. O motivo é que usar tipos de exceção fornecidos pelo sistema:  
  
- Cria uma dependência de tipo que remove um dos maiores pontos fortes dos aplicativos orientados a serviços.  
  
- Não é possível depender da serialização de exceções de forma padrão. Alguns — como <xref:System.Security.SecurityException> – talvez não sejam serializáveis.  
  
- Expõe detalhes de implementação interna aos clientes. Para obter mais informações, consulte [especificando e manipulando falhas em contratos e serviços](specifying-and-handling-faults-in-contracts-and-services.md).  
  
 No entanto, se você estiver depurando um aplicativo, poderá serializar informações de exceção e retorná-la ao cliente usando a <xref:System.ServiceModel.Description.ServiceDebugBehavior> classe.  
  
<a name="BKMK_q6"></a>

## <a name="it-seems-like-one-way-and-request-reply-operations-return-at-roughly-the-same-speed-when-the-reply-contains-no-data-whats-happening"></a>Parece que as operações unidirecionais e de solicitação-resposta retornam com aproximadamente a mesma velocidade quando a resposta não contém dados. O que está acontecendo?  

 Especificar que uma operação é de uma maneira significa apenas que o contrato de operação aceita uma mensagem de entrada e não retorna uma mensagem de saída. No WCF, todas as invocações de cliente retornam quando os dados de saída são gravados na transmissão ou uma exceção é lançada. As operações unidirecionais funcionam da mesma forma e podem gerar se o serviço não puder ser localizado ou bloquear se o serviço não estiver preparado para aceitar os dados da rede. Normalmente, no WCF, isso resulta em chamadas unidirecionais retornando ao cliente mais rapidamente do que solicitação-resposta; Mas qualquer condição que reduz o envio dos dados de saída pela rede reduz a operação unidirecional, bem como operações de solicitação-resposta. Para obter mais informações, consulte [Serviços unidirecionais](./feature-details/one-way-services.md) e [acessando serviços usando um cliente WCF](./feature-details/accessing-services-using-a-client.md).  
  
<a name="BKMK_q77"></a>

## <a name="im-using-an-x509-certificate-with-my-service-and-i-get-a-systemsecuritycryptographycryptographicexception-whats-happening"></a>Estou usando um certificado X. 509 com meu serviço e obtenho um System. Security. Cryptography. CryptographicException. O que está acontecendo?  

 Isso geralmente ocorre depois de alterar a conta de usuário na qual o processo de trabalho do IIS é executado. Por exemplo, no Windows XP, se você alterar a conta de usuário padrão que o Aspnet_wp.exe é executado do ASPNET para uma conta de usuário personalizada, você poderá ver esse erro. Se você estiver usando uma chave privada, o processo que a usa precisará ter permissões para acessar o arquivo que armazena essa chave.  
  
 Se esse for o caso, você deverá conceder privilégios de acesso de leitura à conta do processo para o arquivo que contém a chave privada. Por exemplo, se o processo de trabalho do IIS estiver sendo executado na conta Bob, você precisará dar ao Bob acesso de leitura ao arquivo que contém a chave privada.  
  
 Para obter mais informações sobre como conceder o acesso correto à conta de usuário ao arquivo que contém a chave privada para um certificado X. 509 específico, consulte [como: tornar certificados x. 509 acessíveis ao WCF](./feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md).  
  
<a name="BKMK_q88"></a>

## <a name="i-changed-the-first-parameter-of-an-operation-from-uppercase-to-lowercase-now-my-client-throws-an-exception-whats-happening"></a>Alterei o primeiro parâmetro de uma operação de maiúscula para minúscula; Agora, meu cliente gera uma exceção. O que está acontecendo?  

 Os valores dos nomes de parâmetro na assinatura de operação fazem parte do contrato e diferenciam maiúsculas de minúsculas. Use o <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> atributo quando precisar distinguir entre o nome do parâmetro local e os metadados que descrevem a operação para aplicativos cliente.  
  
<a name="BKMK_q99"></a>

## <a name="im-using-one-of-my-tracing-tools-and-i-get-an-endpointnotfoundexception-whats-happening"></a>Estou usando uma das minhas ferramentas de rastreamento e obtenho um EndpointNotFoundException. O que está acontecendo?  

 Se você estiver usando uma ferramenta de rastreamento que não seja o mecanismo de rastreamento do WCF fornecido pelo sistema e receber um <xref:System.ServiceModel.EndpointNotFoundException> que indica que houve uma incompatibilidade de filtro de endereço, você precisará usar a <xref:System.ServiceModel.Description.ClientViaBehavior> classe para direcionar as mensagens para o utilitário de rastreamento e fazer com que o utilitário redirecione essas mensagens para o endereço do serviço. A <xref:System.ServiceModel.Description.ClientViaBehavior> classe altera o `Via` cabeçalho de endereçamento para especificar o próximo endereço de rede separadamente do receptor final, indicado pelo `To` cabeçalho de endereçamento. No entanto, ao fazer isso, não altere o endereço do ponto de extremidade, que é usado para estabelecer o `To` valor.  
  
 O exemplo de código a seguir mostra um exemplo de arquivo de configuração de cliente.  
  
```xml
<endpoint
  address="http://localhost:8000/MyServer/"  
  binding="wsHttpBinding"  
  bindingConfiguration="WSHttpBinding_IMyContract"  
  behaviorConfiguration="MyClient"
  contract="IMyContract"
  name="WSHttpBinding_IMyContract">  
</endpoint>  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="MyClient">  
      <clientVia viaUri="http://localhost:8001/MyServer/"/>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
```  
  
<a name="BKMK_q10"></a>

## <a name="what-is-the-base-address-how-does-it-relate-to-an-endpoint-address"></a>Qual é o endereço base? Como ele se relaciona a um endereço de ponto de extremidade?  

 Um endereço base é o endereço raiz de uma <xref:System.ServiceModel.ServiceHost> classe. Por padrão, se você adicionar uma <xref:System.ServiceModel.Description.ServiceMetadataBehavior> classe à sua configuração de serviço, o WSDL (Web Services Description Language) para todos os pontos de extremidade publicados pelo host será recuperado do endereço base http, além de qualquer endereço relativo fornecido ao comportamento de metadados, além de "? WSDL". Se você estiver familiarizado com o ASP.NET e o IIS, o endereço base será equivalente ao diretório virtual.  
  
## <a name="sharing-a-port-between-a-service-endpoint-and-a-mex-endpoint-using-the-nettcpbinding"></a>Compartilhando uma porta entre um ponto de extremidade de serviço e um ponto de extremidade MEX usando o NetTcpbinding  

 Se você especificar o endereço base para um serviço como net. TCP://MyServer: 8080/MyService e adicionar os seguintes pontos de extremidade:  
  
```xml  
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
 E se você modificar uma das configurações de NetTcpbinding, conforme mostrado no seguinte trecho de configuração:  
  
```xml  
<bindings>  
  <netTcpBinding>  
    <binding closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" transactionFlow="false" transferMode="Buffered" transactionProtocol="OleTransactions" hostNameComparisonMode="StrongWildcard" listenBacklog="10" maxBufferPoolSize="524288" maxBufferSize="65536" maxConnections="11" maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384"/>  
      <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false"/>  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign"/>  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
 Você verá um erro semelhante ao seguinte: exceção sem tratamento: System. ServiceModel. AddressAlreadyInUseException: já existe um ouvinte no ponto de extremidade IP 0.0.0.0:9000. você pode contornar esse erro especificando uma URL totalmente qualificada com uma porta diferente para o ponto de extremidade MEX, conforme mostrado no seguinte trecho de configuração:  
  
```xml
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="net.tcp://localhost:9001/servicemodelsamples/mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
<a name="BK_MK99"></a>

## <a name="when-calling-a-wcf-web-http-application-from-a-wcf-soap-application-the-service-returns-the-following-error-405-method-not-allowed"></a>Ao chamar um aplicativo Web HTTP WCF de um aplicativo SOAP do WCF, o serviço retorna o seguinte erro: método 405 não permitido  

 Chamar um aplicativo Web HTTP do WCF (um serviço que usa o <xref:System.ServiceModel.WebHttpBinding> e <xref:System.ServiceModel.Description.WebHttpBehavior> ) de um serviço WCF pode gerar a seguinte exceção: ``Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: The remote server returned an unexpected response: (405) Method Not Allowed.`` essa exceção ocorre porque o WCF substitui a saída <xref:System.ServiceModel.OperationContext> pela entrada <xref:System.ServiceModel.OperationContext> . Para resolver esse problema, crie um <xref:System.ServiceModel.OperationContextScope> dentro da operação do serviço http Web do WCF. Por exemplo:  
  
```csharp
public string Echo(string input)  
{  
    using (new OperationContextScope(this.InnerChannel))  
    {  
        return base.Channel.Echo(input);  
    }  
}  
```  
  
## <a name="see-also"></a>Confira também

- [Depurando erros de autenticação do Windows](./feature-details/debugging-windows-authentication-errors.md)
