---
description: Saiba mais sobre:-delaysign
title: -delaysign
ms.date: 03/10/2018
helpviewer_keywords:
- delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
ms.openlocfilehash: fc3e52f63431da870355e369e6ffeb8b7b14c5ab
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100461496"
---
# <a name="-delaysign"></a>-delaysign

Especifica se o assembly será assinado total ou parcialmente.

## <a name="syntax"></a>Sintaxe

```console
-delaysign[+ | -]
```

## <a name="arguments"></a>Argumentos

`+` &#124; `-`  
Opcional. Use `-delaysign-` se você quiser um assembly totalmente assinado. Use `-delaysign+` se você quiser posicionar a chave pública no assembly e reservar espaço para o hash assinado. O padrão é `-delaysign-`.

## <a name="remarks"></a>Comentários

A `-delaysign` opção não tem nenhum efeito, a menos que seja usada com [-keyfile](keyfile.md) ou [-keycontainer](keycontainer.md).

Quando você solicita um assembly totalmente assinado, o compilador usa o hash no arquivo que contém o manifesto (metadados de assembly) e sinaliza esse hash com a chave particular. A assinatura digital resultante é armazenada no arquivo que contém o manifesto. Quando um assembly é assinado com atraso, o compilador não computa e armazena a assinatura, mas reserva espaço no arquivo para que a assinatura possa ser adicionada posteriormente.

Por exemplo, usando `-delaysign+` o, um desenvolvedor em uma organização pode distribuir versões de teste não assinadas de um assembly que os testadores podem registrar com o cache de assembly global e usar. Quando o trabalho no assembly é concluído, a pessoa responsável pela chave privada da organização pode assinar totalmente o assembly. Essa compartimentalização protege a chave privada da organização contra a divulgação, ao mesmo tempo que permite que todos os desenvolvedores trabalhem nos assemblies.

Consulte [criando e usando assemblies de Strong-Named](../../../standard/assembly/create-use-strong-named.md) para obter mais informações sobre como assinar um assembly.

### <a name="to-set--delaysign-in-the-visual-studio-integrated-development-environment"></a>Para Set-delaysign no ambiente de desenvolvimento integrado do Visual Studio

1. Selecione um projeto no **Gerenciador de Soluções**. No menu **Projeto** , clique em **Propriedades**.

2. Clique na guia **Assinatura** .

3. Defina o valor na caixa **somente assinatura de atraso** .

## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [-keyfile](keyfile.md)
- [-keycontainer](keycontainer.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
