---
description: 'Saiba mais sobre: MtomMessageEncodingBindingElement'
title: MtomMessageEncodingBindingElement
ms.date: 03/30/2017
ms.assetid: 4a9c6c3d-e561-4b2d-a693-7e84bdd3534a
ms.openlocfilehash: f06e3d7266c4f7e6f9b4639f7d82941cbabb5dd3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803133"
---
# <a name="mtommessageencodingbindingelement"></a>MtomMessageEncodingBindingElement

MtomMessageEncodingBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class MtomMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  string Encoding;  
  sint32 MaxReadPoolSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe MtomMessageEncodingBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe MtomMessageEncodingBindingElement tem as seguintes propriedades:  
  
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

- <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>
