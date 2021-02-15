---
title: 'Usando o Gerenciamento de Pacotes com F # para o Azure'
description: 'Usar o paket ou o NuGet para gerenciar as dependências do Azure F #'
author: sylvanc
ms.date: 09/20/2016
ms.custom: devx-track-fsharp
ms.openlocfilehash: 7816c82e87db113a35fef967886c8c3e27959332
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756228"
---
# <a name="package-management-for-f-azure-dependencies"></a>Pacote de gerenciamento para Dependências F# do Azure

A obtenção de pacotes para o desenvolvimento do Azure é fácil quando você usa um Gerenciador de pacotes. As duas opções são [paket](https://fsprojects.github.io/Paket/) e [NuGet](https://www.nuget.org/).

## <a name="using-paket"></a>Usando paket

Se você estiver usando o [paket](https://fsprojects.github.io/Paket/) como seu Gerenciador de dependências, poderá usar a `paket.exe` ferramenta para adicionar as dependências do Azure. Por exemplo:

```console
> paket add nuget WindowsAzure.Storage
```

Ou, se você estiver usando o [mono](https://www.mono-project.com/) para desenvolvimento em .net de plataforma cruzada:

```console
> mono paket.exe add nuget WindowsAzure.Storage
```

Isso adicionará `WindowsAzure.Storage` ao conjunto de dependências do pacote para o projeto no diretório atual, modificará o `paket.dependencies` arquivo e baixará o pacote. Se você tiver configurado as dependências anteriormente ou estiver trabalhando com um projeto em que as dependências foram configuradas por outro desenvolvedor, você poderá resolver e instalar dependências localmente da seguinte maneira:

```console
> paket install
```

Ou, para o desenvolvimento mono:

```console
> mono paket.exe install
```

Você pode atualizar todas as dependências de pacote para a versão mais recente como esta:

```console
> paket update
```

Ou, para o desenvolvimento mono:

```console
> mono paket.exe update
```

## <a name="using-nuget"></a>Usando o NuGet

Se você estiver usando o [NuGet](https://www.nuget.org/) como seu Gerenciador de dependências, poderá usar a `nuget.exe` ferramenta para adicionar as dependências do Azure. Por exemplo:

```console
> nuget install WindowsAzure.Storage -ExcludeVersion
```

Ou, para o desenvolvimento mono:

```console
> mono nuget.exe install WindowsAzure.Storage -ExcludeVersion
```

Isso adicionará `WindowsAzure.Storage` ao conjunto de dependências do pacote para o projeto no diretório atual e baixará o pacote. Se você tiver configurado as dependências anteriormente ou estiver trabalhando com um projeto em que as dependências foram configuradas por outro desenvolvedor, você poderá resolver e instalar dependências localmente da seguinte maneira:

```console
> nuget restore
```

Ou, para o desenvolvimento mono:

```console
> mono nuget.exe restore
```

Você pode atualizar todas as dependências de pacote para a versão mais recente como esta:

```console
> nuget update
```

Ou, para o desenvolvimento mono:

```console
> mono nuget.exe update
```

## <a name="referencing-assemblies"></a>Fazendo Referência a Assemblies

Para usar seus pacotes em seu script F #, você precisa fazer referência aos assemblies incluídos nos pacotes usando uma `#r` diretiva. Por exemplo:

```fsharp
> #r "packages/WindowsAzure.Storage/lib/net40/Microsoft.WindowsAzure.Storage.dll"
```

Como você pode ver, você precisará especificar o caminho relativo para a DLL e o nome de DLL completo, que pode não ser exatamente o mesmo que o nome do pacote. O caminho incluirá uma versão da estrutura e, possivelmente, um número de versão do pacote. Para localizar todos os assemblies instalados, você pode usar algo como este em uma linha de comando do Windows:

```console
> cd packages/WindowsAzure.Storage
> dir /s/b *.dll
```

Ou em um shell do UNIX, algo assim:

```console
> find packages/WindowsAzure.Storage -name "*.dll"
```

Isso fornecerá os caminhos para os assemblies instalados. A partir daí, você pode selecionar o caminho correto para a versão da estrutura.
