---
title: Verificar as versões do .NET instaladas no Windows, Linux e macOS-.NET
description: Saiba como listar quais versões do .NET estão instaladas em seu computador. Isso inclui o .NET Runtime e o SDK.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: 2fc12c8c398b1a74d623e53884df666f4d4b85f1
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851608"
---
# <a name="how-to-check-that-net-is-already-installed"></a>Como verificar se o .NET já está instalado

Este artigo ensina como verificar quais versões do .NET Runtime e do SDK estão instaladas no seu computador. Se você tiver um ambiente de desenvolvimento integrado, como o Visual Studio ou o Visual Studio para Mac, o .NET pode já ter sido instalado.

A instalação de um SDK instala o tempo de execução correspondente.

Se qualquer comando deste artigo falhar, você não tem o tempo de execução ou o SDK instalado. Para obter mais informações, consulte os artigos de instalação para [Windows](windows.md), [MacOS](macos.md)ou [Linux](linux.md).

## <a name="check-sdk-versions"></a>Verificar versões do SDK

Você pode ver quais versões do SDK do .NET estão instaladas atualmente com um terminal. Abra um terminal e execute o comando a seguir.

```dotnetcli
dotnet --list-sdks
```

Você Obtém uma saída semelhante à seguinte.

::: zone pivot="os-windows"

```console
2.1.500 [C:\program files\dotnet\sdk]
2.1.502 [C:\program files\dotnet\sdk]
2.1.504 [C:\program files\dotnet\sdk]
2.1.600 [C:\program files\dotnet\sdk]
2.1.602 [C:\program files\dotnet\sdk]
3.1.100 [C:\program files\dotnet\sdk]
5.0.100 [C:\program files\dotnet\sdk]
```

::: zone-end

::: zone pivot="os-linux"

```bash
2.1.500 [/home/user/dotnet/sdk]
2.1.502 [/home/user/dotnet/sdk]
2.1.504 [/home/user/dotnet/sdk]
2.1.600 [/home/user/dotnet/sdk]
2.1.602 [/home/user/dotnet/sdk]
3.1.100 [/home/user/dotnet/sdk]
5.0.100 [/home/user/dotnet/sdk]
```

::: zone-end

::: zone pivot="os-macos"

```bash
2.1.500 [/usr/local/share/dotnet/sdk]
2.1.502 [/usr/local/share/dotnet/sdk]
2.1.504 [/usr/local/share/dotnet/sdk]
2.1.600 [/usr/local/share/dotnet/sdk]
2.1.602 [/usr/local/share/dotnet/sdk]
3.1.100 [/usr/local/share/dotnet/sdk]
5.0.100 [/usr/local/share/dotnet/sdk]
```

::: zone-end

## <a name="check-runtime-versions"></a>Verificar versões de tempo de execução

Você pode ver quais versões do tempo de execução do .NET estão instaladas no momento com o comando a seguir.

```dotnetcli
dotnet --list-runtimes
```

Você Obtém uma saída semelhante à seguinte.

::: zone pivot="os-windows"

```console
Microsoft.AspNetCore.All 2.1.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 5.0.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 5.0.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.WindowsDesktop.App 3.0.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
Microsoft.WindowsDesktop.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
Microsoft.WindowsDesktop.App 5.0.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
```

::: zone-end

::: zone pivot="os-linux"

```bash
Microsoft.AspNetCore.All 2.1.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 5.0.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 5.0.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
```

::: zone-end

::: zone pivot="os-macos"

```bash
Microsoft.AspNetCore.All 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 5.0.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 5.0.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
```

::: zone-end

## <a name="check-for-install-folders"></a>Verificar pastas de instalação

É possível que o .NET esteja instalado, mas não adicionado à `PATH` variável do seu sistema operacional ou perfil do usuário. Nesse caso, os comandos das seções anteriores podem não funcionar. Como alternativa, você pode verificar se as pastas de instalação do .NET existem.

Quando você instala o .NET de um instalador ou script, ele é instalado em uma pasta padrão. Na maior parte do tempo, o instalador ou o script que você está usando para instalar o .NET oferece uma opção para instalar em uma pasta diferente. Se você optar por instalar o em uma pasta diferente, ajuste o início do caminho da pasta.

::: zone pivot="os-windows"

- **executável dotnet**\
_C: \\ arquivos de programas \\ dotnet \\dotnet.exe_

- **SDK .NET**\
_C: \\ arquivos de \\ programas \\ SDK do dotnet \\ {versão}\\_

- **Tempo de execução do .NET**\
_C: \\ arquivos de programas \\ dotnet \\ compartilhado \\ {tipo de tempo de execução} \\ {versão}\\_

::: zone-end

::: zone pivot="os-linux"

- **executável dotnet**\
_/home/user/share/dotnet/dotnet_

- **SDK .NET**\
_/home/user/share/dotnet/sdk/{version}/_

- **Tempo de execução do .NET**\
_/home/user/share/dotnet/shared/{runtime-type}/{version}/_

::: zone-end

::: zone pivot="os-macos"

- **executável dotnet**\
_/usr/local/share/dotnet/dotnet_

- **SDK .NET**\
_/usr/local/share/dotnet/sdk/{version}/_

- **Tempo de execução do .NET**\
_/usr/local/share/dotnet/shared/{runtime-type}/{version}/_

::: zone-end

## <a name="more-information"></a>Mais informações

Você pode ver as versões do SDK e as versões de tempo de execução com o comando `dotnet --info` . Você também obterá outras informações relacionadas ao ambiente, como a versão do sistema operacional e o RID (identificador de tempo de execução).

## <a name="next-steps"></a>Próximas etapas

- [Instale o tempo de execução e o SDK do .net para Windows](windows.md).
- [Instale o tempo de execução e o SDK do .net para MacOS](macos.md).
- [Instale o tempo de execução e o SDK do .net para Linux](linux.md).

## <a name="see-also"></a>Confira também

- [Determinar quais versões do .NET Framework estão instaladas](../../framework/migration-guide/how-to-determine-which-versions-are-installed.md)
