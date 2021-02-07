---
description: 'Saiba mais sobre: retornos de chamada de serialização de Version-Tolerant'
title: Retornos de chamada de serialização tolerantes à versão
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- OnDeserializedAttribute [WCF]
- OnDeserializingAttribute [WCF]
- OnSerializingAttribute [WCF]
- serialization [WCF], setting default values
- OnSerializedAttribute [WCF]
ms.assetid: aa4a3a6f-05ec-4efd-bdbf-2181e13e6468
ms.openlocfilehash: 8ee53e96b90ae6b0f2993a543fc129d75eb3481f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756000"
---
# <a name="version-tolerant-serialization-callbacks"></a>Retornos de chamada de serialização tolerantes à versão

O modelo de programação de contrato de dados dá suporte total aos métodos de retorno de chamada de serialização tolerantes à versão que as <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> classes e dão suporte.  
  
## <a name="version-tolerant-attributes"></a>Atributos de Version-Tolerant  

 Há quatro atributos de retorno de chamada. Cada atributo pode ser aplicado a um método que o mecanismo de serialização/desserialização chama em vários momentos. A tabela a seguir explica quando usar cada atributo.  
  
|Atributo|Quando o método correspondente é chamado|  
|---------------|---------------------------------------------|  
|<xref:System.Runtime.Serialization.OnSerializingAttribute>|Chamado antes de serializar o tipo.|  
|<xref:System.Runtime.Serialization.OnSerializedAttribute>|Chamado após a serialização do tipo.|  
|<xref:System.Runtime.Serialization.OnDeserializingAttribute>|Chamado antes de desserializar o tipo.|  
|<xref:System.Runtime.Serialization.OnDeserializedAttribute>|Chamado após a desserialização do tipo.|  
  
 Os métodos devem aceitar um <xref:System.Runtime.Serialization.StreamingContext> parâmetro.  
  
 Esses métodos se destinam principalmente ao uso com controle de versão ou inicialização. Durante a desserialização, nenhum construtor é chamado. Portanto, os membros de dados podem não ser inicializados corretamente (para valores padrão pretendidos) se os dados desses membros estiverem ausentes no fluxo de entrada, por exemplo, se os dados vierem de uma versão anterior de um tipo que não tem alguns membros de dados. Para corrigir isso, use o método de retorno de chamada marcado com o <xref:System.Runtime.Serialization.OnDeserializingAttribute> , conforme mostrado no exemplo a seguir.  
  
 Você pode marcar apenas um método por tipo com cada um dos atributos de retorno de chamada anteriores.  
  
### <a name="example"></a>Exemplo  

 [!code-csharp[C_DataContract#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#9)]
 [!code-vb[C_DataContract#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#9)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.OnSerializingAttribute>
- <xref:System.Runtime.Serialization.OnSerializedAttribute>
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>
- <xref:System.Runtime.Serialization.OnDeserializedAttribute>
- <xref:System.Runtime.Serialization.StreamingContext>
- [Serialização tolerante a versão](../../../standard/serialization/version-tolerant-serialization.md)
