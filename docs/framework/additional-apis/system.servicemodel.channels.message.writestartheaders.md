---
description: 'Saiba mais sobre: método Message. WriteStartHeaders'
title: Método Message. WriteStartHeaders (System. ServiceModel. Channels)
ms.date: 11/01/2019
topic_type:
- apiref
api_name:
- System.ServiceModel.Channels.Message.WriteStartHeaders
api_location:
- system.servicemodel.dll
api_type:
- Assembly
ms.openlocfilehash: 20cadf5f1eecf6d8e02c5dc4597889abaef4ec36
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699357"
---
# <a name="messagewritestartheaders-method"></a>Método Message. WriteStartHeaders

Grava o cabeçalho inicial em um arquivo XML chamando o <xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A?displayProperty=nameWithType> método.

```csharp
internal void WriteStartHeaders(XmlDictionaryWriter writer)
```

## <a name="parameters"></a>Parâmetros

- `writer` <xref:System.Xml.XmlDictionaryWriter>\
  O gravador usado para gravar o cabeçalho inicial em um arquivo XML.

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `Message.WriteStartHeaders` método é interno e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.ServiceModel.Channels>

**Assembly:** System.ServiceModel.dll

**.NET Framework versões:** Disponível desde 3,0.
