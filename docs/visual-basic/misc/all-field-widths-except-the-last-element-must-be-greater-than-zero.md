---
description: 'Saiba mais sobre: todas as larguras de campo, exceto o último elemento, devem ser maiores que zero'
title: Todas as larguras de campo, exceto do último elemento, devem ser maiores que zero
ms.date: 07/20/2015
f1_keywords:
- vbrTextFieldParser_FieldWidthsMustPositive
ms.assetid: 41d8c661-a749-4c89-be56-905c6e7c3c9d
ms.openlocfilehash: cf2edb21f017031c7dd333893d554353eceebe73
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787377"
---
# <a name="all-field-widths-except-the-last-element-must-be-greater-than-zero"></a>Todas as larguras de campo, exceto do último elemento, devem ser maiores que zero

Todas as larguras de campo, exceto o último elemento, devem ser maiores que zero. Uma largura de campo menor ou igual a zero no último elemento indica que o último campo é de comprimento variável.  
  
 A operação falhou porque uma largura de campo diferente do último elemento está definida como zero ou menos. Uma largura de campo menor ou igual a zero pode ser usada como o último elemento para indicar que o último campo é de comprimento variável, mas não pode ser usado como qualquer outro elemento.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Defina a largura do campo para o comprimento correto.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.SetFieldWidths%2A?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.FieldWidths>
- [Como: ler de arquivos de texto de largura fixa](../developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)
- [Objeto TextFieldParser](../language-reference/objects/textfieldparser-object.md)
