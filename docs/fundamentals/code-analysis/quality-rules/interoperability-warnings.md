---
title: Portabilidade e regras de interoperabilidade (análise de código)
description: Saiba mais sobre a portabilidade da regra de análise de código e as regras de interoperabilidade
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Portablityrules
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis rules, interoperability rules, portability rules
- portability rules
- warnings, portability
- interoperability rules
- warnings, interoperability
author: gewarren
ms.author: gewarren
ms.openlocfilehash: a20cd77e13c4a8b95633d129990667f0a8de3ee8
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "96584727"
---
# <a name="portability-and-interoperability-rules"></a>Regras de portabilidade e interoperabilidade

As regras de portabilidade dão suporte à portabilidade em diferentes plataformas. As regras de interoperabilidade dão suporte à interação com clientes COM.

## <a name="in-this-section"></a>Nesta seção

| Regra | Descrição |
| - | - |
| [CA1401: P/Invokes não devem estar visíveis](ca1401.md) | Um método público ou protegido em um tipo público tem o atributo System.Runtime.InteropServices.DllImportAttribute (também implementado pela palavra-chave declare em Visual Basic). Esses métodos não devem ser expostos. |
| [CA1416: validar a compatibilidade da plataforma](ca1416.md) | O uso de APIs dependentes de plataforma em um componente faz com que o código não funcione mais em todas as plataformas. |
| [CA1417: não usar `OutAttribute` em parâmetros de cadeia de caracteres para P/Invokes](ca1417.md) | Parâmetros de cadeia de caracteres passados por valor com o `OutAttribute` podem desestabilizar o tempo de execução se a cadeia de caracteres for uma cadeia de caracteres interna. |
