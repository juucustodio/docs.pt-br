---
description: 'Saiba mais sobre: BC30140: erro ao criar o manifesto do assembly: <error message>'
title: 'Erro na criação de manifesto do assembly: <error message>'
ms.date: 07/20/2015
f1_keywords:
- bc30140
- vbc30140
helpviewer_keywords:
- BC30140
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
ms.openlocfilehash: 4116f3293a36f4592712c3e39c988aa730753de4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796529"
---
# <a name="bc30140-error-creating-assembly-manifest-error-message"></a>BC30140: erro ao criar o manifesto do assembly: \<error message>

O compilador Visual Basic chama o vinculador de assembly (Al.exe, também conhecido como ALink) para gerar um assembly com um manifesto. O vinculador reportou um erro no estágio de pré-emissão da criação do assembly.

 Isso pode ocorrer se houver problemas com o arquivo de chave ou o contêiner de chave especificado. Para marcar totalmente um assembly, é necessário fornecer um arquivo de chave válido que contenha informações sobre as chaves públicas e privadas. Para marcar um atraso em um assembly, é necessário marcar a caixa de seleção **Somente sinal de atraso** e fornecer um arquivo de chave válido que contenha informações sobre as informações de chave pública. A chave privada não é necessária quando um assembly estiver marcado com atraso. Para obter mais informações, confira [Como assinar um assembly com um nome forte](../../../standard/assembly/sign-strong-name.md).

 **ID do erro:** BC30140

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Examine a mensagem de erro entre aspas e consulte o tópico [Al.exe](../../../framework/tools/al-exe-assembly-linker.md). para ver o erro AL1019 mais explicações e conselhos

2. Se o erro persistir, reúna informações sobre as circunstâncias e notifique o Microsoft Product Support Services.

## <a name="see-also"></a>Consulte também

- [Como assinar um assembly com um nome forte](../../../standard/assembly/sign-strong-name.md)
- [Página de Assinatura, Designer de Projeto](/visualstudio/ide/reference/signing-page-project-designer)
- [Al.exe](../../../framework/tools/al-exe-assembly-linker.md)
- [Fale conosco](/visualstudio/ide/feedback-options)
