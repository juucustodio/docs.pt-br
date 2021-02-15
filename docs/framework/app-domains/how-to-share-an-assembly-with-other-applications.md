---
title: 'Como: compartilhar um assembly com outros aplicativos'
description: Consulte Como compartilhar um assembly com outros aplicativos no .NET. Os assemblies podem ser privados (o padrão) ou compartilhado. Para compartilhar um assembly, coloque-o no GAC.
ms.date: 08/19/2019
ms.assetid: c30e972b-1693-4e05-b115-c31831fdf9f2
ms.openlocfilehash: 1056f8b555713d5d67488537e6c06cc457c4d312
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242533"
---
# <a name="how-to-share-an-assembly-with-other-applications"></a>Como: compartilhar um assembly com outros aplicativos

Os assemblies podem ser particulares ou compartilhados: por padrão, a maioria dos programas simples consistem em um assembly particular porque eles não se destinam a serem usados por outros aplicativos.  

Para compartilhar um assembly com outros aplicativos, ele deve ser colocado no [GAC (cache de assembly global)](gac.md).  
  
Para compartilhar um assembly:
  
1. Crie o assembly. Para obter mais informações, consulte [criar assemblies](../../standard/assembly/create.md).  
  
2. Atribua um nome forte ao assembly. Para obter mais informações, consulte [como assinar um assembly com um nome forte](../../standard/assembly/sign-strong-name.md).  
  
3. Atribua informações de versão ao assembly. Para obter mais informações, consulte [controle de versão do assembly](../../standard/assembly/versioning.md).  
  
4. Adicione seu assembly ao cache de assembly global. Para obter mais informações, consulte [como: instalar um assembly no cache de assembly global](install-assembly-into-gac.md).  
  
5. Acesse os tipos contidos no assembly de outros aplicativos. Para obter mais informações, consulte [como referenciar um assembly de nome forte](../../standard/assembly/reference-strong-named.md).  
  
## <a name="see-also"></a>Veja também

- [Guia de programação em C#](../../../api/index.md)
- [Conceitos de programação (Visual Basic)](../../../api/index.md)
- [Programar com assemblies](../../standard/assembly/index.md)
