---
description: 'Saiba mais sobre: tratando exceções e falhas'
title: Lidando com exceções e falhas
ms.date: 03/30/2017
ms.assetid: a64d01c6-f221-4f58-93e5-da4e87a5682e
ms.openlocfilehash: 9851d63705ba8b28819b11e3893bcd6b019d565d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735069"
---
# <a name="handling-exceptions-and-faults"></a>Lidando com exceções e falhas

As exceções são usadas para comunicar erros localmente no serviço ou na implementação do cliente. As falhas, por outro lado, são usadas para comunicar erros entre limites de serviço, como do servidor para o cliente ou vice-versa. Além das falhas, os canais de transporte geralmente usam mecanismos específicos de transporte para comunicar erros no nível de transporte. Por exemplo, o transporte HTTP usa códigos de status como 404 para comunicar uma URL de ponto de extremidade não existente (não há nenhum ponto de extremidade para enviar de volta uma falha). Este documento consiste em três seções que fornecem orientação aos autores de canal personalizados. A primeira seção fornece orientação sobre quando e como definir e lançar exceções. A segunda seção fornece orientação sobre como gerar e consumir falhas. A terceira seção explica como fornecer informações de rastreamento para ajudar o usuário do seu canal personalizado na solução de problemas de aplicativos em execução.  
  
## <a name="exceptions"></a>Exceções  

 Há duas coisas a serem lembradas ao lançar uma exceção: primeiro, ela deve ser de um tipo que permita que os usuários escrevam o código correto que possa reagir adequadamente à exceção. Em segundo lugar, ele precisa fornecer informações suficientes para que o usuário entenda o que deu errado, o impacto da falha e como corrigi-lo. As seções a seguir fornecem orientação sobre tipos de exceção e mensagens para canais de Windows Communication Foundation (WCF). Também há orientações gerais sobre exceções no .NET no documento diretrizes de design para exceções.  
  
### <a name="exception-types"></a>Tipos de exceção  

 Todas as exceções geradas por canais devem ser um <xref:System.TimeoutException?displayProperty=nameWithType> , <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType> ou um tipo derivado de <xref:System.ServiceModel.CommunicationException> . (Exceções como <xref:System.ObjectDisposedException> também podem ser geradas, mas apenas para indicar que o código de chamada tenha usado o canal inutilizadomente. Se um canal for usado corretamente, ele só deverá lançar as exceções determinadas.) O WCF fornece sete tipos de exceção que derivam de <xref:System.ServiceModel.CommunicationException> e são projetados para serem usados por canais. Há outras <xref:System.ServiceModel.CommunicationException> exceções derivadas que são projetadas para serem usadas por outras partes do sistema. Esses tipos de exceção são:  
  
|Tipo de exceção|Significado|Conteúdo de exceção interna|Estratégia de recuperação|  
|--------------------|-------------|-----------------------------|-----------------------|  
|<xref:System.ServiceModel.AddressAlreadyInUseException>|O endereço do ponto de extremidade especificado para escuta já está em uso.|Se presente, fornece mais detalhes sobre o erro de transporte que causou essa exceção. Por exemplo. <xref:System.IO.PipeException>, <xref:System.Net.HttpListenerException> ou <xref:System.Net.Sockets.SocketException> .|Tente um endereço diferente.|  
|<xref:System.ServiceModel.AddressAccessDeniedException>|O processo não tem permissão para acessar o endereço do ponto de extremidade especificado para escuta.|Se presente, fornece mais detalhes sobre o erro de transporte que causou essa exceção. Por exemplo, <xref:System.IO.PipeException>, ou <xref:System.Net.HttpListenerException>.|Tente com credenciais diferentes.|  
|<xref:System.ServiceModel.CommunicationObjectFaultedException>|O <xref:System.ServiceModel.ICommunicationObject> que está sendo usado está no estado com falha (para obter mais informações, consulte [noções básicas sobre alterações de estado](understanding-state-changes.md)). Observe que quando um objeto com várias chamadas pendentes faz a transição para o estado com falha, apenas uma chamada gera uma exceção que está relacionada à falha e o restante das chamadas lançam um <xref:System.ServiceModel.CommunicationObjectFaultedException> . Essa exceção normalmente é gerada porque um aplicativo ignora alguma exceção e tenta usar um objeto já com falha, possivelmente em um thread diferente daquele que capturou a exceção original.|Se presente, fornece detalhes sobre a exceção interna.|Crie um novo objeto. Observe que, dependendo do que causou a <xref:System.ServiceModel.ICommunicationObject> falha em primeiro lugar, pode haver outro trabalho necessário para a recuperação.|  
|<xref:System.ServiceModel.CommunicationObjectAbortedException>|O <xref:System.ServiceModel.ICommunicationObject> que está sendo usado foi anulado (para obter mais informações, consulte [noções básicas sobre alterações de estado](understanding-state-changes.md)). Semelhante a <xref:System.ServiceModel.CommunicationObjectFaultedException> , essa exceção indica que o aplicativo foi chamado <xref:System.ServiceModel.ICommunicationObject.Abort%2A> no objeto, possivelmente de outro thread, e o objeto não pode mais ser usado por esse motivo.|Se presente, fornece detalhes sobre a exceção interna.|Crie um novo objeto. Observe que, dependendo do que causou a <xref:System.ServiceModel.ICommunicationObject> anulação em primeiro lugar, pode haver outro trabalho necessário para a recuperação.|  
|<xref:System.ServiceModel.EndpointNotFoundException>|O ponto de extremidade remoto de destino não está escutando. Isso pode resultar de qualquer parte do endereço do ponto de extremidade estar incorreta, não resolvível ou o ponto de extremidade estar inativo. Os exemplos incluem erro DNS, Gerenciador de filas não disponível e serviço não está em execução.|A exceção interna fornece detalhes, normalmente do transporte subjacente.|Tente um endereço diferente. Como alternativa, o remetente pode aguardar um pouco e tentar novamente no caso de o serviço estar inoperante|  
|<xref:System.ServiceModel.ProtocolException>|Os protocolos de comunicação, conforme descrito pela política do ponto de extremidade, não correspondem entre os pontos de extremidades. Por exemplo, incompatibilidade de tipo de conteúdo de enquadramento ou tamanho máximo de mensagem excedido.|Se presente, fornece mais informações sobre o erro de protocolo específico. Por exemplo, <xref:System.ServiceModel.QuotaExceededException> é a exceção interna quando a causa do erro está excedendo MaxReceivedMessageSize.|Recuperação: Verifique se as configurações de protocolo remetente e recebido correspondem. Uma maneira de fazer isso é importar novamente os metadados do ponto de extremidade de serviço (política) e usar a associação gerada para recriar o canal.|  
|<xref:System.ServiceModel.ServerTooBusyException>|O ponto de extremidade remoto está escutando, mas não está preparado para processar mensagens.|Se estiver presente, a exceção interna fornecerá os detalhes de erro de nível de transporte ou falha de SOAP.|Recuperação: Aguarde e repita a operação mais tarde.|  
|<xref:System.TimeoutException>|A operação não pôde ser concluída dentro do período de tempo limite.|Pode fornecer detalhes sobre o tempo limite.|Aguarde e repita a operação mais tarde.|  
  
 Defina um novo tipo de exceção somente se esse tipo corresponder a uma estratégia de recuperação específica diferente de todos os tipos de exceção existentes. Se você definir um novo tipo de exceção, ele deverá derivar de <xref:System.ServiceModel.CommunicationException> ou de uma de suas classes derivadas.  
  
### <a name="exception-messages"></a>Mensagens de Exceção  

 As mensagens de exceção são destinadas ao usuário não ao programa para que elas forneçam informações suficientes para ajudar o usuário a entender e resolver o problema. As três partes essenciais de uma boa mensagem de exceção são:  
  
 o que aconteceu. Forneça uma descrição clara do problema usando termos relacionados à experiência do usuário. Por exemplo, uma mensagem de exceção incorreta seria "seção de configuração inválida". Isso deixa o usuário se perguntando qual seção de configuração está incorreta e por que está incorreta. Uma mensagem aprimorada seria "seção de configuração inválida \<customBinding> ". Uma mensagem ainda melhor seria "não é possível adicionar o transporte chamado mytransporte à associação chamada myBinding porque a associação já tem um transporte chamado mytransport". Essa é uma mensagem muito específica usando os termos e nomes que o usuário pode identificar facilmente no arquivo de configuração do aplicativo. No entanto, ainda existem alguns componentes-chave ausentes.  
  
 O significado do erro. A menos que a mensagem declare claramente o que o erro significa, é provável que o usuário se pergunte se é um erro fatal ou se pode ser ignorado. Em geral, as mensagens devem conduzir o significado ou o significado do erro. Para melhorar o exemplo anterior, a mensagem poderia ser "falha do ServiceHost ao abrir devido a um erro de configuração: não é possível adicionar o transporte denominado mytransporte à associação chamada myBinding porque a associação já tem um transporte chamado mytransport".  
  
 Como o usuário deve corrigir o problema. A parte mais importante da mensagem é ajudar o usuário a corrigir o problema. A mensagem deve incluir algumas diretrizes ou dicas sobre o que verificar ou corrigir para corrigir o problema. Por exemplo, "falha do ServiceHost ao abrir devido a um erro de configuração: não é possível adicionar o transporte denominado mytransporte à associação chamada myBinding porque a associação já tem um transporte chamado mytransporte. Verifique se há apenas um transporte na associação ".  
  
## <a name="communicating-faults"></a>Falhas de comunicação  

 SOAP 1,1 e SOAP 1,2 definem uma estrutura específica para falhas. Há algumas diferenças entre as duas especificações, mas, em geral, os tipos de mensagem e MessageFault são usados para criar e consumir falhas.  
  
 ![Tratamento de exceções e falhas](./media/wcfc-soap1-1andsoap1-2faultcomparisonc.gif "wcfc_SOAP1-1AndSOAP1-2FaultComparisonc")  
Falha de SOAP 1,2 (esquerda) e falha de SOAP 1,1 (direita). Observe que, em SOAP 1,1, somente o elemento fault é qualificado como namespace.  
  
 O SOAP define uma mensagem de falha como uma mensagem que contém apenas um elemento Fault (um elemento cujo nome é `<env:Fault>` ) como um filho de `<env:Body>` . O conteúdo do elemento Fault difere ligeiramente entre SOAP 1,1 e SOAP 1,2, como mostra a Figura 1. No entanto, a <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType> classe normaliza essas diferenças em um modelo de objeto:  
  
```csharp
public abstract class MessageFault  
{  
    protected MessageFault();  
  
    public virtual string Actor { get; }  
    public virtual string Node { get; }  
    public static string DefaultAction { get; }  
    public abstract FaultCode Code { get; }  
    public abstract bool HasDetail { get; }  
    public abstract FaultReason Reason { get; }  
  
    public T GetDetail<T>();  
    public T GetDetail<T>( XmlObjectSerializer serializer);  
    public System.Xml.XmlDictionaryReader GetReaderAtDetailContents();  
  
    // other methods omitted  
}  
```  
  
 A `Code` propriedade corresponde ao `env:Code` (ou `faultCode` em SOAP 1,1) e identifica o tipo de falha. O SOAP 1,2 define cinco valores permitidos para `faultCode` (por exemplo, remetente e destinatário) e define um `Subcode` elemento que pode conter qualquer valor de subcódigo. (Consulte a [especificação SOAP 1,2](https://www.w3.org/TR/soap12-part1/#tabsoapfaultcodes) para obter a lista de códigos de falha permitidos e seu significado.) O SOAP 1,1 tem um mecanismo ligeiramente diferente: ele define quatro `faultCode` valores (por exemplo, cliente e servidor) que podem ser estendidos definindo-se totalmente novos ou usando a notação de ponto para criar mais específico `faultCodes` , por exemplo, Client. Authentication.  
  
 Quando você usa MessageFault para programar falhas, o FaultCode.Name e o FaultCode. namespace são mapeados para o nome e o namespace do SOAP 1,2 `env:Code` ou soap 1,1 `faultCode` . O subcódigo FaultCode. é mapeado para `env:Subcode` para soap 1,2 e é nulo para soap 1,1.  
  
 Você deve criar novos subcódigos de falha (ou novos códigos de falha se estiver usando SOAP 1,1) se for interessante distinguir programaticamente uma falha. Isso é análogo à criação de um novo tipo de exceção. Evite usar a notação de ponto com os códigos de falha SOAP 1,1. (O [perfil básico WS-I](http://www.ws-i.org/Profiles/BasicProfile-1.1-2004-08-24.html#SOAP_Custom_Fault_Codes) também desencoraja o uso da notação de ponto de código de falha.)  
  
```csharp
public class FaultCode  
{  
    public FaultCode(string name);  
    public FaultCode(string name, FaultCode subCode);  
    public FaultCode(string name, string ns);  
    public FaultCode(string name, string ns, FaultCode subCode);  
  
    public bool IsPredefinedFault { get; }  
    public bool IsReceiverFault { get; }  
    public bool IsSenderFault { get; }  
    public string Name { get; }  
    public string Namespace { get; }  
    public FaultCode SubCode { get; }  
  
//  methods omitted  
  
}  
```  
  
 A `Reason` propriedade corresponde ao `env:Reason` (ou `faultString` em SOAP 1,1) uma descrição legível por humanos da condição de erro análoga à mensagem de uma exceção. A `FaultReason` classe (e SOAP `env:Reason/faultString` ) tem suporte interno para ter várias traduções no interesse da globalização.  
  
```csharp
public class FaultReason  
{  
    public FaultReason(FaultReasonText translation);  
    public FaultReason(IEnumerable<FaultReasonText> translations);  
    public FaultReason(string text);  
  
    public SynchronizedReadOnlyCollection<FaultReasonText> Translations
    {
       get;
    }  
  
 }  
```  
  
 Os conteúdos de detalhes de falha são expostos em MessageFault usando vários métodos `GetDetail` \<T> , incluindo e `GetReaderAtDetailContents` (). O detalhe da falha é um elemento opaco para a realização de detalhes adicionais sobre a falha. Isso é útil se houver alguns detalhes estruturados arbitrários que você deseja transportar com a falha.  
  
### <a name="generating-faults"></a>Gerando falhas  

 Esta seção explica o processo de gerar uma falha em resposta a uma condição de erro detectada em um canal ou em uma propriedade de mensagem criada pelo canal. Um exemplo típico é enviar de volta uma falha em resposta a uma mensagem de solicitação que contém dados inválidos.  
  
 Ao gerar uma falha, o canal personalizado não deve enviar a falha diretamente, em vez disso, ele deve gerar uma exceção e permitir que a camada acima decida se deseja converter essa exceção em uma falha e como enviá-la. Para auxiliar nessa conversão, o canal deve fornecer uma `FaultConverter` implementação que possa converter a exceção gerada pelo canal personalizado para a falha apropriada. `FaultConverter` é definido como:  
  
```csharp
public class FaultConverter  
{  
    public static FaultConverter GetDefaultFaultConverter(  
                                   MessageVersion version);  
    protected abstract bool OnTryCreateFaultMessage(  
                                   Exception exception,
                                   out Message message);  
    public bool TryCreateFaultMessage(  
                                   Exception exception,
                                   out Message message);  
}  
```  
  
 Cada canal que gera falhas personalizadas deve implementá `FaultConverter` -la e retorná-la de uma chamada para `GetProperty<FaultConverter>` . A `OnTryCreateFaultMessage` implementação personalizada deve converter a exceção em uma falha ou delegar para o canal interno `FaultConverter` . Se o canal for um transporte, ele deverá converter a exceção ou o delegado para o codificador `FaultConverter` ou o padrão `FaultConverter` fornecido no WCF. O padrão `FaultConverter` converte erros correspondentes às mensagens de falha especificadas por WS-Addressing e SOAP. Aqui está um exemplo de `OnTryCreateFaultMessage` implementação.  
  
```csharp
public override bool OnTryCreateFaultMessage(Exception exception,
                                             out Message message)  
{  
    if (exception is ...)  
    {  
        message = ...;  
        return true;  
    }  
  
#if IMPLEMENTING_TRANSPORT_CHANNEL  
    FaultConverter encoderConverter =
                    this.encoder.GetProperty<FaultConverter>();  
    if ((encoderConverter != null) &&
        (encoderConverter.TryCreateFaultMessage(  
         exception, out message)))  
    {  
        return true;  
    }  
  
    FaultConverter defaultConverter =
                   FaultConverter.GetDefaultFaultConverter(  
                   this.channel.messageVersion);  
    return defaultConverter.TryCreateFaultMessage(  
                   exception,
                   out message);  
#else  
    FaultConverter inner =
                   this.innerChannel.GetProperty<FaultConverter>();  
    if (inner != null)  
    {  
        return inner.TryCreateFaultMessage(exception, out message);  
    }  
    else  
    {  
        message = null;  
        return false;  
    }  
#endif  
}  
```  
  
 Uma implicação desse padrão é que as exceções geradas entre camadas para condições de erro que exigem falhas devem conter informações suficientes para o gerador de falhas correspondente criar a falha correta. Como um autor de canal personalizado, você pode definir tipos de exceção que correspondam a diferentes condições de falha se essas exceções ainda não existirem. Observe que as exceções que atravessam as camadas de canal devem comunicar a condição de erro em vez dos dados de falha opacos.  
  
### <a name="fault-categories"></a>Categorias de falha  

 Em geral, há três categorias de falhas:  
  
1. Falhas que são disseminadas em toda a pilha. Essas falhas podem ser encontradas em qualquer camada na pilha de canais, por exemplo, InvalidCardinalityAddressingException.  
  
2. Falhas que podem ser encontradas em qualquer lugar acima de uma determinada camada na pilha, por exemplo, alguns erros que pertencem a uma transação fluida ou a funções de segurança.  
  
3. Falhas direcionadas a uma única camada na pilha, por exemplo, erros como falhas de número de sequência do WS-RM.  
  
 Categoria 1. Falhas geralmente são WS-Addressing e falhas de SOAP. A `FaultConverter` classe base fornecida pelo WCF converte erros correspondentes a mensagens de falha especificadas por WS-Addressing e SOAP para que você não precise manipular a conversão dessas exceções por conta própria.  
  
 Categoria 2. As falhas ocorrem quando uma camada adiciona uma propriedade à mensagem que não consome completamente as informações da mensagem que pertencem a essa camada. Os erros podem ser detectados mais tarde, quando uma camada superior solicita que a propriedade de mensagem processe as informações da mensagem. Esses canais devem implementar o `GetProperty` especificado anteriormente para permitir que a camada superior envie de volta a falha correta. Um exemplo disso é o TransactionMessageProperty. Essa propriedade é adicionada à mensagem sem validar completamente todos os dados no cabeçalho (isso pode envolver o contato com o coordenador de transações distribuídas (DTC).  
  
 Categoria 3. As falhas são geradas e enviadas por uma única camada no processador. Portanto, todas as exceções estão contidas na camada. Para melhorar a consistência entre os canais e facilitar a manutenção, seu canal personalizado deve usar o padrão especificado anteriormente para gerar mensagens de falha mesmo para falhas internas.  
  
### <a name="interpreting-received-faults"></a>Interpretando falhas recebidas  

 Esta seção fornece diretrizes para gerar a exceção apropriada ao receber uma mensagem de falha. A árvore de decisão para processar uma mensagem em cada camada na pilha é a seguinte:  
  
1. Se a camada considerar a mensagem como inválida, a camada deverá fazer o processamento de ' mensagem inválida '. Esse processamento é específico para a camada, mas pode incluir descartar a mensagem, rastrear ou lançar uma exceção que é convertida em uma falha. Exemplos incluem segurança que recebe uma mensagem que não está protegida corretamente ou que o RM recebe uma mensagem com um número de sequência inválido.  
  
2. Caso contrário, se a mensagem for uma mensagem de falha que se aplica especificamente à camada e a mensagem não for significativa fora da interação da camada, a camada deverá tratar a condição de erro. Um exemplo disso é que uma sequência RM recusou a falha que não faz sentido para camadas acima do canal do RM e que implica a falha no canal do RM e o lançamento de operações pendentes.  
  
3. Caso contrário, a mensagem deve ser retornada de Request () ou Receive (). Isso inclui casos em que a camada reconhece a falha, mas a falha apenas indica que uma solicitação falhou e não implica a falha do canal e o lançamento de operações pendentes. Para melhorar a usabilidade nesse caso, a camada deve implementar `GetProperty<FaultConverter>` e retornar uma `FaultConverter` classe derivada que possa converter a falha em uma exceção substituindo `OnTryCreateException` .  
  
 O modelo de objeto a seguir dá suporte à conversão de mensagens em exceções:  
  
```csharp
public class FaultConverter  
{  
    public static FaultConverter GetDefaultFaultConverter(  
                                  MessageVersion version);  
    protected abstract bool OnTryCreateException(  
                                 Message message,
                                 MessageFault fault,
                                 out Exception exception);  
    public bool TryCreateException(  
                                 Message message,
                                 MessageFault fault,
                                 out Exception exception);  
}  
```  
  
 Uma camada de canal pode implementar `GetProperty<FaultConverter>` para dar suporte à conversão de mensagens de falha em exceções. Para fazer isso, substitua `OnTryCreateException` e inspecione a mensagem de falha. Se for reconhecido, faça a conversão, caso contrário, peça ao canal interno para convertê-lo. Os canais de transporte devem delegar para `FaultConverter.GetDefaultFaultConverter` obter o padrão SOAP/WS-Addressing com falha.  
  
 Uma implementação típica tem esta aparência:  
  
```csharp
public override bool OnTryCreateException(  
                            Message message,
                            MessageFault fault,
                            out Exception exception)  
{  
    if (message.Action == "...")  
    {  
        exception = ...;  
        return true;  
    }  
    // OR  
    if ((fault.Code.Name == "...") && (fault.Code.Namespace == "..."))  
    {  
        exception = ...;  
        return true;  
    }  
  
    if (fault.IsMustUnderstand)  
    {  
        if (fault.WasHeaderNotUnderstood(  
                   message.Headers, "...", "..."))  
        {  
            exception = new ProtocolException(...);  
            return true;  
        }  
    }  
  
#if IMPLEMENTING_TRANSPORT_CHANNEL  
    FaultConverter encoderConverter =
              this.encoder.GetProperty<FaultConverter>();  
    if ((encoderConverter != null) &&
        (encoderConverter.TryCreateException(  
                              message, fault, out exception)))  
    {  
        return true;  
    }  
  
    FaultConverter defaultConverter =  
             FaultConverter.GetDefaultFaultConverter(  
                             this.channel.messageVersion);  
    return defaultConverter.TryCreateException(  
                             message, fault, out exception);  
#else  
    FaultConverter inner =
                    this.innerChannel.GetProperty<FaultConverter>();  
    if (inner != null)  
    {  
        return inner.TryCreateException(message, fault, out exception);  
    }  
    else  
    {  
        exception = null;  
        return false;  
    }  
#endif  
}  
```  
  
 Para condições de falha específicas que têm cenários de recuperação distintos, considere definir uma classe derivada de `ProtocolException` .  
  
### <a name="mustunderstand-processing"></a>Processamento de MustUnderstand  

 O SOAP define uma falha geral para sinalizar que um cabeçalho necessário não foi compreendido pelo destinatário. Essa falha é conhecida como a `mustUnderstand` falha. No WCF, os canais personalizados nunca geram `mustUnderstand` falhas. Em vez disso, o Dispatcher do WCF, que está localizado na parte superior da pilha de comunicação do WCF, verifica se todos os cabeçalhos que foram marcados como MustUnderstand = true foram compreendidos pela pilha subjacente. Se algum não tiver sido compreendido, uma `mustUnderstand` falha será gerada nesse ponto. (O usuário pode optar por desativar esse `mustUnderstand` processamento e fazer com que o aplicativo receba todos os cabeçalhos de mensagem. Nesse caso, o aplicativo é responsável por executar o `mustUnderstand` processamento.) A falha gerada inclui um cabeçalho não compreendido que contém os nomes de todos os cabeçalhos com MustUnderstand = true que não foram compreendidos.  
  
 Se o canal de protocolo enviar um cabeçalho personalizado com MustUnderstand = true e receber uma `mustUnderstand` falha, ele deverá descobrir se a falha é devido ao cabeçalho enviado. Há dois membros na `MessageFault` classe que são úteis para isso:  
  
```csharp
public class MessageFault  
{  
    ...  
    public bool IsMustUnderstandFault { get; }  
    public static bool WasHeaderNotUnderstood(MessageHeaders headers,
        string name, string ns) { }  
    ...  
  
}  
```  
  
 `IsMustUnderstandFault` retorna `true` se a falha for uma `mustUnderstand` falha. `WasHeaderNotUnderstood` retorna `true` se o cabeçalho com o nome e o namespace especificados está incluído na falha como um cabeçalho não compreendido.  Caso contrário, ele retornará `false`.  
  
 Se um canal emitir um cabeçalho que está marcado como MustUnderstand = true, essa camada também deverá implementar o padrão de API de geração de exceção e converter as `mustUnderstand` falhas causadas por esse cabeçalho em uma exceção mais útil, conforme descrito anteriormente.  
  
## <a name="tracing"></a>Rastreamento  

 O .NET Framework fornece um mecanismo para rastrear a execução do programa como uma maneira de ajudar a diagnosticar aplicativos de produção ou problemas intermitentes em que não é possível apenas anexar um depurador e percorrer o código. Os principais componentes desse mecanismo estão no <xref:System.Diagnostics?displayProperty=nameWithType> namespace e consistem em:  
  
- <xref:System.Diagnostics.TraceSource?displayProperty=nameWithType>, que é a fonte de informações de rastreamento a ser escrita, <xref:System.Diagnostics.TraceListener?displayProperty=nameWithType> , que é uma classe base abstrata para ouvintes concretos que recebem as informações a serem rastreadas do <xref:System.Diagnostics.TraceSource> e a saída para um destino específico do ouvinte. Por exemplo, <xref:System.Diagnostics.XmlWriterTraceListener> gera informações de rastreamento para um arquivo XML. Por fim, <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType> , que permite que o usuário do aplicativo controle o detalhamento de rastreamento e normalmente é especificado na configuração.  
  
- Além dos componentes principais, você pode usar a ferramenta do [Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) para exibir e Pesquisar rastreamentos do WCF. A ferramenta foi projetada especificamente para arquivos de rastreamento gerados pelo WCF e escrito usando o <xref:System.Diagnostics.XmlWriterTraceListener> . A figura a seguir mostra os vários componentes envolvidos no rastreamento.  
  
 ![Tratamento de exceções e falhas](./media/wcfc-tracinginchannelsc.gif "wcfc_TracingInChannelsc")  
  
### <a name="tracing-from-a-custom-channel"></a>Rastreamento de um canal personalizado  

 Os canais personalizados devem gravar mensagens de rastreamento para auxiliar no diagnóstico de problemas quando não é possível anexar um depurador ao aplicativo em execução. Isso envolve duas tarefas de alto nível: instanciar um <xref:System.Diagnostics.TraceSource> e chamar seus métodos para gravar rastreamentos.  
  
 Ao instanciar um <xref:System.Diagnostics.TraceSource> , a cadeia de caracteres que você especifica se torna o nome dessa fonte. Esse nome é usado para configurar (habilitar/desabilitar/definir o nível de rastreamento) a origem do rastreamento. Ele também aparece na saída de rastreamento em si. Os canais personalizados devem usar um nome de origem exclusivo para ajudar os leitores da saída de rastreamento a entender de onde vêm as informações de rastreamento. O uso do nome do assembly que está gravando as informações como o nome da origem do rastreamento é a prática comum. Por exemplo, o WCF usa System. ServiceModel como a origem do rastreamento para informações gravadas do assembly System. ServiceModel.  
  
 Depois de ter uma origem de rastreamento, você chama <xref:System.Diagnostics.TraceSource.TraceData%2A> seus <xref:System.Diagnostics.TraceSource.TraceEvent%2A> métodos, ou <xref:System.Diagnostics.TraceSource.TraceInformation%2A> para gravar entradas de rastreamento para os ouvintes de rastreamento. Para cada entrada de rastreamento que você escreve, você precisa classificar o tipo de evento como um dos tipos de evento definidos em <xref:System.Diagnostics.TraceEventType> . Essa classificação e a configuração de nível de rastreamento na configuração determinam se a entrada de rastreamento é a saída para o ouvinte. Por exemplo, definir o nível de rastreamento na configuração `Warning` para `Warning` permitir `Error` e `Critical` rastrear entradas a serem gravadas, mas bloqueia informações e entradas detalhadas. Aqui está um exemplo de instanciação de uma origem de rastreamento e gravação de uma entrada no nível de informação:  
  
```csharp
using System.Diagnostics;  
//...  
TraceSource udpSource = new TraceSource("Microsoft.Samples.Udp");  
//...  
udpsource.TraceInformation("UdpInputChannel received a message");  
```  
  
> [!IMPORTANT]
> É altamente recomendável que você especifique um nome de origem de rastreamento que seja exclusivo para seu canal personalizado para ajudar os leitores de saída de rastreamento a entender de onde provém a saída.  
  
#### <a name="integrating-with-the-trace-viewer"></a>Integração com o Visualizador de rastreamento  

 Os rastreamentos gerados pelo canal podem ser impressos em um formato legível pela [ferramenta do Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) usando <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> como o ouvinte de rastreamento. Isso não é algo que você, como desenvolvedor do canal, precisa fazer. Em vez disso, é o usuário do aplicativo (ou a pessoa que está Solucionando problemas do aplicativo) que precisa configurar esse ouvinte de rastreamento no arquivo de configuração do aplicativo. Por exemplo, a configuração a seguir gera informações de rastreamento de <xref:System.ServiceModel?displayProperty=nameWithType> e `Microsoft.Samples.Udp` para o arquivo chamado `TraceEventsFile.e2e` :  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <!-- configure System.ServiceModel trace source -->  
      <source name="System.ServiceModel" switchValue="Verbose"
              propagateActivity="true">  
        <listeners>  
          <add name="e2e" />  
        </listeners>  
      </source>  
      <!-- configure Microsoft.Samples.Udp trace source -->  
      <source name="Microsoft.Samples.Udp" switchValue="Verbose" >  
        <listeners>  
          <add name="e2e" />  
        </listeners>  
      </source>  
    </sources>  
    <!--   
    Define a shared trace listener that outputs to TraceFile.e2e  
    The listener name is e2e   
    -->  
    <sharedListeners>  
      <add name="e2e" type="System.Diagnostics.XmlWriterTraceListener"  
        initializeData=".\TraceFile.e2e"/>  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
</configuration>  
```  
  
#### <a name="tracing-structured-data"></a>Rastreando dados estruturados  

 <xref:System.Diagnostics.TraceSource?displayProperty=nameWithType> tem um <xref:System.Diagnostics.TraceSource.TraceData%2A> método que usa um ou mais objetos que devem ser incluídos na entrada de rastreamento. Em geral, o <xref:System.Object.ToString%2A?displayProperty=nameWithType> método é chamado em cada objeto e a cadeia de caracteres resultante é gravada como parte da entrada de rastreamento. Ao usar <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> para os rastreamentos de saída, você pode passar um <xref:System.Xml.XPath.IXPathNavigable?displayProperty=nameWithType> como o objeto de dados para <xref:System.Diagnostics.TraceSource.TraceData%2A> . A entrada de rastreamento resultante inclui o XML fornecido pelo <xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType> . Aqui está um exemplo de entrada com dados de aplicativo XML:  
  
```xml  
<E2ETraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2ETraceEvent">  
  <System xmlns="...">  
    <EventID>12</EventID>  
    <Type>3</Type>  
    <SubType Name="Information">0</SubType>  
    <Level>8</Level>  
    <TimeCreated SystemTime="2006-01-13T22:58:03.0654832Z" />  
    <Source Name="Microsoft.ServiceModel.Samples.Udp" />  
    <Correlation ActivityID="{00000000-0000-0000-0000-000000000000}" />  
    <Execution  ProcessName="UdpTestConsole"
                ProcessID="3348" ThreadID="4" />  
    <Channel />  
    <Computer>COMPUTER-LT01</Computer>  
  </System>  
<!-- XML application data -->  
  <ApplicationData>  
  <TraceData>  
   <DataItem>  
   <TraceRecord
     Severity="Information"  
     xmlns="…">  
        <TraceIdentifier>some trace id</TraceIdentifier>  
        <Description>EndReceive called</Description>  
        <AppDomain>UdpTestConsole.exe</AppDomain>  
        <Source>UdpInputChannel</Source>  
      </TraceRecord>  
    </DataItem>  
  </TraceData>  
  </ApplicationData>  
</E2ETraceEvent>  
```  
  
 O Visualizador de rastreamento do WCF compreende o esquema do `TraceRecord` elemento mostrado anteriormente e extrai os dados de seus elementos filho e os exibe em um formato tabular. Seu canal deve usar esse esquema ao rastrear dados de aplicativo estruturados para ajudar a Svctraceviewer.exe os usuários a ler os dados.
