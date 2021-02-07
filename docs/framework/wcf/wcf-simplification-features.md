---
description: 'Saiba mais sobre: recursos de simplificação do WCF'
title: funcionalidades de simplificação do WCF
ms.date: 03/30/2017
ms.assetid: 4535a511-6064-4da0-b361-80262a891663
ms.openlocfilehash: cf89ff7775e2a162760c3c6c598a045ddccdf8d8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703372"
---
# <a name="wcf-simplification-features"></a>funcionalidades de simplificação do WCF

Este tópico discute os novos recursos que facilitam escrever aplicativos WCF.

## <a name="simplified-generated-configuration-files"></a>Arquivos de configuração gerados simplificados

Quando você adiciona uma referência de serviço no Visual Studio ou usa a ferramenta SvcUtil.exe, um arquivo de configuração de cliente é gerado. Em versões anteriores do WCF, esses arquivos de configuração continham o valor de cada propriedade de associação mesmo se seu valor fosse o valor padrão. No WCF 4.5, os arquivos de configuração gerados contêm apenas as propriedades de associação que são definidas com um valor não padrão.

Veja a seguir um exemplo de um arquivo de configuração gerado por WCF 3.0.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.serviceModel>
        <bindings>
            <basicHttpBinding>
                <binding name="BasicHttpBinding_IService1" closeTimeout="00:01:00"
                    openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00"
                    allowCookies="false" bypassProxyOnLocal="false"
                    hostNameComparisonMode="StrongWildcard" maxBufferSize="65536"
                    maxBufferPoolSize="524288" maxReceivedMessageSize="65536"
                    messageEncoding="Text" textEncoding="utf-8" transferMode="Buffered"
                    useDefaultWebProxy="true">
                    <readerQuotas maxDepth="32" maxStringContentLength="8192"
                        maxArrayLength="16384" maxBytesPerRead="4096"
                        maxNameTableCharCount="16384" />
                    <security mode="None">
                        <transport clientCredentialType="None" proxyCredentialType="None"
                            realm="" />
                        <message clientCredentialType="UserName" algorithmSuite="Default" />
                    </security>
                </binding>
            </basicHttpBinding>
        </bindings>
        <client>
            <endpoint address="http://localhost:36906/Service1.svc" binding="basicHttpBinding"
                bindingConfiguration="BasicHttpBinding_IService1" contract="IService1"
                name="BasicHttpBinding_IService1" />
        </client>
    </system.serviceModel>
</configuration>
```

Veja a seguir um exemplo do mesmo arquivo de configuração gerado por WCF 4.5.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <system.serviceModel>
        <bindings>
            <basicHttpBinding>
                <binding name="BasicHttpBinding_IService1" />
            </basicHttpBinding>
        </bindings>
        <client>
            <endpoint address="http://localhost:36906/Service1.svc" binding="basicHttpBinding"
                bindingConfiguration="BasicHttpBinding_IService1" contract="IService1"
                name="BasicHttpBinding_IService1" />
        </client>
    </system.serviceModel>
</configuration>
```

## <a name="contract-first-development"></a>Desenvolvimento de primeiro contrato

O WCF agora tem suporte para desenvolvimento do primeiro contrato. A ferramenta de svcutil.exe tem um comutador/serviceContract que permite gerar contratos de serviço e de dados de um documento WSDL.

## <a name="add-service-reference-from-a-portable-subset-project"></a>Adicione uma referência de serviço de um projeto de subconjunto portátil

Os projetos de subconjuntos portáteis permitem que os programadores de assembly .NET mantenham uma única árvore de origem e um sistema de compilação enquanto ainda dão suporte a várias implementações do .NET (desktop, Silverlight, Windows Phone e Xbox). Os projetos de subconjuntos portáteis só fazem referência a bibliotecas portáteis .NET que são assemblies que podem ser usados em qualquer implementação do .NET. A experiência do desenvolvedor é a mesma que adicionar uma referência de serviço dentro de qualquer outro aplicativo cliente WCF. Para obter mais informações, consulte [Adicionar referência de serviço em um projeto de subconjunto portátil](add-service-reference-in-a-portable-subset-project.md).

## <a name="aspnet-compatibility-mode-default-changed"></a>Padrão do modo de compatibilidade do ASP.NET alterado

O WCF fornece o modo de compatibilidade do ASP.NET para conceder aos desenvolvedores acesso completo aos recursos no pipeline HTTP do ASP.NET ao escrever serviços do WCF. Para usar esse modo, você deve definir o `aspNetCompatibilityEnabled` atributo como true na [\<serviceHostingEnvironment>](../configure-apps/file-schema/wcf/servicehostingenvironment.md) seção de web.config. Além disso, qualquer serviço nesse appDomain precisa ter a `RequirementsMode` propriedade <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> definida como <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> or <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required> . Por padrão, <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> agora é definido como <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> e o modelo de aplicativo de serviço WCF padrão define o `aspNetCompatibilityEnabled` atributo como `true` . Para obter mais informações, consulte [What ' s New in Windows Communication Foundation 4,5](whats-new.md) and [WCF Services and ASP.net](./feature-details/wcf-services-and-aspnet.md).

## <a name="streaming-improvements"></a>Melhorias de streaming

- Novo suporte para streaming assíncrono foi adicionado ao WCF. Para habilitar o streaming assíncrono, adicione o comportamento do ponto de extremidade <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior> ao host de serviço e defina sua propriedade <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.AsynchronousSendEnabled%2A> como `true`. Isso pode beneficiar a escalabilidade quando um serviço está enviando mensagens transmitidas a vários clientes que estão lendo lentamente. O WCF não bloqueia mais um thread por cliente e liberará o thread para atender outro cliente.

- Removeu limitações em torno do armazenamento em buffer de mensagens quando um serviço é hospedado no IIS. Em versões anteriores do WCF, ao receber uma mensagem para um serviço hospedado no IIS que usa a transferência da mensagem por streaming, o ASP.NET armazenaria em buffer a mensagem inteira antes de enviar para o WCF. Isso causaria um grande consumo de memória. Esse buffer foi removido no .NET Framework 4,5 e agora os serviços WCF hospedados pelo IIS podem iniciar o processamento do fluxo de entrada antes de a mensagem inteira ter sido recebida, permitindo assim um verdadeiro streaming. Isso permite que o WCF responda imediatamente as mensagens e permite o desempenho aprimorado. Além disso, você não tem mais que especificar um valor para `maxRequestLength`, o limite de tamanho do ASP.NET sobre solicitações de entrada. Se essa propriedade for definida, ela será ignorada. Para obter mais informações sobre como `maxRequestLength` ver o [ \<httpRuntime> elemento Configuration](/previous-versions/dotnet/netframework-1.1/e1f13641(v=vs.71)). Você ainda precisará configurar o maxAllowedContentLength para obter mais informações, consulte [limites de solicitação do IIS](/previous-versions/iis/settings-schema/ms689462(v=vs.90)).

## <a name="new-transport-default-values"></a>Novos valores padrão de transporte

A tabela a seguir descreve as configurações que foram alteradas e onde localizar informações adicionais.

|Propriedade|Ativado|Novo padrão|Mais informações|
|--------------|--------|-----------------|----------------------|
|channelInitializationTimeout|<xref:System.ServiceModel.NetTcpBinding>|30 segundos|Essa propriedade determina quanto tempo uma conexão TCP pode tomar para se autenticar usando o protocolo de enquadramento .NET. Um cliente precisa enviar alguns dados iniciais antes que o servidor tenha informações suficientes para executar a autenticação. Esse tempo limite é feito intencionalmente menor que o ReceiveTimeout (10 min) para que os clientes não autenticados mal-intencionados não mantenham as conexões vinculadas no servidor por muito tempo. O valor padrão é 30 segundos. Para obter mais informações sobre <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.ChannelInitializationTimeout%2A>|
|listenBacklog|<xref:System.ServiceModel.NetTcpBinding>|16 * número de processadores|Esta propriedade de nível de soquete descreve o número de solicitações com aceitações pendentes a serem enfileiradas. Se a fila de pendências de escuta for preenchida, as novas solicitações de soquete serão rejeitadas. Para obter mais informações sobre <xref:System.ServiceModel.NetTcpBinding.ListenBacklog%2A>|
|maxPendingAccepts|ConnectionOrientedTransportBindingElement<br /><br /> SMSvcHost.exe|2 * número de processadores para o transporte<br /><br /> 4 \* números de processadores para SMSvcHost.exe|Essa propriedade limita o número de canais que o servidor pode ter em espera em um ouvinte. Quando MaxPendingAccepts for muito baixo, haverá um pequeno intervalo de tempo no qual todos os canais de espera terão ligado conexões de serviços, mas nenhum novo canal terá começado a escutar. Uma conexão poderá chegar durante esse intervalo e falhará porque nada o está aguardando no servidor. Essa propriedade pode ser configurada definindo a propriedade <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A> como um número maior. Para obter mais informações, consulte <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingAccepts%2A> e [Configurando o serviço de compartilhamento de porta Net. TCP](./feature-details/configuring-the-net-tcp-port-sharing-service.md)|
|maxPendingConnections|ConnectionOrientedTransportBindingElement|12 * número de processadores|Esta propriedade controla quantas conexões um transporte aceitou, mas não foram selecionadas pelo Dispatcher do ServiceModel. Para definir esse valor, use `MaxConnections` na associação ou `maxOutboundConnectionsPerEndpoint` no elemento de associação. Para obter mais informações sobre <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A>|
|receiveTimeout|SMSvcHost.exe|30 segundos|Esta propriedade especifica o tempo limite para ler os dados do enquadramento de TCP e executar a conexão que distribui de conexões subjacentes. Isso existir para colocar um limite na quantidade de tempo que o serviço SMSvcHost.exe é mantido envolvido para ler os dados do preâmbulo de uma conexão de entrada. Para obter mais informações, consulte [Configurando o serviço de compartilhamento de porta Net. TCP](./feature-details/configuring-the-net-tcp-port-sharing-service.md).|

> [!NOTE]
> Essas novas opções são usadas apenas se você implantar o serviço WCF em um computador com o .NET Framework 4.5. Se você implantar o mesmo serviço em um computador com o .NET Framework 4.0, os padrões do .NET Framework 4.0 serão usados. Nesses casos, é recomendável configurar explicitamente esses parâmetros.

## <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas

<xref:System.Xml.XmlDictionaryReaderQuotas> contém valores de cota configuráveis para os leitores de dicionário de XML que limitam a quantidade de memória utilizada por um codificador ao criar uma mensagem. Embora essas quotas sejam configuráveis, os valores padrão foram alterados para diminuir a possibilidade de um desenvolvedor precisar defini-las explicitamente. A cota de `MaxReceivedMessageSize` não foi alterada para que ainda possa limitar o consumo de memória evitando a necessidade de você ter que lidar com a complexidade de <xref:System.Xml.XmlDictionaryReaderQuotas>. A tabela a seguir mostra as cotas, seus novos valores padrão e uma explicação breve do uso de cada cota.

|Nome da Cota|Valor padrão|Descrição|
|----------------|-------------------|-----------------|
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>|Int32.MaxValue|Obtém e define a extensão máxima permitida da matriz. Essa cota limita o tamanho máximo de uma matriz de primitivas que o leitor de XML retorna, inclusive matrizes de bytes. Essa cota não limita o consumo de memória no próprio leitor de XML, mas em qualquer componente que esteja usando o leitor. Por exemplo, quando o <xref:System.Runtime.Serialization.DataContractSerializer> usa um leitor protegido com <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>, ele não desserializa as matrizes de bytes maiores do que essa cota.|
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A>|Int32.MaxValue|Obtém e define o máximo permitido de bytes retornados para cada leitura. Essa cota limita o número de bytes que são lidos em uma única operação de leitura ao ler a marca inicial do elemento e seus atributos. (Em casos não transmitidos por streaming, o nome do elemento em si não é contado na cota.) Ter atributos XML demais pode consumir todo o tempo de processamento de maneira desproporcional porque a exclusividade dos nomes de atributo tem que ser verificada. O <xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A> atenua essa ameaça.|
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A>|128 nós profundos|Essa cota limita a profundidade máxima de aninhamento dos elementos XML. O <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> interage com o <xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A>: o leitor sempre mantém dados na memória para o elemento atual e todos os seus ancestrais, para que o consumo máximo de memória do leitor seja proporcional ao produto dessas duas configurações. Ao desserializar um grafo de objeto aninhado mais profundamente, o desserializador é forçado para acessar a pilha inteira e gerar um <xref:System.StackOverflowException> irrecuperável. Uma correlação direta existe entre aninhamento de XML e aninhamento de objeto para <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Xml.Serialization.XmlSerializer>. O <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> é usado para atenuar essa ameaça.|
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxNameTableCharCount%2A>|Int32.MaxValue|Essa cota limita o número máximo de caracteres permitidos em um nametable. O nametable contém algumas cadeias de caracteres (como namespaces e prefixos) que são encontrados ao processar um documento XML. Como essas cadeias de caracteres são armazenadas em buffer na memória, essa cota é usada para evitar o armazenamento em buffer excessivo quando o streaming é esperado.|
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>|Int32.MaxValue|Essa cota limita o tamanho máximo da cadeia de caracteres que o leitor de XML retorna. Essa cota não limita o consumo de memória no próprio leitor de XML, mas no componente que esteja usando o leitor. Por exemplo, quando o <xref:System.Runtime.Serialization.DataContractSerializer> usa um leitor protegido com <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>, ele não desserializa as cadeias de caracteres maiores do que essa cota.|

> [!IMPORTANT]
> Consulte "usando o XML com segurança" em [considerações de segurança para dados](./feature-details/security-considerations-for-data.md) para obter mais informações sobre como proteger seus dados.

> [!NOTE]
> Essas novas opções são usadas apenas se você implantar o serviço WCF em um computador com o .NET Framework 4.5. Se você implantar o mesmo serviço em um computador com o .NET Framework 4.0, os padrões do .NET Framework 4.0 serão usados. Nesses casos, é recomendável configurar explicitamente esses parâmetros.

## <a name="wcf-configuration-validation"></a>Validação da instalação do WCF

Como parte do processo de compilação dentro do Visual Studio, os arquivos de configuração do WCF agora são validados. Uma lista de erros de validação ou avisos serão exibidos no Visual Studio se a validação falhar.

## <a name="xml-editor-tooltips"></a>Dicas do editor XML

Para ajudar os desenvolvedores novos e existentes do serviço WCF a configurarem os serviços, o editor de XML do Visual Studio agora fornece dicas de ferramenta para cada elemento de configuração e suas propriedades que fazem parte do arquivo de configuração do serviço.

## <a name="basichttpbinding-improvements"></a>Melhorias de BasicHttpBinding

1. Habilita um único ponto de extremidade do WCF para responder a diferentes modos de autenticação.

2. Permite as configurações de segurança de um serviço WCF a serem controladas pelo IIS
