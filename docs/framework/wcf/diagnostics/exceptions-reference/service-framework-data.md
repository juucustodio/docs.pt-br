---
description: 'Saiba mais sobre: dados do Service Framework'
title: Dados de estrutura de serviço
ms.date: 03/30/2017
ms.assetid: 2a2c8ddc-4e82-4e7f-a79f-97085c469517
ms.openlocfilehash: f2f4645e0a2473e565286a45e6d20e3d1ef7c2f4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686187"
---
# <a name="service-framework-data"></a>Dados de estrutura de serviço

Este tópico lista todas as exceções geradas pelos dados do Service Framework.  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|AddressingExtensionInBadNS|O elemento especificado no namespace especificado não é válido. Isso significa que o elemento especificado é um elemento duplicado ou que não é uma extensão válida porque os elementos de extensão não podem estar no namespace de endereçamento.|  
|BinaryEncoderSessionInvalid|A sessão do codificador binário não é válida porque ocorreu um erro ao decodificar uma mensagem anterior.|  
|CannotDetectAddressingVersion|Não é possível detectar WS-Addressing versão. O EndpointAddress não começa com um elemento.|  
|CouldNotFindNamespaceForPrefix|O prefixo especificado não tem nenhuma associação de namespace no escopo.|  
|EncoderBadContentType|Não é possível processar contentType.|  
|EncoderEnvelopeVersionMismatch|A versão de envelope da mensagem de entrada especificada não corresponde ao codificador especificado. Verifique se a associação está configurada com a mesma versão das mensagens esperadas.|  
|EncoderMessageVersionMismatch|A versão da mensagem de saída especificada não corresponde ao codificador especificado. Verifique se a associação está configurada com a mesma versão da mensagem.|  
|ExtraContentIsPresentInFaultDetail|O conteúdo de linguagem XML adicional está presente no elemento de detalhes de falha. Somente um elemento é permitido.|  
|FilterBadTableType|O interface IMessageFilterTable criado para um filtro não pode ser um MessageFilterTable ou derivado de MessageFilterTable.|  
|FilterTableInvalidForLookup|O estado MessageFilterTable está corrompido. Não é possível executar a pesquisa solicitada.|  
|MandatoryHeaderNotUnderstood|Um ou mais blocos de cabeçalho do protocolo de acesso a objeto simples necessários não foram compreendidos.|  
|MessageBodyIsStream|O corpo da mensagem é um fluxo.|  
|MessageBodyIsUnknown|O formato do corpo da mensagem é desconhecido.|  
|MessageBodyReaderInvalidReadState|O ReadState especificado do leitor de corpo de mensagem não pode ser consumido.|  
|MessageTextEncodingNotSupported|Não há suporte para a codificação de texto especificada que é usada no formato de mensagem de texto.|  
|MissingMessageID|A mensagem de solicitação não tem um cabeçalho MessageID. Um cabeçalho MessageID é necessário para correlacionar uma resposta.|  
|MultipleMessageHeaders|Mais de um cabeçalho com o nome e namespace especificados foram encontrados.|  
|MultipleMessageHeadersWithActor|Mais de um cabeçalho com o nome, namespace e função especificados foram encontrados.|  
|MultipleRelatesToHeaders|Foi encontrado mais de um cabeçalho RelatesTo com a relação especificada. Apenas um é permitido para cada relação.|  
|QueryFunctionTypeNotSupported|Não há suporte para o tipo de retorno especificado para IXsltContextFunction.|  
|QueryIteratorOutOfScope|O XPathNodeIterator foi invalidado. XPathNodeIterators que são passados como argumentos para IXsltContextFunctions só são válidos dentro da função. Eles não podem ser armazenados em cache para uso posterior ou retornados pela função.|  
|QueryVariableNull|Os métodos IXsltContextVariable não podem retornar NULL.|  
|QueryVariableTypeNotSupported|Não há suporte para o tipo derivado IXsltContextVariable especificado.|  
|ReceiveShutdownReturnedMessage|O canal recebeu uma mensagem de entrada inesperada com a ação especificada durante o fechamento. Feche o canal quando não estiver esperando mais mensagens de entrada.|  
|XmlBufferInInvalidState|Ocorreu um erro interno. A operação não pode ser executada devido ao estado do buffer XML.|  
|XmlBufferQuotaExceeded|O tamanho necessário para armazenar em buffer o conteúdo de linguagem XML excedeu a cota de buffer.|
