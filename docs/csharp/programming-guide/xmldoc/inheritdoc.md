---
description: 'Saiba mais sobre: <inheritdoc> (guia de programação C#)'
title: <inheritdoc> – Guia de Programação em C#
ms.date: 01/21/2020
f1_keywords:
- inheritdoc
- <inheritdoc>
helpviewer_keywords:
- <inheritdoc> C# XML tag
- inheritdoc C# XML tag
ms.assetid: 46d329b1-5b84-4537-9e17-73ca97313e4e
ms.openlocfilehash: 960bdfbcec1e3f6a89675273f63b6d398e44947e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99719390"
---
# <a name="inheritdoc-c-programming-guide"></a>\<inheritdoc> (Guia de programação C#)

## <a name="syntax"></a>Syntax  
  
```xml  
<inheritdoc/>
```  

## <a name="inheritdoc"></a>InheritDoc

Herde comentários XML de classes base, interfaces e métodos semelhantes. Isso elimina a cópia indesejada e a colagem de comentários XML duplicados e mantém automaticamente os comentários XML sincronizados.
  
## <a name="remarks"></a>Comentários  

Adicione seus comentários XML em classes ou interfaces base e deixe que InheritDoc Copie os comentários para a implementação de classes.

Adicione seus comentários XML aos seus métodos síncronos e deixe que InheritDoc Copie os comentários para suas versões assíncronas dos mesmos métodos.  

Se você quiser copiar os comentários de um membro específico, poderá usar o `cref` atributo para especificar o membro.
  
## <a name="examples"></a>Exemplos

[!code-csharp[csProgGuideDocComments#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#16)]  

[!code-csharp[csProgGuideDocComments#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#17)]  

## <a name="see-also"></a>Confira também

- [Guia de programação C#](../index.md)
- [Marcas recomendadas para comentários de documentação](./recommended-tags-for-documentation-comments.md)
