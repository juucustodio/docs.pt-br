---
title: Use 'FileGetObject' em vez de 'FileGet' quando usar argumento do tipo 'Object'
ms.date: 07/20/2015
ms.assetid: 090b8088-895a-482a-9362-606596bac304
ms.openlocfilehash: 318a0772a99aa86d9a4633e6021f77616a43fc7e
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91059399"
---
# <a name="use-filegetobject-instead-of-fileget-when-using-argument-of-type-object"></a>Use 'FileGetObject' em vez de 'FileGet' quando usar argumento do tipo 'Object'

O `FileGet` método inclui um argumento do tipo `Object` . `FileGetObject` deve ser usado no lugar de `FileGet` para evitar ambiguidades.  
  
 Observe que a funcionalidade oferecida pelo `My.Computer.Filesystem` oferece maior facilidade de uso e desempenho do que o `FileGet` ou o `FileGetObject` .  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Substitua `FileGet` por `FileGetObject`.  
  
2. Converta o `Object` argumento para um tipo mais específico.  
  
## <a name="see-also"></a>Confira também

- [My. Computer. FileSystem](xref:Microsoft.VisualBasic.FileIO.FileSystem)
