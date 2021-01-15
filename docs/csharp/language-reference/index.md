---
description: Referência de C#
title: Referência de C#
ms.date: 01/13/2021
ms.custom: updateeachrelease
f1_keywords:
- _CSharpKeyword
helpviewer_keywords:
- Visual C#, language reference
- language reference [C#]
- Programmer's Reference for C#
- C# language, reference
- reference, C# language
ms.assetid: 06de3167-c16c-4e1a-b3c5-c27841d4569a
ms.openlocfilehash: 663d08921b1fb6c5013ce8dddb044ba12ead8409
ms.sourcegitcommit: 4f5f1855849cb02c3b610c7006ac21d7429f3348
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235229"
---
# <a name="c-reference"></a>Referência de C#

Esta seção fornece o material de referência sobre palavras-chave do C#, operadores, caracteres especiais, diretivas de pré-processador, opções de compilador e erros de compilador e avisos.  
  
## <a name="in-this-section"></a>Nesta seção

 [Palavras-chave do C#](./keywords/index.md)  
 Fornece links para informações sobre a sintaxe e as palavras-chave do C#.  
  
 [Operadores do C#](./operators/index.md)  
 Fornece links para informações sobre a sintaxe e os operadores do C#.  

 [Caracteres especiais do C#](./tokens/index.md)  
 Fornece links para informações sobre caracteres especiais contextuais em C# e seu uso.  

 [Diretivas de pré-processador do C#](./preprocessor-directives/index.md)  
 Fornece links para informações sobre os comandos do compilador para inserir no código-fonte do C#.  
  
 [Opções do compilador de C#](./compiler-options/index.md)  
 Inclui informações sobre as opções do compilador e como usá-las.  
  
 [Erros do compilador C#](./compiler-messages/index.md)  
 Inclui snippets de código que demonstram a causa e a correção de erros do compilador do C# e avisos.  
  
 [Especificação da linguagem C#](../../../_csharplang/spec/introduction.md)  
 Especificação de linguagem do C# 6.0. Este é um projeto de proposta da linguagem C# 6.0. Este documento será refinado por meio do trabalho com o Comitê de padrões ECMA C#. A versão 5.0 foi lançada em dezembro de 2017 como o documento [Padrão ECMA-334 – 5ª Edição](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-334.pdf).

Os recursos que foram implementados nas versões do C# depois da 6.0 são representados em propostas de especificação de linguagem. Esses documentos descrevem os deltas para a especificação da linguagem a fim de adicionar os novos recursos. Eles estão no formulário de proposta de rascunho. Essas especificações serão refinadas e enviadas para o Comitê de padrões ECMA para revisão formal e Incorporation em uma versão futura do C# Standard.

 [Propostas de especificação do C# 7,0](../../../_csharplang/proposals/csharp-7.0/pattern-matching.md)  
 Implementamos diversos recursos novos no C# 7.0. Entre eles estão correspondência de padrões, funções locais, declarações de variável out, expressões throw, literais binários e separadores de dígito. Esta pasta contém as especificações de cada um desses recursos.
  
 [Propostas de especificação do C# 7,1](../../../_csharplang/proposals/csharp-7.1/async-main.md)  
 Há novos recursos adicionados no C# 7.1. Primeiramente, você pode gravar um método `Main` que retorna `Task` ou `Task<int>`. Isso permite que você adicione o modificador `async` ao `Main`. A expressão `default` pode ser usada sem um tipo em locais onde o tipo pode ser inferido. Além disso, os nomes dos membros de tupla podem ser inferidos. Por fim, a correspondência de padrões pode ser usada com genéricos.

 [Propostas de especificação do C# 7,2](../../../_csharplang/proposals/csharp-7.2/readonly-ref.md)  
 O C# 7.2 adicionou a uma série de recursos pequenos. Você pode passar argumentos por referência de somente leitura usando a palavra-chave `in`. Há uma série de alterações de nível inferior para dar suporte à segurança de tempo de compilação para `Span` e tipos relacionados. Você pode usar argumentos nomeados nos quais os argumentos posteriores são posicionais, em algumas situações. O modificador de acesso `private protected` permite que você especifique que os chamadores são limitados aos tipos derivados, implementados no mesmo assembly. O operador `?:` pode resolver em uma referência a uma variável. Você também pode formatar números hexadecimais e binários usando um separador de dígito à esquerda.

 [Propostas de especificação do C# 7,3](../../../_csharplang/proposals/csharp-7.3/blittable.md)  
 C# 7.3 é outra versão de ponto que inclui várias atualizações pequenas. Você pode usar novas restrições em parâmetros de tipo genérico. Outras alterações facilitam o trabalho com `fixed` campos, incluindo o uso de [`stackalloc`](./operators/stackalloc.md) alocações. Variáveis locais declaradas com a `ref` palavra-chave podem ser reatribuídas para se referirem ao novo armazenamento. Você pode colocar os atributos em propriedades autoimplementadas que direcionam o campo de suporte gerado pelo compilador. As variáveis de expressão podem ser usadas em inicializadores. As tuplas podem ser comparadas quanto à igualdade (ou desigualdade). Também houve algumas melhorias para a resolução de sobrecarga.
  
 [Propostas de especificação do C# 8,0](../../../_csharplang/proposals/csharp-8.0/nullable-reference-types.md)  
 O C# 8,0 está disponível com o .NET Core 3,0. Os recursos incluem tipos de referência anuláveis, correspondência de padrões recursivos, métodos de interface padrão, fluxos assíncronos, intervalos e índices, com base em padrões usando e usando declarações, atribuição de União nula e membros de instância ReadOnly.

 [Propostas de especificação do C# 9,0](../../../_csharplang/proposals/csharp-9.0/records.md)  
 O C# 9,0 está disponível com o .NET 5,0. Os recursos incluem registros, instruções de nível superior, aprimoramentos de correspondência de padrões, init somente setters, novas expressões com tipo de destino, inicializadores de módulo, extensão de métodos parciais, funções anônimas estáticas, expressões condicionais de tipo de destino, tipos de retorno covariantes, extensão getenumerador em loops foreach, parâmetros de descarte de lambda, atributos em funções locais, inteiros de tamanho nativo, ponteiros de função, supressão de emissão de sinalizador localsinit

## <a name="related-sections"></a>Seções relacionadas  

 [Usando o ambiente de desenvolvimento do Visual Studio para C#](/visualstudio/get-started/csharp)  
 Fornece links para tópicos conceituais e de tarefas que descrevem o IDE e o Editor.  
  
 [Guia de programação C#](../programming-guide/index.md)  
 Inclui informações sobre como usar a linguagem de programação do C#.
