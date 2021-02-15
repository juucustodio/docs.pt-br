---
description: 'Saiba mais sobre: como Pesquisar dentro de uma cadeia de caracteres (Visual Basic)'
title: 'Como: Pesquisar dentro de uma cadeia de caracteres'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], finding
- strings [Visual Basic], searching
- examples [Visual Basic], strings
ms.assetid: ae4c79e0-08ea-489f-bdb2-5eb6d355f284
ms.openlocfilehash: dab9faf91eef2e6d845805693227e1a6735ec796
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429721"
---
# <a name="how-to-search-within-a-string-visual-basic"></a>Como: Pesquisar dentro de uma cadeia de caracteres (Visual Basic)

Este artigo mostra um exemplo de como Pesquisar dentro de uma cadeia de caracteres em Visual Basic.

## <a name="example"></a>Exemplo

Este exemplo chama o <xref:System.String.IndexOf%2A> método em um <xref:System.String> objeto para relatar o índice da primeira ocorrência de uma subcadeia de caracteres:

 [!code-vb[VbVbalrStrings#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#71)]

## <a name="robust-programming"></a>Programação robusta

O <xref:System.String.IndexOf%2A> método retorna o local do primeiro caractere da primeira ocorrência da subcadeia de caracteres. O índice é baseado em 0, o que significa que o primeiro caractere de uma cadeia de caracteres tem um índice de 0.

Se não <xref:System.String.IndexOf%2A> encontrar a subcadeia de caracteres, retornará-1.

O <xref:System.String.IndexOf%2A> método diferencia maiúsculas de minúsculas e usa a cultura atual.

Para obter um controle de erro ideal, talvez você queira colocar a pesquisa de cadeia de caracteres no `Try` bloco de uma [tentativa... Capturar... Instrução Finally](../../../language-reference/statements/try-catch-finally-statement.md) .

## <a name="see-also"></a>Consulte também

- <xref:System.String.IndexOf%2A>
- [Instrução Try...Catch...Finally](../../../language-reference/statements/try-catch-finally-statement.md)
- [Introdução a cadeias de caracteres no Visual Basic](introduction-to-strings.md)
- [Cadeias de caracteres](index.md)
