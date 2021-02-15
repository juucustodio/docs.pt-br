---
title: 'NETSDK1022: itens duplicados foram incluídos.'
description: Como resolver a mensagem de item duplicada com base em inclusões padrão.
author: marcpopMSFT
ms.topic: error-reference
ms.date: 10/9/2020
f1_keywords:
- NETSDK1022
ms.openlocfilehash: c2bdbbb5503e5e4f6e6826f95f5a2cb08c908ceb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717858"
---
# <a name="netsdk1022-duplicate-items-were-included"></a>NETSDK1022: itens duplicados foram incluídos.

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

A partir do Visual Studio 2017/MSBuild versão 15,3, o SDK do .NET inclui automaticamente itens do diretório do projeto por padrão.  Isso inclui `Compile` `Content` destinos e.  Isso deve limpar muito o arquivo do projeto e reduzir a complexidade que você tem.

Você pode reverter para o comportamento anterior definindo a propriedade correta como false.

Exemplo de `Compile` itens:

```xml
<PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```
