---
title: Regras de documentação (análise de código)
description: Saiba mais sobre as regras de documentação da regra de análise de código
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation rules
- managed code analysis rules, documentation rules
- warnings, documentation
author: mavasani
ms.author: mavasani
ms.openlocfilehash: 29d1734eec29bd00d456b4b00c48c2e8ef223441
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "96584812"
---
# <a name="documentation-rules"></a>Regras de documentação

As regras de documentação dão suporte à gravação de bibliotecas bem documentadas por meio do uso correto de [comentários de documentação XML](../../../csharp/codedoc.md) para APIs visíveis externamente.

## <a name="in-this-section"></a>Nesta seção

| Regra | Descrição |
| - | - |
| [CA1200: Evitar o uso de marcas cref com um prefixo](ca1200.md) | O atributo [cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) em uma marca de documentação XML significa "referência de código". Ele especifica que o texto interno da marca é um elemento de código, como um tipo, método ou propriedade. Evite usar `cref` marcas com prefixos, pois isso impede que o compilador Verifique as referências. Ele também impede que o IDE (ambiente de desenvolvimento integrado) do Visual Studio Localize e atualize essas referências de símbolo durante refatoração. |
