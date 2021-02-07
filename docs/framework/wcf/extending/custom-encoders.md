---
description: 'Saiba mais sobre: codificadores personalizados'
title: Decodificadores personalizados
ms.date: 03/30/2017
ms.assetid: fa0e1d7f-af36-4bf4-aac9-cd4eab95bc4f
ms.openlocfilehash: 12c706daf025b6ab63bd5c4e2cbb426a2ea83af1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735290"
---
# <a name="custom-encoders"></a>Decodificadores personalizados

Este tópico discute como criar codificadores personalizados.  
  
 No Windows Communication Foundation (WCF), você usa uma *Associação* para especificar como transferir dados em uma rede entre pontos de extremidade. Uma associação é composta de uma sequência de *elementos de associação*. Uma associação inclui elementos de associação de protocolo opcionais, como segurança, um elemento de associação de *codificador de mensagem* necessário e um elemento de associação de transporte necessário. Um codificador de mensagem é representado por um elemento de ligação de codificação de mensagem. Três codificadores de mensagem estão incluídos no WCF: binário, MTOM (mecanismo de otimização de transmissão de mensagens) e texto.  
  
 Um elemento de associação de codificação de mensagem serializa um saída <xref:System.ServiceModel.Channels.Message> e o passa para o transporte, ou recebe a forma serializada de uma mensagem do transporte e a passa para a camada de protocolo, se presente, ou para o aplicativo, se não estiver presente.  
  
 Os codificadores de mensagem <xref:System.ServiceModel.Channels.Message> transformam instâncias de e para uma representação de transmissão. Embora os codificadores sejam descritos como estão acima da camada de transporte na pilha de canais, eles residem dentro da camada de transporte. Os transportes (por exemplo, HTTP) formatam a mensagem de acordo com os requisitos do padrão de transporte. Os codificadores (por exemplo, text xml) apenas codificam a mensagem.  
  
 Ao se conectar a um cliente ou servidor preexistente, talvez você não tenha a opção de usar uma codificação de mensagem específica. No entanto, os serviços WCF podem se tornar acessíveis por meio de vários pontos de extremidade, cada um com um codificador de mensagem diferente. Quando um único codificador não cobre todo o público para seu serviço, considere expor seu serviço em vários pontos de extremidade. Os aplicativos cliente podem escolher o ponto de extremidade que é melhor para eles. O uso de vários pontos de extremidade permite combinar as vantagens de codificadores de mensagens diferentes com outros elementos de ligação.  
  
## <a name="system-provided-encoders"></a>Codificadores de System-Provided  

 O WCF fornece várias associações fornecidas pelo sistema que são projetadas para abranger os cenários de aplicativos mais comuns. Cada uma dessas associações combina um transporte, um codificador de mensagem e outras opções (segurança, por exemplo). Este tópico descreve como estender os codificadores de `Text` `Binary` mensagens, e `MTOM` que estão incluídos no WCF ou criar seu próprio codificador personalizado. O codificador de mensagem de texto dá suporte a codificação XML simples, bem como a codificações SOAP. O modo de codificação XML sem formatação do codificador de mensagem de texto é chamado de codificador POX ("XML antigo") para distingui-lo da codificação SOAP baseada em texto.  
  
 Para obter mais informações sobre as combinações de elementos de associação fornecidos pelas associações fornecidas pelo sistema, consulte a seção correspondente em [escolhendo um transporte](../feature-details/choosing-a-transport.md).  
  
## <a name="how-to-work-with-system-provided-encoders"></a>Como trabalhar com System-Provided codificadores  

 Uma codificação é adicionada a uma associação usando uma classe derivada de <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> .  
  
 O WCF fornece os seguintes tipos de elementos de ligação derivados da <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> classe que pode fornecer texto, binário e codificação de MTOM (mecanismo de otimização de transmissão de mensagens):  
  
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>: O mais interoperável, mas o codificador menos eficiente para mensagens XML. Um serviço Web ou cliente de serviço Web geralmente pode entender XML textual. No entanto, a transmissão de blocos grandes de dados binários como texto não é eficiente.  
  
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>: Representa o elemento de associação que especifica a codificação de caracteres e o controle de versão de mensagem usados para mensagens XML baseadas em binário. Isso é mais eficiente para as opções de codificação, mas o menos interoperável, porque só é suportado por pontos de extremidade do WCF.  
  
- <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>: Representa o elemento de associação que especifica a codificação de caracteres e o controle de versão de mensagem usados para uma mensagem usando uma codificação MTOM (mecanismo de otimização de transmissão de mensagens). O MTOM é uma tecnologia eficiente para transmitir dados binários em mensagens do WCF. O codificador MTOM tenta balancear entre eficiência e interoperabilidade. A codificação MTOM transmite a maioria dos XML na forma textual, mas otimiza grandes blocos de dados binários transmitindo-os como estão, sem conversão em texto.  
  
 O elemento Binding cria um Binary, MTOM ou text <xref:System.ServiceModel.Channels.MessageEncoderFactory> . A fábrica cria uma instância binária, MTOM ou de texto <xref:System.ServiceModel.Channels.MessageEncoderFactory> . Normalmente, há apenas uma única instância. No entanto, se as sessões forem usadas, um codificador diferente poderá ser fornecido para cada sessão. O codificador binário usa isso para coordenar dicionários dinâmicos (consulte infraestrutura XML).  
  
 Os <xref:System.ServiceModel.Channels.MessageEncoder.ReadMessage%2A> <xref:System.ServiceModel.Channels.MessageEncoder.WriteMessage%2A> métodos e são o núcleo dos codificadores. Os métodos fornecem para ler uma mensagem de um fluxo ou de uma <xref:System.Byte> matriz. As matrizes de bytes são usadas quando o transporte está operando no modo de buffer. As mensagens são sempre gravadas em fluxos. Se o transporte precisar armazenar a mensagem em buffer, ele fornecerá um fluxo que faz o buffer.  
  
 O restante dos membros funciona com conteúdo de suporte, tipos de mídia e <xref:System.ServiceModel.Channels.MessageEncoder.MessageVersion%2A> . O transporte chama esses métodos de codificador para testar se a mensagem de entrada pode ser decodificada por ela ou para determinar se a mensagem de saída é válida para esse codificador.  
  
 Cada uma das três implementações de codificador adiciona propriedades que são relevantes para as codificações específicas e são totalmente configuráveis. Os codificadores também expõem as cotas de leitor que têm padrões seguros. Consulte infraestrutura XML para uma discussão sobre as cotas.  
  
## <a name="features-of-system-provided-encoders"></a>Recursos de codificadores de System-Provided  

 Há vários recursos fornecidos pelos codificadores fornecidos pelo sistema.  
  
### <a name="pooling"></a>Agrupamento  

 Cada uma das implementações do codificador tenta o pool o máximo possível. Reduzir as alocações é uma maneira importante de melhorar o desempenho do código gerenciado. Para realizar esse pool, as implementações usam a `SynchronizedPool` classe. O arquivo C# contém uma descrição das otimizações adicionais usadas por essa classe.  
  
 <xref:System.Xml.XmlDictionaryReader> e as <xref:System.Xml.XmlDictionaryWriter> instâncias são agrupadas e reinicializadas para evitar a alocação de novas para cada mensagem. Para os leitores, um `OnClose` retorno de chamada recupera o leitor quando `Close()` é chamado. O codificador também recicla alguns objetos de estado da mensagem usados durante a construção de mensagens. Os tamanhos desses pools são configuráveis pelas `MaxReadPoolSize` `MaxWritePoolSize` Propriedades e em cada uma das três classes derivadas de <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> .  
  
### <a name="binary-encoding"></a>Codificação binária  

 Quando a codificação binária usa sessões, a cadeia de caracteres do dicionário dinâmico deve ser comunicada ao destinatário da mensagem. Isso é feito por meio da prefixação da mensagem com as cadeias de caracteres do dicionário dinâmico. O receptor retira as cadeias de caracteres, adiciona-as à sessão e processa a mensagem. A passagem correta de cadeias de caracteres de dicionário exige que o transporte seja armazenado em buffer.  
  
 As cadeias de caracteres são anexadas à mensagem por um `AddSessionInformationToMessage` método interno. Ele adiciona as cadeias de caracteres como UTF-8 à frente da mensagem prefixada com seu comprimento. O cabeçalho de dicionário inteiro é, então, prefixado com o comprimento de seus dados. A operação inversa é executada por um `ExtractSessionInformationFromMessage` método interno.  
  
 Além de processar as chaves de dicionário dinâmico, as mensagens de sessão em buffer são recebidas de uma maneira exclusiva. Em vez de criar um leitor sobre o documento e processá-lo, o codificador binário usa a `MessagePatterns` classe interna para desconstruir o fluxo binário. A ideia é que a maioria das mensagens tem um determinado conjunto de cabeçalhos que aparecem em uma determinada ordem quando geradas pelo WCF. O sistema de padrão quebra a mensagem com base no que espera. Se for bem-sucedida, ele inicializará um <xref:System.ServiceModel.Channels.MessageHeaders> objeto sem analisar o XML. Caso contrário, ele retornará ao método padrão.  
  
### <a name="mtom-encoding"></a>Codificação de MTOM  

 A <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> classe tem uma propriedade de configuração adicional chamada <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement.MaxBufferSize%2A> . Isso coloca um limite superior na quantidade de dados permitido para o buffer durante o processo de leitura de uma mensagem. O conjunto de informações XML (Infoset) ou outras partes MIME podem precisar ser armazenados em buffer para remontar todas as partes MIME em uma única mensagem.  
  
 Para funcionar corretamente com HTTP, a classe interna de codificador de mensagem MTOM fornece algumas APIs internas para `GetContentType` (que também são internas) e `WriteMessage` , que são públicas e podem ser substituídas. Mais comunicação deve ocorrer para garantir que os valores nos cabeçalhos HTTP concordem com valores nos cabeçalhos MIME.  
  
 Internamente, o codificador de mensagem MTOM usa leitores de texto do WCF e é semelhante ao codificador de texto. A principal diferença é que ele otimiza grandes partes de binários ou "objetos binários grandes" (BLOBs), não convertendo-os em codificação base-64 antes de serem inseridos nos bytes de mensagem. Em vez disso, esses BLOBs são mantidos extraídos e referenciados como anexos MIME.  
  
## <a name="writing-your-own-encoder"></a>Escrevendo seu próprio codificador  

 Para implementar seu próprio codificador de mensagem personalizado, você deve fornecer implementações personalizadas das seguintes classes base abstratas:  
  
- <xref:System.ServiceModel.Channels.MessageEncoder>  
  
- <xref:System.ServiceModel.Channels.MessageEncoderFactory>  
  
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>  
  
 A conversão da representação na memória de uma mensagem em uma representação que pode ser gravada em um fluxo é encapsulada dentro da <xref:System.ServiceModel.Channels.MessageEncoder> classe, que serve como um alocador para leitores XML e gravadores XML que dão suporte a tipos específicos de codificações XML.  
  
- Os principais métodos dessa classe que você deve substituir são:  
  
- <xref:System.ServiceModel.Channels.MessageEncoder.WriteMessage%2A> que pega um <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> objeto e o grava em um <xref:System.IO.Stream> objeto.  
  
- <xref:System.ServiceModel.Channels.MessageEncoder.ReadMessage%2A> que usa um <xref:System.IO.Stream> objeto e um tamanho máximo de cabeçalho e retorna um <xref:System.ServiceModel.Channels.Message> objeto.  
  
 É o código que você escreve nesses métodos que lidam com a conversão entre o protocolo de transporte padrão e sua codificação personalizada.  
  
 Em seguida, você precisa codificar uma classe de fábrica que cria o codificador personalizado. Substitua o <xref:System.ServiceModel.Channels.MessageEncoderFactory.Encoder%2A> para retornar uma instância de seu personalizado <xref:System.ServiceModel.Channels.MessageEncoder> .  
  
 Em seguida, conecte seu personalizado <xref:System.ServiceModel.Channels.MessageEncoderFactory> à pilha de elementos de associação usada para configurar o serviço ou cliente substituindo o <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> método para retornar uma instância dessa fábrica.  
  
 Há dois exemplos fornecidos com o WCF que ilustram esse processo com o código de exemplo: [codificador de mensagem personalizada:](../samples/custom-message-encoder-custom-text-encoder.md) codificador de texto personalizado e [codificador de mensagem personalizada: codificador de compactação](../samples/custom-message-encoder-compression-encoder.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.MessageEncoderFactory>
- <xref:System.ServiceModel.Channels.MessageEncoder>
- [Visão geral da arquitetura de transferência de dados](../feature-details/data-transfer-architectural-overview.md)
- [Escolhendo um codificador de mensagem](../feature-details/choosing-a-message-encoder.md)
- [Selecionando um transporte](../feature-details/choosing-a-transport.md)
