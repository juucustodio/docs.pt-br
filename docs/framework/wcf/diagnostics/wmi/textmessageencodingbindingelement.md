---
description: 'Saiba mais sobre: TextMessageEncodingBindingElement'
title: TextMessageEncodingBindingElement
ms.date: 03/30/2017
ms.assetid: 885e2d7a-3436-4093-bc5f-0a404c62acdc
ms.openlocfilehash: 9848f1660642f92c4bce3542fbd404f463b8c84d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757339"
---
# <a name="textmessageencodingbindingelement"></a>TextMessageEncodingBindingElement

TextMessageEncodingBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class TextMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  string Encoding;  
  sint32 MaxReadPoolSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe TextMessageEncodingBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe TextMessageEncodingBindingElement tem as seguintes propriedades:  
  
### <a name="encoding"></a>Codificação  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A codificação do conjunto de caracteres a ser usada para emitir mensagens na associação.  
  
### <a name="maxreadpoolsize"></a>MaxReadPoolSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 Um inteiro que define quantas mensagens podem ser lidas simultaneamente sem alocar novos leitores.  
  
### <a name="maxwritepoolsize"></a>MaxWritePoolSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 Um inteiro que define quantas mensagens podem ser enviadas simultaneamente sem alocar novos gravadores.  
  
### <a name="readerquotas"></a>ReaderQuotas  

 Tipo de dados: XmlDictionaryReaderQuotas  
  
 Tipo de acesso: Somente leitura  
  
 As cotas dos leitores.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>
