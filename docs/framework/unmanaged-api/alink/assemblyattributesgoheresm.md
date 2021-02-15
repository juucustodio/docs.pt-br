---
description: 'Saiba mais sobre: classe AssemblyAttributesGoHereSM'
title: Classe AssemblyAttributesGoHereSM (System. Runtime. Compiladorservices)
ms.date: 03/30/2017
api_name:
- System.Runtime.CompilerServices.AssemblyAttributesGoHereSM
api_location:
- mscorlib.dll
api_type:
- Assembly
f1_keywords:
- AssemblyAttributesGoHereSM
helpviewer_keywords:
- AssemblyAttributesGoHereSM type
- Alink API, AssemblyAttributesGoHereSM type
ms.assetid: 4cf9bf39-1527-49e0-a0e9-55e7a018bf66
topic_type:
- apiref
ms.openlocfilehash: ac38017b6ae9169b853da1daa8533d4c1cf44d97
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638516"
---
# <a name="assemblyattributesgoheresm-class"></a>Classe AssemblyAttributesGoHereSM

Usado pelo ALink como um espaço reservado para armazenar informações sobre atributos personalizados.

## <a name="syntax"></a>Sintaxe

```csharp
internal sealed class AssemblyAttributesGoHereSM
```

## <a name="remarks"></a>Comentários

As referências a esse tipo podem ser inseridas dentro de netmodules cujas fontes contêm atributos personalizados de assembly. Ao criar um manifesto do assembly a partir de um ou mais netmodules que contêm referências a esses tipos, o ALink usa informações anexadas a essas referências para emitir atributos personalizados reais. Dessa forma, esse tipo nunca é instanciado e as referências a ele são usadas somente como parte do processo de compilação e não atendem a nenhuma finalidade no assembly final.

Referências a esse tipo indicam atributos personalizados que são relacionados à segurança e ao uso múltiplo.

Esses tipos são marcados como "internos" dentro do .NET Framework e estão localizados no <xref:System.Runtime.CompilerServices> namespace.

## <a name="requirements"></a>Requisitos

mscorlib.dll

## <a name="see-also"></a>Consulte também

- [AssemblyAttributesGoHere](assemblyattributesgohere.md)
- [AssemblyAttributesGoHereM](assemblyattributesgoherem.md)
- [AssemblyAttributesGoHereS](assemblyattributesgoheres.md)
