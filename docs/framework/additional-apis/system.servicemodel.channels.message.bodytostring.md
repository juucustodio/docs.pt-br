---
description: 'Saiba mais sobre: método Message. BodyToString'
title: Método Message. BodyToString (System. ServiceModel. Channels)
ms.date: 11/01/2019
topic_type:
- apiref
api_name:
- System.ServiceModel.Channels.Message.BodyToString
api_location:
- system.servicemodel.dll
api_type:
- Assembly
ms.openlocfilehash: babcd881d191ff46b98e9999c4ff04166479a68d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699370"
---
# <a name="messagebodytostring-method"></a>Método Message. BodyToString

Converte o corpo da mensagem em uma cadeia de caracteres chamando o <xref:System.ServiceModel.Channels.Message.OnBodyToString%2A?displayProperty=nameWithType> método.

```csharp
internal void BodyToString(XmlDictionaryWriter writer);
```

## <a name="parameters"></a>Parâmetros

- `writer` <xref:System.Xml.XmlDictionaryWriter>\
  O gravador usado para converter o corpo da mensagem em uma cadeia de caracteres.

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `Message.BodyToString` método é interno e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.ServiceModel.Channels>

**Assembly:** System.ServiceModel.dll

**.NET Framework versões:** Disponível desde 3,0.
