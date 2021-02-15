---
title: Manipulações básicas de cadeia de caracteres no .NET
description: Veja um exemplo que chama vários métodos de cadeia de caracteres.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET], examples
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
ms.openlocfilehash: e3e969520e068bde234c13d45ad790b76ecf8fdb
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94825150"
---
# <a name="how-to-perform-basic-string-manipulations-in-net"></a>Como: executar manipulações de cadeias de caracteres básicas no .NET

O exemplo a seguir usa alguns dos métodos discutidos nos tópicos de [Operações de cadeias de caracteres básicas](basic-string-operations.md) para construir uma classe que realiza manipulações de cadeia de caracteres de uma maneira que pode ser encontrada em um aplicativo real. A classe `MailToData` armazena o nome e endereço de um indivíduo em propriedades separadas e fornece uma maneira de combinar os campos `City`, `State` e `Zip` em uma única cadeia de caracteres para exibição para o usuário. Além disso, a classe permite que o usuário insira a cidade, o estado e as informações de CEP como uma única cadeia de caracteres. O aplicativo analisa automaticamente a única cadeia de caracteres e insere as informações apropriadas na propriedade correspondente.

Para simplificar, este exemplo usa um aplicativo de console com uma interface de linha de comando.

## <a name="example"></a>Exemplo

[!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
[!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]

Quando o código anterior é executado, o usuário é solicitado a inserir seu nome e endereço. O aplicativo coloca as informações nas propriedades apropriadas e exibe as informações de volta para o usuário, criando uma única cadeia de caracteres que exibe a cidade, o estado e as informações de CEP.

## <a name="see-also"></a>Confira também

- [Operações básicas de cadeia de caracteres](basic-string-operations.md)
