---
description: 'Saiba mais sobre: modo de arquivo inadequado'
title: Modo de arquivo inválido
ms.date: 07/20/2015
f1_keywords:
- vbrID54
ms.assetid: 74891e96-884b-4c8d-872d-cd11ae272372
ms.openlocfilehash: da792407fb37f5c206be7ff39da14d314ef1e2d2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797075"
---
# <a name="bad-file-mode"></a>Modo de arquivo inválido

As instruções usadas na manipulação do conteúdo do arquivo devem ser apropriadas para o modo no qual o arquivo foi aberto. As possíveis causas incluem:  
  
- Uma `FilePutObject` `FileGetObject` instrução or especifica um arquivo sequencial.  
  
- Uma `Print` instrução especifica um arquivo aberto para um modo de acesso diferente de `Output` ou `Append` .  
  
- Uma `Input` instrução especifica um arquivo aberto para um modo de acesso diferente de `Input`  
  
- Uma tentativa de gravar em um arquivo somente leitura.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Certifique-se de que `FilePutObject` e `FileGetObject` estão apenas se referindo a arquivos abertos para o `Random` ou o `Binary` Access.  
  
- Certifique-se `Print` de especificar um arquivo aberto para o `Output` modo de `Append` acesso ou. Caso contrário, use uma instrução diferente para inserir dados no arquivo ou reabra o arquivo em um modo apropriado.  
  
- Certifique-se `Input` de especificar um arquivo aberto para `Input` . Caso contrário, use uma instrução diferente para inserir dados no arquivo ou reabra o arquivo em um modo apropriado.  
  
- Se você estiver gravando em um arquivo somente leitura, altere o status de leitura/gravação do arquivo ou não tente gravar nele.  
  
- Use a funcionalidade disponível no `My.Computer.FileSystem` objeto.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.FileSystem>
- [Solução de problemas: ler e gravar em arquivos de texto](../../developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
