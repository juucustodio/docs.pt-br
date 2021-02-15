---
title: Bibliotecas do Framework
description: Saiba como as bibliotecas fornecem implementações para muitos algoritmos, funcionalidades do utilitário e tipos gerais e específicos do aplicativo.
author: richlander
ms.date: 06/20/2016
ms.assetid: 7b77b6c1-8367-4602-bff3-91e4c05ac643
ms.openlocfilehash: 4e71f81b0dd72f4569d8b6b319b9e97491533d28
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438206"
---
# <a name="framework-libraries"></a>Bibliotecas do Framework

O .NET tem um conjunto padrão expansivo de bibliotecas de classes, conhecido como as bibliotecas de classes base (conjunto principal) ou as bibliotecas de classes .NET Framework (conjunto completo). Essas bibliotecas fornecem implementações para muitos algoritmos, funcionalidades do utilitário e tipos gerais e específicos do aplicativo. Tanto bibliotecas comerciais quanto comunitárias são criadas com base nas bibliotecas de classes .NET Framework, fornecendo bibliotecas off-the-shelf fáceis de usar para uma amplo conjunto de tarefas de computação.

Um subconjunto dessas bibliotecas é fornecido com cada implementação do .NET. APIs de BCL (bibliotecas de classes base) são esperadas com qualquer implementação do .NET, porque os desenvolvedores desejarão tê-las e porque bibliotecas populares precisarão delas para serem executadas. Bibliotecas específicas de aplicativo acima da BCL, como ASP.NET, não estarão disponíveis em todas as implementações do .NET.

## <a name="base-class-libraries"></a>Bibliotecas de classes base

As BCL fornecem a funcionalidade de utilitário e tipos mais básicos e são a base de todas as outras bibliotecas de classes do .NET. Elas têm o objetivo de fornecer implementações de caráter bastante geral, sem nenhum desvio para nenhuma carga de trabalho. O desempenho é sempre uma consideração importante, já que os aplicativos podem preferir uma política específica como baixa latência para alta taxa de transferência ou memória insuficiente para baixo uso de CPU. Essas bibliotecas estão destinadas a, em termos gerais, serem de alto desempenho e adotarem uma abordagem intermediária acordo com essas preocupações de desempenho diversas. Para a maioria dos aplicativos, essa abordagem tem sido muito bem-sucedida.

## <a name="primitive-types"></a>Tipos primitivos

O .NET inclui um conjunto de tipos primitivos, que são usados (em graus variáveis) em todos os programas. Esses tipos contêm dados, como números, cadeias de caracteres, bytes e objetos arbitrários. A linguagem C# inclui palavras-chave para esses tipos. Um conjunto de amostra desses tipos é listado abaixo, com palavras-chave do C# correspondentes.

* <xref:System.Object?displayProperty=nameWithType> ([object](../csharp/language-reference/builtin-types/reference-types.md#the-object-type)) – a classe base ultimate no sistema de tipos CLR. É a raiz da hierarquia de tipos.
* <xref:System.Int16?displayProperty=nameWithType> ([short](../csharp/language-reference/builtin-types/integral-numeric-types.md)) – tipo inteiro com sinal de 16 bits. O <xref:System.UInt16> sem sinal também existe.
* <xref:System.Int32?displayProperty=nameWithType> ([int](../csharp/language-reference/builtin-types/integral-numeric-types.md)) – um tipo inteiro com sinal de 32 bits. O [UInt32](../csharp/language-reference/builtin-types/integral-numeric-types.md) sem sinal também existe.
* <xref:System.Single?displayProperty=nameWithType> ([float](../csharp/language-reference/builtin-types/floating-point-numeric-types.md)) – um tipo de ponto flutuante de 32 bits.
* <xref:System.Decimal?displayProperty=nameWithType> ([decimal](../csharp/language-reference/builtin-types/floating-point-numeric-types.md)) – um tipo decimal de 128 bits.
* <xref:System.Byte?displayProperty=nameWithType> ([byte](../csharp/language-reference/builtin-types/integral-numeric-types.md)) – um inteiro de 8 bits sem sinal que representa um byte de memória.
* <xref:System.Boolean?displayProperty=nameWithType> ([bool](../csharp/language-reference/builtin-types/bool.md))-um tipo booliano que representa `true` ou `false` .
* <xref:System.Char?displayProperty=nameWithType> ([char](../csharp/language-reference/builtin-types/char.md)) – um tipo numérico de 16 bits que representa um caractere Unicode.
* <xref:System.String?displayProperty=nameWithType> ([string](../csharp/language-reference/builtin-types/reference-types.md#the-string-type)) – representa uma série de caracteres. Diferente de um `char[]`, mas permite a indexação em cada `char` individual em `string`.

## <a name="data-structures"></a>estruturas de dados

O .NET inclui um conjunto de estruturas de dados que são fundamentais para quase todos os aplicativos .NET.  Elas são em sua maioria coleções, mas também incluem outros tipos.

* <xref:System.Array> -Representa uma matriz de objetos fortemente tipados que podem ser acessados pelo índice. Tem um tamanho fixo, de acordo com sua construção.
* <xref:System.Collections.Generic.List%601> – representa uma lista fortemente tipada de objetos que podem ser acessados por índice. É redimensionado automaticamente conforme necessário.
* <xref:System.Collections.Generic.Dictionary%602> – representa uma coleção de valores que são indexados por uma chave. Os valores podem ser acessados via chave. É redimensionado automaticamente conforme necessário.
* <xref:System.Uri> – fornece uma representação de objeto de um URI (Uniform Resource Identifier) e fácil acesso às partes do URI.
* <xref:System.DateTime> – representa um momento no tempo, geralmente expresso como uma data e hora do dia.

## <a name="utility-apis"></a>APIs utilitárias

O .NET inclui um conjunto de APIs utilitárias que fornecem funcionalidade para várias tarefas importantes.

* <xref:System.Net.Http.HttpClient> – uma API para enviar solicitações HTTP e receber respostas HTTP de um recurso identificado por um URI.
* <xref:System.Xml.Linq.XDocument> – uma API para carregar e consultar documentos XML com o LINQ.
* <xref:System.IO.StreamReader> – uma API para ler arquivos.
* <xref:System.IO.StreamWriter> – uma API para gravar arquivos.

## <a name="app-model-apis"></a>APIs do modelo de aplicativo

Há muitos modelos de aplicativo que podem ser usados com o .NET, fornecidos por várias empresas.

* [ASP.NET](https://www.asp.net) – fornece uma estrutura da Web para a criação de sites e serviços. Suporte para Windows, Linux e macOS (depende de versão do ASP.NET).
