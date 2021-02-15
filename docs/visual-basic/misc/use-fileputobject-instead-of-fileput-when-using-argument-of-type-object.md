---
description: "Saiba mais sobre: use ' FilePutObject ' em vez de ' FilePut ' ao usar argumento do tipo ' Object '"
title: Use 'FilePutObject' em vez de 'FilePut' quando usar argumento do tipo 'Object'
ms.date: 07/20/2015
f1_keywords:
- vbrUseFilePutObject
ms.assetid: d207b9b7-5898-4c13-8b03-9feefac5f726
ms.openlocfilehash: 5e5822999aa39bff4d43f83a2719341034cdcadc
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100460092"
---
# <a name="use-fileputobject-instead-of-fileput-when-using-argument-of-type-object"></a>Use 'FilePutObject' em vez de 'FilePut' quando usar argumento do tipo 'Object'

O `FilePut` método inclui um argumento do tipo `Object` . `FilePutObject` deve ser usado no lugar de `FilePut` para evitar ambiguidades.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Substitua `FilePut` por `FilePutObject`.  
  
- Converta o `Object` argumento para um tipo mais específico.  
  
- Use a funcionalidade disponível no `My.Computer.FileSystem` objeto.  
  
## <a name="see-also"></a>Consulte também

- [My. Computer. FileSystem](xref:Microsoft.VisualBasic.FileIO.FileSystem)
- [My. Computer. FileSystem. WriteAllBytesAsyncInternal](xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.WriteAllBytes%2A)
