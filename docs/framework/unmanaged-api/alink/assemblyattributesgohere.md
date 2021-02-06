---
description: 'Saiba mais sobre: classe AssemblyAttributesGoHere'
title: Classe AssemblyAttributesGoHere (System. Runtime. Compiladorservices)
ms.date: 03/30/2017
api_name:
- System.Runtime.CompilerServices.AssemblyAttributesGoHere
api_location:
- mscorlib.dll
api_type:
- Assembly
f1_keywords:
- AssemblyAttributesGoHere
helpviewer_keywords:
- AssemblyAttributesGoHere type
- Alink API, AssemblyAttributesGoHere type
ms.assetid: 7b26fcb6-94f4-4f09-933e-b33efe451f4f
topic_type:
- apiref
ms.openlocfilehash: b95ff377f7fa0ffc85136dd69eb4a32121a50dc2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638581"
---
# <a name="assemblyattributesgohere-class"></a>Classe AssemblyAttributesGoHere

Usado pelo ALink como um espaço reservado para armazenar informações sobre atributos personalizados.

## <a name="syntax"></a>Sintaxe

```csharp
internal sealed class AssemblyAttributesGoHere
```

## <a name="remarks"></a>Comentários

As referências a esse tipo podem ser inseridas dentro de netmodules cujas fontes contêm atributos personalizados de assembly. Ao criar um manifesto do assembly a partir de um ou mais netmodules que contêm referências a esses tipos, o ALink usa informações anexadas a essas referências para emitir atributos personalizados reais. Dessa forma, esse tipo nunca é instanciado e as referências a ele são usadas somente como parte do processo de compilação e não atendem a nenhuma finalidade no assembly final.

Referências a este tipo indicam atributos personalizados que não são relacionados à segurança e não são de uso múltiplo.

Esses tipos são marcados como "internos" dentro do .NET Framework e estão localizados no <xref:System.Runtime.CompilerServices> namespace.

## <a name="requirements"></a>Requisitos

mscorlib.dll

## <a name="see-also"></a>Consulte também

- [AssemblyAttributesGoHereM](assemblyattributesgoherem.md)
- [AssemblyAttributesGoHereS](assemblyattributesgoheres.md)
- [AssemblyAttributesGoHereSM](assemblyattributesgoheresm.md)
