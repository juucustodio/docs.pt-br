---
description: "Saiba mais sobre: BC30007: referência necessária para o assembly ' <assemblyname> ' que contém a classe base '<classname>"
title: Referência obrigatória ao assembly '<assemblyname>' que contém a classe base '<classname>'
ms.date: 07/20/2015
f1_keywords:
- bc30007
- vbc30007
helpviewer_keywords:
- BC30007
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
ms.openlocfilehash: f01795d3e8147015f9f46697b047a8c63099ff32
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792044"
---
# <a name="bc30007-reference-required-to-assembly-assemblyname-containing-the-base-class-classname"></a>BC30007: referência necessária para o assembly ' \<assemblyname> ' que contém a classe base ' \<classname> '

Referência necessária para o assembly ' \<assemblyname> ' que contém a classe base ' \<classname> '. Adicione um ao seu projeto.

 A classe é definida em uma DLL (biblioteca de vínculo dinâmico) ou assembly que não é referenciada diretamente em seu projeto. O compilador Visual Basic requer uma referência para evitar ambigüidade, caso a classe esteja definida em mais de uma DLL ou assembly.

 **ID do erro:** BC30007

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Inclua o nome da DLL ou assembly não referenciado em suas referências de projeto.

## <a name="see-also"></a>Consulte também

- [Gerenciando referências em um projeto](/visualstudio/ide/managing-references-in-a-project)
- [Solução de Problemas de Referências Quebradas](/visualstudio/ide/troubleshooting-broken-references)
