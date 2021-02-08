---
description: 'Saiba mais sobre: um nome inválido foi especificado para o log de eventos'
title: Um nome inválido foi especificado para o log de evento
ms.date: 07/20/2015
ms.assetid: b1b158bd-f13f-4371-a8af-31c0e86ae6be
ms.openlocfilehash: 4786483fe0b1ae32a16b67bfb4f406587719011b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787364"
---
# <a name="an-invalid-name-was-specified-for-the-event-log"></a>Um nome inválido foi especificado para o log de evento

Um nome inválido foi especificado para o log de eventos. Normalmente, isso é resultado de caracteres inválidos no nome, um nome de arquivo em branco ou um nome de arquivo muito longo.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Se o nome especificado tiver mais de oito caracteres, verifique se não há conflito com os nomes de outros logs de eventos. Somente os oito primeiros caracteres são avaliados ao determinar se o nome é exclusivo.  
  
- Se fornecer um caminho, verifique se ele foi analisado corretamente.  
  
- Verifique se não há caracteres inválidos no nome. Os caracteres que não podem ser usados em um nome de arquivo incluem `<` , `>` ,,,, `:` `"` `/` `\` e `|` .  
  
## <a name="see-also"></a>Consulte também

- [Como: analisar caminhos de arquivo](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
- [Como: renomear um arquivo](../developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)
