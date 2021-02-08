---
description: 'Saiba mais sobre: BC40035: <proceduresignature1> não tem conformidade com CLS porque sobrecarrega o <proceduresignature2> que difere dele somente por matriz de tipos de parâmetro de matriz ou pela classificação dos tipos de parâmetro de matriz'
title: <proceduresignature1> não está em conformidade com CLS porque sobrecarrega <proceduresignature2> que difere dele somente pelos tipos de matriz e parâmetro de matriz ou pela classificação dos tipos de parâmetro da matriz
ms.date: 07/20/2015
f1_keywords:
- vbc40035
- bc40035
helpviewer_keywords:
- BC40035
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
ms.openlocfilehash: 056683033a4eacdc6ad783f5056b639e849e3507
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795385"
---
# <a name="bc40035-proceduresignature1-is-not-cls-compliant-because-it-overloads-proceduresignature2-which-differs-from-it-only-by-array-of-array-parameter-types-or-by-the-rank-of-the-array-parameter-types"></a>BC40035: \<proceduresignature1> não tem conformidade com CLS porque sobrecarrega o \<proceduresignature2> que difere dele somente por matriz de tipos de parâmetro de matriz ou pela classificação dos tipos de parâmetro de matriz

Um procedimento ou propriedade é marcado como `<CLSCompliant(True)>` quando ele substitui outro procedimento ou propriedade e a única diferença entre suas listas de parâmetros é o nível de aninhamento de uma matriz denteada ou a classificação de uma matriz.

 Nas declarações a seguir, a segunda e terceira declarações geram esse erro:

 `Overloads Sub ProcessArray(arrayParam() As Integer)`

 `Overloads Sub ProcessArray(arrayParam()() As Integer)`

 `Overloads Sub ProcessArray(arrayParam(,) As Integer)`

 A segunda declaração altera o parâmetro unidimensional original `arrayParam` para uma matriz de matrizes. A terceira declaração muda `arrayParam` para uma matriz bidimensional (Rank 2). Embora Visual Basic permita sobrecargas para diferir apenas por uma dessas alterações, tal sobrecarga não é compatível com a independência de [linguagem e os componentes de Language-Independent](../../../standard/language-independence-and-language-independent-components.md) (CLS).

 Quando você aplica o a <xref:System.CLSCompliantAttribute> um elemento de programação, você define o parâmetro do atributo `isCompliant` como `True` ou `False` para indicar conformidade ou não conformidade. Não há nenhum padrão para esse parâmetro, e você deve fornecer um valor.

 Se você não aplicar o <xref:System.CLSCompliantAttribute> a um elemento, será considerado como não compatível.

 Por padrão, esta mensagem é um aviso. Para obter informações sobre como ocultar avisos ou tratar avisos como erros, consulte [Configurando avisos no Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).

 **ID do erro:** BC40035

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Se você precisar de conformidade com CLS, defina suas sobrecargas para diferir umas das outras em mais formas do que apenas as alterações citadas nesta página de ajuda.
- Se você precisar que as sobrecargas diferem apenas pelas alterações citadas nesta página de ajuda, remova o <xref:System.CLSCompliantAttribute> de suas definições ou marque-os como `<CLSCompliant(False)>` .

## <a name="see-also"></a>Consulte também

- [Sobrecarga de procedimento](../../programming-guide/language-features/procedures/procedure-overloading.md)
- [Sobrecargas](../modifiers/overloads.md)
