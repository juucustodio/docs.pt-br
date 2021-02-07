---
description: 'Saiba mais sobre: método XmlReader. CreateSqlReader'
title: Método XmlReader. CreateSqlReader (System.Xml)
ms.date: 10/17/2019
topic_type:
- apiref
api_name:
- System.Xml.XmlReader.CreateSqlReader
api_location:
- system.xml.dll
api_type:
- Assembly
ms.openlocfilehash: 61d594c0438c86863ce4052387439f5483d8a34c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99740426"
---
# <a name="xmlreadercreatesqlreader-method"></a>Método XmlReader.CreateSqlReader

Cria uma nova instância <xref:System.Xml.XmlReader> usando as informações de fluxo, configurações e contexto especificadas para análise.

```csharp
internal static XmlReader CreateSqlReader(Stream input,
  XmlReaderSettings settings, XmlParserContext inputContext)
```

## <a name="parameters"></a>Parâmetros

- `input` <xref:System.IO.Stream>  
  O fluxo que contém os dados XML.

- `settings` <xref:System.Xml.XmlReaderSettings>  
  As configurações para a nova instância <xref:System.Xml.XmlReader>. Este valor pode ser `null`.

- `inputContext` <xref:System.Xml.XmlParserContext>  
  As informações de contexto necessárias para analisar o fragmento XML. Este valor pode ser `null`.

## <a name="returns"></a>Retornos

<xref:System.Xml.XmlReader>  
Um objeto usado para ler os dados XML no fluxo.

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `XmlReader.CreateSqlReader` método é interno e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Xml>

**Assembly:** System.Xml.dll

**.NET Framework versões:** Disponível desde 2,0.
