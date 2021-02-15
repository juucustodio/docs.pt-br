---
description: "Saiba mais sobre: BC42319: a exceção de comentário XML deve ter um atributo ' cref '"
title: A exceção de comentário XML deve ter um atributo 'cref'
ms.date: 07/20/2015
f1_keywords:
- bc42319
- vbc42319
helpviewer_keywords:
- BC42319
ms.assetid: 62eeeba3-6811-48be-b1ef-c2e4feda3177
ms.openlocfilehash: e602a2973d95f70d5ab532e6be319a9575d239a7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99701450"
---
# <a name="bc42319-xml-comment-exception-must-have-a-cref-attribute"></a>BC42319: a exceção de comentário XML deve ter um atributo ' cref '

A \<exception> marca fornece uma maneira de documentar as exceções que podem ser geradas por um método. O `cref` Atributo Required designa o nome de um membro, que é verificado pelo gerador de documentação. Se o membro existir, ele será convertido para o nome do elemento canônico no arquivo de documentação.

**ID do erro:** BC42319

## <a name="to-correct-this-error"></a>Para corrigir este erro

Adicione o `cref` atributo à exceção da seguinte maneira:

```xml
<exception cref="member">description</exception>
```

## <a name="see-also"></a>Consulte também

- [\<exception>](../xmldoc/exception.md)
- [Como criar documentação XML](../../programming-guide/program-structure/how-to-create-xml-documentation.md)
- [Marcações de Comentário XML](../xmldoc/index.md)
