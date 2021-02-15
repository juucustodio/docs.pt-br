---
description: 'Saiba mais sobre: sub ou função não definida (Visual Basic)'
title: Sub ou Function não definida
ms.date: 07/20/2015
f1_keywords:
- vbrID35
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
ms.openlocfilehash: 5726e8b23283b419577c468eee2344b234493425
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641376"
---
# <a name="sub-or-function-not-defined-visual-basic"></a>Sub ou função não definida (Visual Basic)

Um `Sub` ou `Function` deve ser definido para ser chamado. Possíveis causas do erro incluem:  
  
- Digitação incorreta do nome do procedimento.  
  
- Tentativa de chamar um procedimento de outro projeto sem adicionar explicitamente uma referência a esse projeto na caixa de diálogo **referências** .  
  
- Especificar um procedimento que não seja visível para o procedimento de chamada.  
  
- Declarando uma rotina DLL (biblioteca de vínculo dinâmico) do Windows ou uma rotina de recurso de código do Macintosh que não está na biblioteca ou no recurso de código especificado.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Verifique se o nome do procedimento está escrito corretamente.  
  
2. Localize o nome do projeto que contém o procedimento que você deseja chamar na caixa de diálogo **referências** . Se não aparecer, clique no botão **procurar** para procurá-lo. Marque a caixa de seleção à esquerda do nome do projeto e clique em **OK**.  
  
3. Verifique o nome da rotina.  
  
## <a name="see-also"></a>Consulte também

- [Tipos de erro](../../programming-guide/language-features/error-types.md)
- [Gerenciando referências em um projeto](/visualstudio/ide/managing-references-in-a-project)
- [Instrução Sub](../statements/sub-statement.md)
- [Instrução Function](../statements/function-statement.md)
