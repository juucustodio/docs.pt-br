---
description: "Saiba mais sobre: BC30969: referência necessária para o assembly ' <assemblyidentity> ' contendo o tipo ' <typename> ', mas não foi possível encontrar uma referência adequada devido à ambiguidade entre os projetos ' <projectname1> ' e ' <projectname2> '"
title: Referência obrigatória ao assembly '<assemblyidentity>' contendo o tipo '<typename>', mas não foi possível localizar uma referência adequada devido à ambiguidade entre os projetos '<projectname1>' e '<projectname2>'
ms.date: 07/20/2015
f1_keywords:
- bc30969
- vbc30969
helpviewer_keywords:
- BC30969
ms.assetid: 1b29dbc5-8268-45fe-bfc2-b2070a5c845c
ms.openlocfilehash: 93713fe2175c303b7d126a7c3d5e33f9990955a1
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100481656"
---
# <a name="bc30969-reference-required-to-assembly-assemblyidentity-containing-type-typename-but-a-suitable-reference-could-not-be-found-due-to-ambiguity-between-projects-projectname1-and-projectname2"></a>BC30969: referência necessária para o assembly ' \<assemblyidentity> ' contendo o tipo ' \<typename> ', mas não foi possível encontrar uma referência adequada devido à ambiguidade entre os projetos ' \<projectname1> ' e ' \<projectname2> '

Uma expressão usa um tipo, como uma classe, estrutura, interface, enumeração ou delegado, que é definido fora do seu projeto. No entanto, você tem referências de projeto para mais de um assembly que define esse tipo.

 Os projetos citados produzem assemblies com o mesmo nome. Portanto, o compilador não pode determinar qual assembly usar para o tipo que você está acessando.

 Para acessar um tipo definido em outro assembly, o compilador Visual Basic deve ter uma referência a esse assembly. Essa deve ser uma referência única e não ambígua que não cause referências circulares entre projetos.

 **ID do erro:** BC30969

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Determine qual projeto produz o melhor assembly para referência do seu projeto. Para essa decisão, você pode usar critérios como a facilidade de acesso a arquivos e a frequência de atualizações.

2. Nas propriedades do projeto, adicione uma referência ao arquivo que contém o assembly que define o tipo que você está usando.

## <a name="see-also"></a>Consulte também

- [Gerenciando referências em um projeto](/visualstudio/ide/managing-references-in-a-project)
- [Referências a elementos declarados](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)

- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
- [Solução de Problemas de Referências Quebradas](/visualstudio/ide/troubleshooting-broken-references)
