---
description: 'Saiba mais sobre: erro ao carregar DLL (Visual Basic)'
title: Erro ao carregar DLL
ms.date: 07/20/2015
f1_keywords:
- vbrID48
ms.assetid: 4226cd1f-028c-477d-88a5-cb57f7e0cdc8
ms.openlocfilehash: 098d05e93d328f3667000bd81290f4b77cf7949e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796503"
---
# <a name="error-in-loading-dll-visual-basic"></a>Erro no carregamento da DLL (Visual Basic)

Uma DLL (biblioteca de vínculo dinâmico) é uma biblioteca especificada na `Lib` cláusula de uma `Declare` instrução. Possíveis causas desse erro incluem:  
  
- O arquivo não é executável de DLL.  
  
- O arquivo não é uma DLL do Microsoft Windows.  
  
- A DLL faz referência a outra DLL que não está presente.  
  
- A DLL ou a DLL referenciada não está em um diretório especificado no caminho.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Se o arquivo for um arquivo de texto de origem e, portanto, não executável de DLL, ele deverá ser compilado e vinculado a um formulário executável DLL.  
  
- Se o arquivo não for uma DLL do Microsoft Windows, obtenha o equivalente do Microsoft Windows.  
  
- Se a DLL fizer referência a outra DLL que não está presente, obtenha a DLL referenciada e torne-a disponível.  
  
- Se a dll ou a DLL referenciada não estiver em um diretório especificado pelo caminho, mova a DLL para um diretório referenciado.  
  
## <a name="see-also"></a>Consulte também

- [Instrução Declare](../statements/declare-statement.md)
