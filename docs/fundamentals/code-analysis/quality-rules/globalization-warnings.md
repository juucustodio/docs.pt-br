---
title: Regras de globalização (análise de código)
description: Saiba mais sobre regras de globalização de regra de análise de código
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- rules, globalization
- globalization rules
- globalization [Visual Studio], rules
- managed code analysis rules, globalization rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 83ecc52c5e20e074c6c1aed68204a574494f42d5
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "96585001"
---
# <a name="globalization-rules"></a>Regras de globalização

As regras de globalização dão suporte a bibliotecas e aplicativos preparados para o mundo.

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA1303: Não passar literais como parâmetros localizados](ca1303.md)|Um método visível externamente passa um literal de cadeia de caracteres como um parâmetro para um construtor ou método .NET, e essa cadeia de caracteres deve ser localizável.|
|[CA1304: Especificar CultureInfo](ca1304.md)|Um método ou um construtor chama um membro que tem uma sobrecarga que aceita um parâmetro System.Globalization.CultureInfo, e o método ou o construtor não chama a sobrecarga que utiliza o parâmetro CultureInfo. Quando um objeto CultureInfo ou System.IFormatProvider não for fornecido, o valor padrão fornecido pelo membro sobrecarregado poderá não ter o efeito desejado em todas as localidades.|
|[CA1305: Especificar IFormatProvider](ca1305.md)|Um método ou um construtor chama um ou mais membros que têm sobrecargas que aceitam um parâmetro System.IFormatProvider, e o método ou o construtor não chama a sobrecarga que utiliza o parâmetro IFormatProvider. Quando um objeto System.Globalization.CultureInfo ou System.IFormatProvider não for fornecido, o valor padrão fornecido pelo membro sobrecarregado poderá não ter o efeito desejado em todas as localidades.|
|[CA1307: Especificar StringComparison para garantir a clareza](ca1307.md)|Uma operação de comparação de cadeia de caracteres usa uma sobrecarga de método que não define um parâmetro StringComparison.|
|[CA1308: Normalizar cadeias de caracteres em maiúsculas](ca1308.md)|As cadeias de caracteres devem ser normalizadas em maiúsculas. Um pequeno grupo de caracteres não pode fazer uma viagem de ida e volta quando são convertidos em minúsculas.|
|[CA1309: Usar StringComparison ordinal](ca1309.md)|Uma operação de comparação de cadeia de caracteres não linguística não define o parâmetro StringComparison como Ordinal ou OrdinalIgnoreCase. Definindo-se explicitamente o parâmetro como StringComparison.Ordinal ou StringComparison.OrdinalIgnoreCase, o código normalmente ganha velocidade, fica mais correto e se torna mais confiável.|
|[CA1310: Especificar StringComparison para garantir a exatidão](ca1310.md)|Uma operação de comparação de cadeia de caracteres usa uma sobrecarga de método que não define um parâmetro StringComparison e usa a comparação de cadeia de caracteres específica de cultura por padrão.|
|[CA2101: especificar o marshaling para argumentos de cadeia de caracteres P/Invoke](ca2101.md)|Um membro de invocação de plataforma permite chamadores parcialmente confiáveis, tem um parâmetro de cadeia de caracteres e não empacota explicitamente a cadeia de caracteres. Isso pode causar uma vulnerabilidade de segurança em potencial.|
