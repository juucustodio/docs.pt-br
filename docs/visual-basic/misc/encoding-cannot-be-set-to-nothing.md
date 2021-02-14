---
description: 'Saiba mais sobre: a codificação não pode ser definida como Nothing'
title: A codificação não pode ser definida como Nothing
ms.date: 07/20/2015
ms.assetid: 59f7c731-8291-4a85-bf51-c225e48cdc84
ms.openlocfilehash: 4fa9cbd9488501b5295da8d8ace41ef06a706c12
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100462989"
---
# <a name="encoding-cannot-be-set-to-nothing"></a>A codificação não pode ser definida como Nothing

Falha na tentativa de ler ou gravar em um arquivo porque o parâmetro foi `encoding` definido como `Nothing` , mas requer um valor válido.  
  
 <xref:System.Text.Encoding> é usado para determinar qual codificação usar ao gravar em um arquivo. O padrão é UTF-8.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Forneça um valor válido para o `encoding` parâmetro.  
  
## <a name="see-also"></a>Consulte também

- [Codificações de arquivo](../developing-apps/programming/drives-directories-files/file-encodings.md)
- [Ler arquivos](../developing-apps/programming/drives-directories-files/reading-from-files.md)
- [Gravar em arquivos](../developing-apps/programming/drives-directories-files/writing-to-files.md)
- [My. Computer. FileSystem. ReadAllText](xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A)
- [My. Computer. FileSystem. WriteAllText](xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A)
