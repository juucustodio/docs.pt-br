---
title: Criar assemblies
description: Saiba como criar assemblies de arquivo único ou de multiarquivos usando um IDE, como o Visual Studio, ou os compiladores e ferramentas fornecidos pelo SDK do Windows.
ms.date: 08/19/2019
helpviewer_keywords:
- assemblies [.NET], multifile
- single-file assemblies
- assemblies [.NET], creating
- multifile assemblies
ms.assetid: 54832ee9-dca8-4c8b-913c-c0b9d265e9a4
ms.openlocfilehash: e1b08e40ae3b4c377cec52cb1ebf6db643af6429
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160575"
---
# <a name="create-assemblies"></a>Criar assemblies

Você pode criar assemblies de vários arquivos ou um único arquivo usando um IDE, como Visual Studio, ou outros compiladores e ferramentas fornecidos pelo SDK do Windows. O assembly mais simples é um único arquivo que tem um nome simples e é carregado em um único domínio de aplicativo. Esse assembly não pode ser referenciado por outros assemblies fora do diretório do aplicativo e não é submetido à verificação de versão. Para desinstalar o aplicativo composto do assembly, você simplesmente exclui o diretório em que ele reside. Para muitos desenvolvedores, um assembly com esses recursos é tudo o que é necessário para implantar um aplicativo.

Você pode criar um assembly de vários arquivos de vários módulos de código e arquivos de recurso. Você também pode criar um assembly que pode ser compartilhado por vários aplicativos. Um assembly compartilhado deve ter um nome forte e pode ser implantado no cache de assembly global.

Você tem várias opções ao agrupar módulos de código e recursos em assemblies, dependendo dos seguintes fatores:

- Controle de versão

     Agrupe módulos que devem ter as mesmas informações de versão.

- Implantação

     Agrupe recursos e módulos de código que dão suporte ao seu modelo de implantação.

- Reutilizar

     Agrupe os módulos se eles puderem ser usados em conjunto de forma lógica para alguma finalidade. Por exemplo, um assembly composto pelos tipos e classes usados com pouca frequência para a manutenção do programa podem ser colocados no mesmo assembly. Além disso, os tipos que você pretende compartilhar com vários aplicativos devem ser agrupados em um assembly e o assembly deve ser assinado com um nome forte.

- Segurança

     Agrupe módulos que contêm tipos que exigem as mesmas permissões de segurança.

- Scoping

     Agrupe módulos que contêm tipos cuja visibilidade deve ser restrita ao mesmo assembly.

Há considerações especiais ao tornar Common Language Runtime assemblies disponíveis para aplicativos COM não gerenciados. Para obter mais informações sobre como trabalhar com código não gerenciado, consulte [expor .NET Framework Components to com](../../framework/interop/exposing-dotnet-components-to-com.md).

## <a name="see-also"></a>Veja também

- [Controle de versão do assembly](versioning.md)
- [Como: criar um assembly de arquivo único](../../framework/app-domains/build-single-file-assembly.md)
- [Como: criar um assembly de vários arquivos](../../framework/app-domains/build-multifile-assembly.md)
- [Como o tempo de execução localiza assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [Assemblies de vários arquivos](../../framework/app-domains/multifile-assemblies.md)
