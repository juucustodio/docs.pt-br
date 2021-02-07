---
description: 'Saiba mais sobre: BC40041: o tipo <typename> não é compatível com CLS'
title: O tipo <typename> não é compatível com CLS
ms.date: 07/20/2015
f1_keywords:
- bc40041
- vbc40041
helpviewer_keywords:
- BC40041
ms.assetid: 634132c2-5646-44aa-98c6-f773e2e63882
ms.openlocfilehash: a1e807dba64f2fce70b0fb39147087d91ca80fbc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675033"
---
# <a name="bc40041-type-typename-is-not-cls-compliant"></a>BC40041: tipo \<typename> não tem conformidade com CLS

Uma variável, propriedade ou retorno de função é declarada com um tipo de dados que não tem conformidade com CLS.

 Para que um aplicativo seja compatível com a [independência de idioma e](../../../standard/language-independence-and-language-independent-components.md) com os componentes de Language-Independent (CLS), ele deve usar somente tipos em conformidade com CLS.

 Os tipos de dados a seguir Visual Basic não são compatíveis com CLS:

- [Tipo de Dados SByte](../data-types/sbyte-data-type.md)

- [Tipo de Dados UInteger](../data-types/uinteger-data-type.md)

- [Tipo de Dados ULong](../data-types/ulong-data-type.md)

- [Tipo de Dados UShort](../data-types/ushort-data-type.md)

 **ID do erro:** BC40041

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Se seu aplicativo precisar ser compatível com CLS, altere o tipo de dados desse elemento para o tipo mais próximo em conformidade com CLS. Por exemplo, no lugar de `UInteger` você pode ser capaz de usar `Integer` se não precisar do intervalo de valores acima de 2.147.483.647. Se você precisar do intervalo estendido, poderá substituir `UInteger` por `Long` .

- Se seu aplicativo não precisar ser compatível com CLS, você não precisará alterar nada. No entanto, você deve estar ciente de sua não conformidade.
