---
description: 'Saiba mais sobre: BC40033: não é permitido não compatível com CLS <membername> em uma interface em conformidade com CLS'
title: <membername> não compatível com CLS não é permitido em uma interface compatível com CLS
ms.date: 07/20/2015
f1_keywords:
- bc40033
- vbc40033
helpviewer_keywords:
- BC40033
ms.assetid: 060c4b08-798e-40f1-94cf-c05c524f1b8a
ms.openlocfilehash: 070b56a8bf9df930de5bb5e363a9b157fcdc7ad7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795632"
---
# <a name="bc40033-non-cls-compliant-membername-is-not-allowed-in-a-cls-compliant-interface"></a>BC40033: \<membername> não é permitido compatível com CLS em uma interface em conformidade com CLS

Uma propriedade, um procedimento ou um evento em uma interface é marcado como `<CLSCompliant(True)>` quando a própria interface está marcada como `<CLSCompliant(False)>` ou não está marcada.

 Para que uma interface seja compatível com a [independência de idioma e os componentes de Language-Independent](../../../standard/language-independence-and-language-independent-components.md) (CLS), todos os seus membros devem estar em conformidade.

 Quando você aplica o a <xref:System.CLSCompliantAttribute> um elemento de programação, você define o parâmetro do atributo `isCompliant` como `True` ou `False` para indicar conformidade ou não conformidade. Não há nenhum padrão para esse parâmetro, e você deve fornecer um valor.

 Se você não aplicar o <xref:System.CLSCompliantAttribute> a um elemento, será considerado como não compatível.

 Por padrão, esta mensagem é um aviso. Para obter informações sobre como ocultar avisos ou tratar avisos como erros, consulte [Configurando avisos no Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).

 **ID do erro:** BC40033

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Se você precisar de conformidade com CLS e tiver controle sobre o código-fonte da interface, marque a interface como `<CLSCompliant(True)>` se todos os seus membros estiverem em conformidade.

- Se você precisar de conformidade com CLS e não tiver controle sobre o código-fonte da interface, ou se ele não estiver qualificado para ser compatível, defina esse membro em uma interface diferente.

- Se você precisar que esse membro permaneça em sua interface atual, remova o <xref:System.CLSCompliantAttribute> de sua definição ou marque-o como `<CLSCompliant(False)>` .

## <a name="see-also"></a>Consulte também

- [Instrução Interface](../statements/interface-statement.md)
