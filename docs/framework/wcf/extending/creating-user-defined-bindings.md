---
description: 'Saiba mais sobre: Criando associações de User-Defined'
title: Criando associações definidas pelo usuário
ms.date: 03/30/2017
helpviewer_keywords:
- user-defined bindings [WCF]
ms.assetid: c4960675-d701-4bc9-b400-36a752fdd08b
ms.openlocfilehash: 9eabb1840f343439d8a8cc79fb0a9b1582b9126d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735394"
---
# <a name="creating-user-defined-bindings"></a>Criando associações definidas pelo usuário

Há várias maneiras de criar associações não fornecidas pelo sistema:  
  
- Crie uma associação personalizada, com base na <xref:System.ServiceModel.Channels.CustomBinding> classe, que é um contêiner que você preenche com elementos de associação. Em seguida, a associação personalizada é adicionada a um ponto de extremidade de serviço. Você pode criar a associação personalizada programaticamente ou em um arquivo de configuração de aplicativo. Para usar um elemento Binding de um arquivo de configuração de aplicativo, o elemento Binding deve ser estendido <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> . Para obter mais informações sobre associações personalizadas, consulte [associações personalizadas](custom-bindings.md) e <xref:System.ServiceModel.Channels.CustomBinding> .  
  
- Você pode criar uma classe que deriva de uma associação padrão. Por exemplo, você pode derivar uma classe de <xref:System.ServiceModel.WSHttpBinding> e substituir <xref:System.ServiceModel.Channels.CustomBinding.CreateBindingElements%2A> o método para obter os elementos de associação e inserir um elemento de ligação personalizado ou estabelecer um valor específico para segurança.  
  
- Você pode criar um novo <xref:System.ServiceModel.Channels.Binding> tipo para controlar completamente toda a implementação de associação.  
  
## <a name="the-order-of-binding-elements"></a>A ordem dos elementos de associação  

 Cada elemento de associação representa uma etapa de processamento ao enviar ou receber mensagens. Em tempo de execução, os elementos de associação criam os canais e ouvintes necessários para criar pilhas de canal de entrada e de saída.  
  
 Há três tipos principais de elementos de associação: elementos de associação de protocolo, elementos de associação de codificação e elementos de associação de transporte.  
  
 Elementos de associação de protocolo – esses elementos representam etapas de processamento de nível superior que atuam em mensagens. Canais e ouvintes criados por esses elementos de ligação podem adicionar, remover ou modificar o conteúdo da mensagem. Uma determinada associação pode ter um número arbitrário de elementos de ligação de protocolo, cada um herdado de <xref:System.ServiceModel.Channels.BindingElement> . O Windows Communication Foundation (WCF) inclui vários elementos de ligação de protocolo, incluindo o <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> e o <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> .  
  
 Elemento de associação de codificação – esses elementos representam transformações entre uma mensagem e uma codificação pronta para transmissão na conexão. As associações típicas do WCF incluem exatamente um elemento de associação de codificação. Exemplos de elementos de associação de codificação incluem o <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> , o <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> e o <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> . Se um elemento de associação de codificação não for especificado para uma associação, uma codificação padrão será usada. O padrão é Text quando o transporte é HTTP e binary de outra forma.  
  
 Elemento de associação de transporte – esses elementos representam a transmissão de uma mensagem de codificação em um protocolo de transporte. As associações típicas do WCF incluem exatamente um elemento de associação de transporte, que é herdado de <xref:System.ServiceModel.Channels.TransportBindingElement> . Exemplos de elementos de associação de transporte incluem o <xref:System.ServiceModel.Channels.TcpTransportBindingElement> , o <xref:System.ServiceModel.Channels.HttpTransportBindingElement> e o <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement> .  
  
 Ao criar novas associações, a ordem dos elementos de associação adicionados é importante. Sempre adicione elementos de associação na seguinte ordem:  
  
|Camada|Opções|Obrigatório|  
|-----------|-------------|--------------|  
|Fluxo de transações|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement?displayProperty=nameWithType>|Não|  
|Confiabilidade|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=nameWithType>|Não|  
|Segurança|<xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType>|Não|  
|Duplex composto|<xref:System.ServiceModel.Channels.CompositeDuplexBindingElement?displayProperty=nameWithType>|Não|  
|Codificação|Texto, binário, MTOM, personalizado|Sim\*|  
|Transport|TCP, pipes nomeados, HTTP, HTTPS, MSMQ, personalizado|Yes|  
  
\*Como uma codificação é necessária para cada associação, se uma codificação não for especificada, o WCF adicionará uma codificação padrão para você. O padrão é Text/XML para os transportes HTTP e HTTPS e, caso contrário, binary.  
  
## <a name="creating-a-new-binding-element"></a>Criando um novo elemento de associação  

 Além dos tipos derivados de <xref:System.ServiceModel.Channels.BindingElement> que são fornecidos pelo WCF, você pode criar seus próprios elementos de ligação. Isso permite que você personalize a maneira como a pilha de associações é criada e os componentes que o acompanham criando as suas próprias <xref:System.ServiceModel.Channels.BindingElement> que podem ser compostas com os outros tipos fornecidos pelo sistema na pilha.  
  
 Por exemplo, se você implementar um `LoggingBindingElement` que forneça a capacidade de registrar a mensagem em um banco de dados, deverá colocá-la acima de um canal de transporte na pilha de canais. Nesse caso, o aplicativo cria uma associação personalizada que criou o `LoggingBindingElement` com `TcpTransportBindingElement` , como no exemplo a seguir.  
  
```csharp  
Binding customBinding = new CustomBinding(  
  new LoggingBindingElement(),
  new TcpTransportBindingElement()  
);  
```  
  
 A maneira como você escreve seu novo elemento de associação depende de sua funcionalidade exata. Um dos exemplos, [Transport: UDP](../samples/transport-udp.md), fornece uma descrição detalhada de como implementar um tipo de elemento de ligação.  
  
## <a name="creating-a-new-binding"></a>Criando uma nova associação  

 Um elemento de Associação criado pelo usuário pode ser usado de duas maneiras. A seção anterior ilustra a primeira maneira: por meio de uma associação personalizada. Uma associação personalizada permite que o usuário crie sua própria associação com base em um conjunto arbitrário de elementos de ligação, incluindo aqueles criados pelo usuário.  
  
 Se você usar a associação em mais de um aplicativo, crie sua própria ligação e estenda o <xref:System.ServiceModel.Channels.Binding> . Isso evita a criação manual de uma associação personalizada toda vez que você desejar usá-la. Uma associação definida pelo usuário permite que você defina o comportamento da associação e inclua elementos de associação definidos pelo usuário. E ele é *previamente empacotado*: você não precisa recompilar a associação sempre que usá-la.  
  
 No mínimo, uma associação definida pelo usuário deve implementar o <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> método e a <xref:System.ServiceModel.Channels.Binding.Scheme%2A> propriedade.  
  
 O <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> método retorna um novo <xref:System.ServiceModel.Channels.BindingElementCollection> que contém os elementos de associação para a associação. A coleção é ordenada e deve conter os elementos de associação de protocolo primeiro, seguidos pelo elemento de associação de codificação, seguido pelo elemento de associação de transporte. Ao usar os elementos de associação fornecidos pelo sistema do WCF, você deve seguir as regras de ordenação do elemento de associação especificadas em [associações personalizadas](custom-bindings.md). Essa coleção nunca deve fazer referência a objetos referenciados dentro da classe de associação definida pelo usuário; Consequentemente, os autores de associação devem retornar um `Clone()` dos <xref:System.ServiceModel.Channels.BindingElementCollection> em cada chamada para <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> .  
  
 A <xref:System.ServiceModel.Channels.Binding.Scheme%2A> propriedade representa o esquema de URI para o protocolo de transporte em uso na associação. Por exemplo, *WSHttpBinding* e *NetTcpBinding* retornam "http" e "net. TCP" de suas respectivas <xref:System.ServiceModel.Channels.Binding.Scheme%2A> Propriedades.  
  
 Para obter uma lista completa de métodos e propriedades opcionais para associações definidas pelo usuário, consulte <xref:System.ServiceModel.Channels.Binding> .  
  
### <a name="example"></a>Exemplo  

 Este exemplo implementa a associação de perfil no `SampleProfileUdpBinding` , que deriva de <xref:System.ServiceModel.Channels.Binding> . O `SampleProfileUdpBinding` contém até quatro elementos de associação dentro dele: um criado pelo usuário `UdpTransportBindingElement` ; e três fornecidos pelo sistema: `TextMessageEncodingBindingElement` , `CompositeDuplexBindingElement` e `ReliableSessionBindingElement` .  
  
```csharp
public override BindingElementCollection CreateBindingElements()  
{
    BindingElementCollection bindingElements = new BindingElementCollection();  
    if (ReliableSessionEnabled)  
    {  
        bindingElements.Add(session);  
        bindingElements.Add(compositeDuplex);  
    }  
    bindingElements.Add(encoding);  
    bindingElements.Add(transport);  
    return bindingElements.Clone();  
}  
```  
  
## <a name="security-restrictions-with-duplex-contracts"></a>Restrições de segurança com contratos duplex  

 Nem todos os elementos de associação são compatíveis entre si. Em particular, há algumas restrições em elementos de associação de segurança quando usadas com contratos duplex.  
  
### <a name="one-shot-security"></a>Segurança de One-Shot  

 Você pode implementar a segurança "One-shot", em que todas as credenciais de segurança necessárias são enviadas em uma única mensagem, definindo o `negotiateServiceCredential` atributo do \<message> elemento de configuração como `false` .  
  
 A autenticação One-Shot não funciona com contratos duplex.  
  
 Para contratos de Request-Reply, a autenticação única funcionará somente se a pilha de associação abaixo do elemento de associação de segurança der suporte à criação <xref:System.ServiceModel.Channels.IRequestChannel> ou <xref:System.ServiceModel.Channels.IRequestSessionChannel> instâncias.  
  
 Para contratos unidirecionais, a autenticação única funciona se a pilha de associação abaixo do elemento de associação de segurança oferecer suporte à criação <xref:System.ServiceModel.Channels.IRequestChannel> de <xref:System.ServiceModel.Channels.IRequestSessionChannel> <xref:System.ServiceModel.Channels.IOutputChannel> instâncias, ou <xref:System.ServiceModel.Channels.IOutputSessionChannel> .  
  
### <a name="cookie-mode-security-context-tokens"></a>Tokens de contexto de segurança no modo de cookie  

 Os tokens de contexto de segurança do modo de cookie não podem ser usados com contratos duplex.  
  
 Para contratos de Request-Reply, os tokens de contexto de segurança no modo de cookie só funcionarão se a pilha de associação abaixo do elemento de associação de segurança oferecer suporte à criação <xref:System.ServiceModel.Channels.IRequestChannel> ou <xref:System.ServiceModel.Channels.IRequestSessionChannel> instâncias.  
  
 Para contratos unidirecionais, os tokens de contexto de segurança no modo de cookie funcionarão se a pilha de associação abaixo do elemento de associação de segurança der suporte à criação <xref:System.ServiceModel.Channels.IRequestChannel> ou <xref:System.ServiceModel.Channels.IRequestSessionChannel> instâncias.  
  
### <a name="session-mode-security-context-tokens"></a>Tokens de contexto de segurança no modo de sessão  

 O modo de sessão SCT funciona para contratos duplex se a pilha de associação abaixo do elemento de associação de segurança dá suporte à criação <xref:System.ServiceModel.Channels.IDuplexChannel> ou <xref:System.ServiceModel.Channels.IDuplexSessionChannel> instâncias.  
  
 O modo de sessão SCT trabalha para Request-Reply contratos se a pilha de associação abaixo do elemento de associação de segurança dá suporte à criação <xref:System.ServiceModel.Channels.IDuplexChannel> de <xref:System.ServiceModel.Channels.IDuplexSessionChannel> instâncias, ou, <xref:System.ServiceModel.Channels.IRequestChannel> <xref:System.ServiceModel.Channels.IRequestSessionChannel> .  
  
 O modo de sessão SCT funciona para contratos de 1 forma se a pilha de associação abaixo do elemento de associação de segurança dá suporte à criação <xref:System.ServiceModel.Channels.IDuplexChannel> de <xref:System.ServiceModel.Channels.IDuplexSessionChannel> <xref:System.ServiceModel.Channels.IRequestChannel> instâncias, ou <xref:System.ServiceModel.Channels.IRequestSessionChannel> .  
  
## <a name="deriving-from-a-standard-binding"></a>Derivando de uma associação padrão  

 Em vez de criar uma classe de associação totalmente nova, talvez seja possível estender uma das associações existentes fornecidas pelo sistema. Assim como no caso anterior, você deve substituir o <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> método e a <xref:System.ServiceModel.Channels.Binding.Scheme%2A> propriedade.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.Binding>
- [Associações personalizadas](custom-bindings.md)
