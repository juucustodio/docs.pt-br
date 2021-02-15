---
description: 'Saiba mais sobre: <para> (Visual Basic)'
title: <para>
ms.date: 07/20/2015
helpviewer_keywords:
- <para> XML tag
- para XML tag
ms.assetid: a3a18b6c-6416-4358-94ec-37b22675fd37
ms.openlocfilehash: 51dd9ff300d980b4c0576566cad5d17375889ba1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99740763"
---
# <a name="para-visual-basic"></a>\<para> (Visual Basic)

Especifica que o conteúdo é formatado como um parágrafo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<para>content</para>  
```  
  
## <a name="parameters"></a>Parâmetros  

 `content`  
 O texto do parágrafo.  
  
## <a name="remarks"></a>Comentários  

 A `<para>` marca é para uso dentro de uma marca, como [\<summary>](summary.md) , [\<remarks>](remarks.md) ou [\<returns>](returns.md) , e permite que você adicione a estrutura ao texto.  
  
 Compile com [-Doc](../../reference/command-line-compiler/doc.md) para processar comentários de documentação em um arquivo.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a `<para>` marca para dividir a seção de comentários do `UpdateRecord` método em dois parágrafos.  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>Consulte também

- [Marcações de Comentário XML](index.md)
