---
description: 'Saiba mais sobre: <code>(Visual Basic)'
title: <code>
ms.date: 07/20/2015
helpviewer_keywords:
- code XML tag
- <code> XML tag
ms.assetid: 925e5342-be05-45f2-bf66-7398bbd6710e
ms.openlocfilehash: 80fc0988f60d9d82b9c88734f86b20ebccc80b7c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787494"
---
# <a name="code-visual-basic"></a>\<code> (Visual Basic)

Indica que o texto tem várias linhas de código.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<code>content</code>  
```  
  
## <a name="parameters"></a>Parâmetros  

 `content`  
 O texto a ser marcado como código.  
  
## <a name="remarks"></a>Comentários  

 Use a `<code>` marca para indicar várias linhas como código. Use [\<c>](c.md) para indicar que o texto dentro de uma descrição deve ser marcado como código.  
  
 Compile com [-Doc](../../reference/command-line-compiler/doc.md) para processar comentários de documentação em um arquivo.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a \<code> marca para incluir o código de exemplo para usar o `ID` campo.  
  
 [!code-vb[VbVbcnXmlDocComments#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [Marcações de Comentário XML](index.md)
