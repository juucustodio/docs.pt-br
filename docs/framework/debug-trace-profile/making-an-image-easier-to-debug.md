---
title: Tornando uma imagem mais fácil de depurar no .NET
description: Saiba como configurar uma imagem executável para uma depuração mais fácil usando comutadores IDE e opções de linha de comando.
ms.date: 08/30/2018
helpviewer_keywords:
- images [.NET Framework], debugging
- executable image for debugging
- debugging [.NET Framework], executable images for
ms.assetid: 7d90ea7a-150f-4f97-98a7-f9c26541b9a3
ms.openlocfilehash: a3305dc864e7852c2336009503732a51868410d2
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558505"
---
# <a name="making-an-image-easier-to-debug-in-net"></a>Tornando uma imagem mais fácil de depurar no .NET

Ao compilar código não gerenciado, você pode configurar uma imagem executável para depuração, definindo opções de IDE ou opções de linha de comando. Por exemplo, você pode usar a opção de linha de comando /**Zi** no Visual C++ para solicitar a ele que emita arquivos de símbolo de depuração (extensão de arquivo .pdb). De modo similar, a opção de linha de comando /**Od** informa ao compilador para desabilitar a otimização. O código resultante é executado mais lentamente, mas é mais fácil de depurar, caso isso seja necessário.

Ao compilar .NET Framework código gerenciado, compiladores como Visual C++, Visual Basic e C# compilam seu programa de origem no MSIL (Microsoft Intermediate Language). A MSIL é então compilada por JIT, logo antes da execução, em código de máquina nativo. Assim como ocorre com código não gerenciado, você pode configurar uma imagem executável para depuração, definindo opções de IDE ou opções de linha de comando. Você também pode configurar a compilação JIT para depuração praticamente da mesma maneira.

Essa configuração de JIT tem dois aspectos:

- Você pode solicitar que o compilador JIT gere informações de rastreamento. Isso possibilita que o depurador faça a correspondência entre uma cadeia de MSIL com seu equivalente em código de máquina e que controle o local em que os argumentos de função e variáveis locais são armazenados. A partir do .NET Framework versão 2,0, o compilador JIT sempre gera informações de rastreamento, portanto, não há necessidade de solicitá-la.

- Você pode solicitar que o compilador JIT não Otimize o código do computador resultante.

Normalmente, o compilador que gera a MSIL define essas opções de compilador JIT adequadamente, com base nos comutadores IDE ou nas opções de linha de comando que você especificar, por exemplo,/**OD**.

Em alguns casos, talvez você queira alterar o comportamento do compilador JIT para que o código de máquina gerado por ele seja mais fácil de depurar. Por exemplo, talvez você queira gerar informações de acompanhamento JIT de um build de varejo ou controlar a otimização. Você pode fazer isso com um arquivo de inicialização (.ini).

Por exemplo, se o assembly que você deseja depurar for chamado *MyApp.exe*, você poderá criar um arquivo de texto chamado *MyApp.ini*, na mesma pasta que *MyApp.exe*, que contém estas três linhas:

```ini
[.NET Framework Debugging Control]
GenerateTrackingInfo=1
AllowOptimize=0
```

Você pode definir o valor de cada opção como 0 ou 1 e qualquer opção ausente assume 0 por padrão. Configurar `GenerateTrackingInfo` como 1 e `AllowOptimize` como 0 proporciona a depuração mais fácil.

A partir do .NET Framework versão 2,0, o compilador JIT sempre gera informações de rastreamento, independentemente do valor de `GenerateTrackingInfo` ; no entanto, o `AllowOptimize` valor ainda tem um efeito. Ao usar o [Ngen.exe (Gerador de Imagens Nativas)](../tools/ngen-exe-native-image-generator.md) para pré-compilar a imagem nativa sem otimização, o arquivo .ini deve estar presente na pasta de destino com `AllowOptimize=0` quando Ngen.exe for executado. Se você tiver pré-compilado um assembly sem otimização, deverá remover o código pré-compilado usando a opção NGen.exe **/Uninstall** antes de executar novamente Ngen.exe para pré-compilar o código como otimizado. Se o arquivo. ini não estiver presente na pasta, por padrão Ngen.exe pré-compila o código como otimizado.

O <xref:System.Diagnostics.DebuggableAttribute?displayProperty=nameWithType> controla as configurações de um assembly. O **DebuggableAttribute** inclui dois campos que controlam se o compilador JIT deve otimizar e/ou gerar informações de rastreamento. A partir do .NET Framework versão 2,0, o compilador JIT sempre gera informações de rastreamento.

Para uma compilação de varejo, os compiladores não definem o **DebuggableAttribute**. Por padrão, o compilador JIT gera o mais alto desempenho, o mais difícil de depurar o código da máquina. Habilitar o acompanhamento JIT reduz um pouco o desempenho, enquanto desabilitar a otimização reduz muito o desempenho.

O **DebuggableAttribute** aplica-se a um assembly inteiro por vez e não a módulos individuais dentro do assembly. Ferramentas de desenvolvimento, portanto, deverão anexar atributos personalizados ao token de metadados de assembly se um assembly já tiver sido criado ou então anexá-los à classe chamada **System.Runtime.CompilerServices.AssemblyAttributesGoHere**. Em seguida, a ferramenta ALink promove esses atributos **DebuggableAttribute** de cada módulo para o assembly do qual eles se tornam parte. Se houver um conflito, a operação ALink falhará.

> [!NOTE]
> Na versão 1.0 do .NET Framework, o compilador do Microsoft Visual C++ adiciona o **DebuggableAttribute** quando as opções do compilador **/clr** e **/Zi** são especificadas. Na versão 1,1 do .NET Framework, você deve adicionar o **DebuggableAttribute** manualmente em seu código ou usar a opção de vinculador **/ASSEMBLYDEBUG** .

## <a name="see-also"></a>Confira também

- [Depuração, rastreamento e criação de perfil](index.md)
- [Habilitando a depuração por anexação JIT](enabling-jit-attach-debugging.md)
- [Habilitando a criação de perfil](/previous-versions/dotnet/netframework-4.0/s5ec0es1(v=vs.100))
