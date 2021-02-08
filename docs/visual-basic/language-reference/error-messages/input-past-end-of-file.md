---
description: 'Saiba mais sobre: entrada após o final do arquivo'
title: Entrada passou do final do arquivo
ms.date: 07/20/2015
f1_keywords:
- vbrID62
ms.assetid: 65292704-6e7d-4622-9f50-eb655a59b016
ms.openlocfilehash: b65a57bdc56367518a93880be28781e56c9b99cc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796035"
---
# <a name="input-past-end-of-file"></a>Entrada passou do final do arquivo

Uma `Input` instrução está lendo um arquivo vazio ou um em que todos os dados são usados, ou você usou a `EOF` função com um arquivo aberto para acesso binário.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Use a `EOF` função imediatamente antes da `Input` instrução para detectar o final do arquivo.  
  
2. Se o arquivo for aberto para acesso binário, use `Seek` e `Loc` .  
  
## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.FileSystem.Input%2A>
- <xref:Microsoft.VisualBasic.FileSystem.EOF%2A>
- <xref:Microsoft.VisualBasic.FileSystem.Seek%2A>
- <xref:Microsoft.VisualBasic.FileSystem.Loc%2A>
