---
title: Estendendo metadados por meio de atributos
description: Saiba como estender metadados usando atributos no .NET. Os atributos são declarações descritivas semelhantes a palavras-chave para anotar elementos de programação, como tipos e campos.
ms.date: 10/14/2020
helpviewer_keywords:
- metadata, extending
- attributes [.NET], metadata
- elements [.NET], attributes
- common language runtime, attributes
- annotating programming elements
- keyword-like descriptive declarations
- runtime, attributes
- extending metadata
ms.assetid: 30386922-1e00-4602-9ebf-526b271a8b87
ms.openlocfilehash: e41299b83ae451117ab6829eee928b0d2306be19
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829070"
---
# <a name="extend-metadata-using-attributes"></a>Estender metadados usando atributos

O Common Language Runtime permite adicionar declarações descritivas parecidas com palavras, chamadas atributos, para anotar elementos de programação como tipos, campos, métodos e propriedades. Quando você compila seu código para o runtime, ele é convertido em MSIL (Microsoft Intermediate Language) e colocado dentro de um arquivo PE (executável portátil) com metadados gerados pelo compilador. Os atributos permitem colocar informações descritivas extras em metadados que podem ser extraídos usando serviços de reflexão de runtime. O compilador cria atributos quando você declara instâncias de classes especiais que derivam de <xref:System.Attribute?displayProperty=nameWithType>.

O .NET usa atributos por vários motivos e para resolver vários problemas. Os atributos descrevem como serializar dados, especificar características que são usadas para impor segurança e limitar otimizações pelo compilador JIT (Just-In-Time) para que o código permaneça fácil de depurar. Os atributos também podem registrar o nome de um arquivo ou o autor do código, ou controlar a visibilidade de controles e membros durante o desenvolvimento de formulários.

## <a name="related-articles"></a>Artigos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Aplicando atributos](applying-attributes.md)|Descreve como aplicar um atributo a um elemento do código.|
|[Escrevendo atributos personalizados](writing-custom-attributes.md)|Descreve como criar classes de atributos personalizados.|
|[Recuperando informações armazenadas em atributos](retrieving-information-stored-in-attributes.md)|Descreve como recuperar atributos personalizados para o código que é carregado no contexto de execução.|
|[Metadados e componentes autodescritivos](../metadata-and-self-describing-components.md)|Fornece uma visão geral dos metadados e descreve como ele é implementado em um arquivo PE (executável portátil do .NET).|
|[Como carregar assemblies no contexto de somente reflexão](../../framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|Explica como recuperar informações de atributos personalizados no contexto somente reflexão.|

## <a name="reference"></a>Referência

- <xref:System.Attribute?displayProperty=nameWithType>
