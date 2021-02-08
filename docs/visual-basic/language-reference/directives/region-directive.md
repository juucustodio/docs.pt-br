---
description: 'Saiba mais sobre a diretiva: #Region'
title: '#Diretiva Region'
ms.date: 07/20/2015
f1_keywords:
- vb.Region
- vb.#Region
helpviewer_keywords:
- Visual Basic compiler, compiler directives
- '#region directive'
- region directive (#region)
- '#Region keyword [Visual Basic]'
ms.assetid: 90a6a104-3cbf-47d0-bdc4-b585d0921b87
ms.openlocfilehash: 4ba1645cfc51a69d39e6a60b5ea236dd65883e1c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797218"
---
# <a name="region-directive"></a>Diretiva #Region

Recolhe e oculta seções de código em Visual Basic arquivos.  
  
## <a name="syntax"></a>Syntax  

```vb
#Region "identifier_string"  
#End Region  
```  
  
## <a name="parts"></a>Partes  
  
|Termo|Definição|  
|---|---|  
|`identifier_string`|Obrigatório. Cadeia de caracteres que atua como o título de uma região quando ela é recolhida. As regiões são recolhidas por padrão.|  
|`#End Region`|Encerra o `#Region` bloco.|  
  
## <a name="remarks"></a>Comentários  

 Use a `#Region` diretiva para especificar um bloco de código para expandir ou recolher ao usar o recurso de estrutura de tópicos do editor de Visual Studio Code. Você pode posicionar ou *aninhar* regiões em outras regiões para agrupar regiões semelhantes.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a `#Region` diretiva.  
  
 [!code-vb[VbVbalrConditionalComp#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#4)]  
  
## <a name="see-also"></a>Consulte também

- [#If... Diretivas then... #Else](if-then-else-directives.md)
- [Estrutura de tópicos](/visualstudio/ide/outlining)
- [Como: Recolher e ocultar seções do código](../../programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)
