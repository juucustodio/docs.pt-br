---
description: "Saiba mais sobre: BC42104: a variável ' <variablename> ' é usada antes de receber um valor"
title: A variável '<variablename>' é usada antes de receber um valor
ms.date: 07/20/2015
f1_keywords:
- vbc42104
- BC42104
helpviewer_keywords:
- BC42104
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
ms.openlocfilehash: 501c3e3971c5ca0ebdba6981134f5029b77d0075
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99701489"
---
# <a name="bc42104-variable-variablename-is-used-before-it-has-been-assigned-a-value"></a>BC42104: a variável ' \<variablename> ' é usada antes de receber um valor

A variável ' \<variablename> ' é usada antes de receber um valor. Uma exceção de referência nula pode resultar em tempo de execução.

 Um aplicativo tem pelo menos um caminho possível por meio de seu código que lê uma variável antes que qualquer valor seja atribuído a ela.

 Se uma variável nunca tiver sido atribuído um valor, ela manterá o valor padrão para seu tipo de dados. Para um tipo de dados de referência, esse valor padrão é [Nothing](../nothing.md). A leitura de uma variável de referência que tem um valor de `Nothing` pode causar um <xref:System.NullReferenceException> em algumas circunstâncias.

 Por padrão, esta mensagem é um aviso. Para obter mais informações sobre como ocultar avisos ou tratar avisos como erros, consulte [Configurando avisos no Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).

 **ID do erro:** BC42104

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Verifique sua lógica de fluxo de controle e certifique-se de que a variável tem um valor válido antes que o controle passe para qualquer instrução que a Leia.

- Uma maneira de garantir que a variável sempre tenha um valor válido é inicializá-la como parte de sua declaração. Consulte "inicialização" na [instrução Dim](../statements/dim-statement.md).

## <a name="see-also"></a>Consulte também

- [Instrução Dim](../statements/dim-statement.md)
- [Declaração de Variável](../../programming-guide/language-features/variables/variable-declaration.md)
- [Solução de problemas de Variáveis](../../programming-guide/language-features/variables/troubleshooting-variables.md)
