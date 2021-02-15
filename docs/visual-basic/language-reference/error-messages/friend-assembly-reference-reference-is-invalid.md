---
description: 'Saiba mais sobre: BC31535: a referência do assembly Friend <reference> é inválida'
title: A referência de assembly amigável <reference> é inválida.
ms.date: 07/20/2015
f1_keywords:
- vbc31535
- bc31535
helpviewer_keywords:
- BC31535
ms.assetid: 6540c1d0-bb19-4051-a579-2e4f9094585e
ms.openlocfilehash: e3e08edede9bee4710c415a61592857229ea4f35
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796191"
---
# <a name="bc31535-friend-assembly-reference-reference-is-invalid"></a>BC31535: a referência do assembly Friend \<reference> é inválida

A referência do assembly Friend \<reference> é inválida. O nome forte assinado em assemblies deve especificar uma chave pública em suas declarações InternalsVisibleTo.

 O nome do assembly passado para o <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> Construtor de atributo identifica um assembly de nome forte, mas não inclui um `PublicKey` atributo.

 **ID do erro:** BC31535

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Determine a chave pública para o assembly Friend de nome forte. Inclua a chave pública como parte do nome do assembly passado para o <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> Construtor de atributo usando o `PublicKey` atributo.

## <a name="see-also"></a>Consulte também

- <xref:System.Reflection.AssemblyName>
- [Assemblies Friend](../../../standard/assembly/friend.md)
