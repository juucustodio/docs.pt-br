---
description: 'Saiba mais sobre: BinaryMessageEncodingBindingElement'
title: BinaryMessageEncodingBindingElement
ms.date: 03/30/2017
ms.assetid: e2bb3cdd-3bbd-4bb5-85fe-570457500a66
ms.openlocfilehash: e2bc711416c61ca29a93fbf75e4e734137f2b4be
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757872"
---
# <a name="binarymessageencodingbindingelement"></a>BinaryMessageEncodingBindingElement

BinaryMessageEncodingBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp  
class BinaryMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  sint32 MaxReadPoolSize;  
  sint32 MaxSessionSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe BinaryMessageEncodingBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe BinaryMessageEncodingBindingElement tem as propriedades a seguir.  
  
## <a name="maxreadpoolsize"></a>MaxReadPoolSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 Um inteiro que define quantas mensagens podem ser lidas simultaneamente sem alocar novos leitores.  
  
## <a name="maxsessionsize"></a>MaxSessionSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que especifica o tamanho, em bytes, do buffer usado para codificação.  
  
## <a name="maxwritepoolsize"></a>MaxWritePoolSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 Um inteiro que define quantas mensagens podem ser enviadas simultaneamente sem alocar novos gravadores.  
  
## <a name="readerquotas"></a>ReaderQuotas  

 Tipo de dados: XmlDictionaryReaderQuotas  
  
 Tipo de acesso: Somente leitura  
  
 As cotas dos leitores.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>
