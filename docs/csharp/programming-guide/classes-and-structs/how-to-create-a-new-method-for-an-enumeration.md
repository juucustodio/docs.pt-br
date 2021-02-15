---
title: Como criar um novo método para uma enumeração – guia de programação C#
description: Saiba como usar métodos de extensão para adicionar funcionalidade a uma enumeração em C#. Este exemplo mostra um método de extensão chamado passagem de uma enumeração chamada notas.
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [C#]
- extension methods [C#], for enums
- enum extensibility [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
ms.openlocfilehash: 88afff854b8136bde837db8effb0e0eb512e1099
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513087"
---
# <a name="how-to-create-a-new-method-for-an-enumeration-c-programming-guide"></a>Como criar um novo método para uma enumeração (guia de programação C#)

Você pode usar métodos de extensão para adicionar funcionalidades específica para um tipo de enumeração específico.  
  
## <a name="example"></a>Exemplo  

 No exemplo a seguir, a enumeração `Grades` representa as letras possíveis que um aluno pode receber em uma classe. Um método de extensão chamado `Passing` é adicionado ao tipo `Grades` de forma que cada instância desse tipo agora "sabe" se ele representa uma nota de aprovação ou não.  
  
 [!code-csharp[csProgGuideExtensionMethods#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#2)]  
  
 Observe que a classe `Extensions` também contém uma variável estática atualizada dinamicamente e que o valor retornado do método de extensão reflete o valor atual dessa variável. Isso demonstra que, nos bastidores, os métodos de extensão são chamados diretamente na classe estática na qual eles são definidos.  
  
## <a name="see-also"></a>Consulte também

- [Guia de programação C#](../index.md)
- [Métodos de Extensão](./extension-methods.md)
