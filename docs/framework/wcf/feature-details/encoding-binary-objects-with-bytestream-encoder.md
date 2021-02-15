---
description: 'Saiba mais sobre: codificando objetos binários com o codificador bytes'
title: Objetos binários de codificação com codificador ByteStream
ms.date: 03/30/2017
ms.assetid: 020ee981-c889-4b12-a3ea-91823ef46444
ms.openlocfilehash: 4ef3d3cd378abacd14dd502530a8090f3982e4ea
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704895"
---
# <a name="encoding-binary-objects-with-bytestream-encoder"></a>Objetos binários de codificação com codificador ByteStream

O envio e o recebimento de dados binários brutos com Windows Communication Foundation (WCF) são configurados usando <xref:System.ServiceModel.Channels.ByteStreamMessageEncodingBindingElement> .  
  
## <a name="byte-stream-message-encoder-architecture"></a>Arquitetura do codificador de mensagens de fluxo de bytes  

 O codificador de mensagem binária usado pelo WCF não tem nenhum recurso para processar, validar ou identificar os dados binários subjacentes na mensagem. O pacote de dados é codificado em XML, enviado, recebido e decodificado. O codificador processa os dados depois de serem passados para o transporte e antes que a mensagem seja enviada para a fila de mensagens. Funcionalmente, o codificador binário encapsula os dados da mensagem em `<binary>` elementos para enviar e remove os elementos depois que a mensagem é recebida.  
  
## <a name="using-the-byte-stream-message-encoder"></a>Usando o codificador de mensagens de fluxo de bytes  

 O exemplo a seguir mostra um contrato de serviço que implementa o codificador de mensagem de fluxo de bytes.  
  
```csharp  
[OperationContract]  
Void Myfunction(Stream stream);  
```  
  
 O exemplo a seguir mostra o serviço que está sendo invocado.  
  
```csharp  
proxy.MyFunction(stream);  
```  
  
 No caso do uso de um serviço que implementa uma infraestrutura de mensagem (como um roteador), a mensagem é processada sem inspecionar, validar ou interagir com a mensagem, conforme mostrado no exemplo a seguir.  
  
```csharp  
[OperationContract]  
void ProcessMessage(Message message) ;  
```  
  
## <a name="scenarios"></a>Cenários  

 O codificador de fluxo de bytes é útil nos cenários a seguir.  
  
- Transferindo uma imagem JPEG entre computadores usando o WCF. Nesse cenário, a imagem será recebida pelo transporte de uma fonte externa e os dados enviados serão os bytes brutos que compõem a imagem. Um serviço receberá os dados binários e exibirá a imagem.  
  
- Ler informações de uma fila de mensagens e processá-las. A mensagem será lida de um Gerenciador de filas de mensagens e transmitida ao canal da fila de mensagens a ser tratada. O canal da fila de mensagens atuará como um Gerenciador de filas na pilha de canais do WCF.  
  
 No caso de envio de uma mensagem por um canal da fila de mensagens, o remetente não tem controle sobre os bytes recebidos do Gerenciador de filas. Se o processo de recebimento não tiver capacidade para ler bytes brutos, a mensagem será recebida como formatada incorretamente e não será processada; Supõe-se que o processo de recebimento terá a capacidade de converter os bytes recebidos de volta em um formato utilizável.
