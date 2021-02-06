---
description: 'Saiba mais sobre: <remarks> (Visual Basic)'
title: <remarks>
ms.date: 07/20/2015
helpviewer_keywords:
- <remarks> XML tag
- remarks XML tag
ms.assetid: c6241773-a7ed-41c9-9a8b-9722a0c606a9
ms.openlocfilehash: 4b0584abbe85a7ecc73e25dd1f6ec321962b88a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99640401"
---
# <a name="remarks-visual-basic"></a>\<remarks> (Visual Basic)

Especifica uma seção de comentários para o membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<remarks>description</remarks>  
```  
  
## <a name="parameters"></a>Parâmetros  

 `description`  
 Uma descrição do membro.  
  
## <a name="remarks"></a>Comentários  

 Use a `<remarks>` marca para adicionar informações sobre um tipo, complementando as informações especificadas com [\<summary>](summary.md) .  
  
 Essas informações são exibidas no Pesquisador de objetos. Para obter informações sobre o pesquisador de objetos, consulte [exibindo a estrutura do código](/visualstudio/ide/viewing-the-structure-of-code).  
  
 Compile com [-Doc](../../reference/command-line-compiler/doc.md) para processar comentários de documentação em um arquivo.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a `<remarks>` marca para explicar o que o `UpdateRecord` método faz.  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>Consulte também

- [Marcações de Comentário XML](index.md)
