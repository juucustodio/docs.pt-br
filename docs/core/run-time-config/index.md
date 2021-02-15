---
title: Opções de configuração de tempo de execução
description: Saiba como configurar aplicativos .NET Core usando as definições de configuração de tempo de execução.
ms.date: 01/21/2020
ms.openlocfilehash: 5e9f292476cf953c3e63bb8e89268f7cc06b3bfc
ms.sourcegitcommit: 2b878d7011306b215dbf3d5dc9c1e78355a6dcd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2021
ms.locfileid: "98757844"
---
# <a name="net-core-run-time-configuration-settings"></a>Definições de configuração de tempo de execução do .NET Core

O .NET Core dá suporte ao uso de arquivos de configuração e variáveis de ambiente para configurar o comportamento de aplicativos .NET Core em tempo de execução. A configuração de tempo de execução é uma opção atraente se:

- Você não possui ou controla o código-fonte de um aplicativo e, portanto, não é possível configurá-lo programaticamente.

- Várias instâncias do seu aplicativo são executadas ao mesmo tempo em um único sistema e você deseja configurar cada uma para obter um desempenho ideal.

> [!NOTE]
> Esta documentação é um trabalho em andamento. Se você observar que as informações apresentadas aqui estão incompletas ou imprecisas, [abra um problema](https://github.com/dotnet/docs/issues) para nos informar sobre ela ou [envie uma solicitação de pull](https://github.com/dotnet/docs/pulls) para resolver o problema. Para obter informações sobre como enviar solicitações pull para o repositório dotnet/docs, consulte o [Guia do colaborador](/contribute/dotnet/dotnet-contribute).

O .NET Core fornece os seguintes mecanismos para configurar o comportamento do aplicativo em tempo de execução:

- O [runtimeconfig.jsno arquivo](#runtimeconfigjson)

- [propriedades MSBuild](#msbuild-properties)

- [Variáveis de ambiente](#environment-variables)

> [!TIP]
> A configuração de uma opção de tempo de execução usando uma variável de ambiente aplica a configuração a todos os aplicativos .NET Core. A configuração de uma opção de tempo de execução no *runtimeconfig.jsno ou no* arquivo de projeto aplica a configuração somente a esse aplicativo.

Alguns valores de configuração também podem ser definidos programaticamente chamando o <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> método.

Os artigos nesta seção da documentação são organizados por categoria, por exemplo, [depuração](debugging-profiling.md) e coleta de [lixo](garbage-collector.md). Quando aplicável, as opções de configuração são mostradas para *runtimeconfig.jsem* arquivos, propriedades do MSBuild, variáveis de ambiente e, para referência cruzada *app.config* arquivos para projetos de .NET Framework.

## <a name="runtimeconfigjson"></a>runtimeconfig.jsem

Quando um projeto é [compilado](../tools/dotnet-build.md), um *[AppName] .runtimeconfig.jsno* arquivo é gerado no diretório de saída. Se uma *runtimeconfig.template.jsno* arquivo existir na mesma pasta que o arquivo de projeto, todas as opções de configuração contidas nela serão inseridas na *.runtimeconfig.js[AppName] no* arquivo. Se você estiver criando o aplicativo por conta própria, coloque as opções de configuração na *runtimeconfig.template.jsno* arquivo. Se você estiver apenas executando o aplicativo, insira-os diretamente no *[AppName] .runtimeconfig.jsno* arquivo.

> [!NOTE]
> O *[AppName] .runtimeconfig.jsno* arquivo será substituído em compilações subsequentes.

Especifique as opções de configuração de tempo de execução na seção **configproperties** do *runtimeconfig.jsem* arquivos. Esta seção tem o formato:

```json
"configProperties": {
  "config-property-name1": "config-value1",
  "config-property-name2": "config-value2"
}
```

### <a name="example-appnameruntimeconfigjson-file"></a>Exemplo [AppName] .runtimeconfig.jsno arquivo

Se você estiver colocando as opções no arquivo JSON de saída, aninhe-as na `runtimeOptions` propriedade.

```json
{
  "runtimeOptions": {
    "tfm": "netcoreapp3.1",
    "framework": {
      "name": "Microsoft.NETCore.App",
      "version": "3.1.0"
    },
    "configProperties": {
      "System.GC.Concurrent": false,
      "System.Threading.ThreadPool.MinThreads": 4,
      "System.Threading.ThreadPool.MaxThreads": 25
    }
  }
}
```

### <a name="example-runtimeconfigtemplatejson-file"></a>Exemplo runtimeconfig.template.jsno arquivo

Se você estiver colocando as opções no arquivo JSON de modelo, omita a `runtimeOptions` propriedade.

```json
{
  "configProperties": {
    "System.GC.Concurrent": false,
    "System.Threading.ThreadPool.MinThreads": "4",
    "System.Threading.ThreadPool.MaxThreads": "25"
  }
}
```

## <a name="msbuild-properties"></a>propriedades MSBuild

Algumas opções de configuração de tempo de execução podem ser definidas usando as propriedades do MSBuild no arquivo *. csproj* ou *. vbproj* dos projetos do .NET Core do estilo SDK. As propriedades do MSBuild têm precedência sobre as opções definidas na *runtimeconfig.template.jsno* arquivo.

Aqui está um exemplo de arquivo de projeto no estilo SDK com propriedades do MSBuild para configurar o comportamento de tempo de execução:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <PropertyGroup>
    <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
    <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
    <ThreadPoolMaxThreads>25</ThreadPoolMaxThreads>
  </PropertyGroup>

</Project>
```

As propriedades do MSBuild para configurar o comportamento de tempo de execução são indicadas nos artigos individuais para cada área, por exemplo, [coleta de lixo](garbage-collector.md). Eles também estão listados na seção de [configuração de tempo de execução](../project-sdk/msbuild-props.md#run-time-configuration-properties) da referência de propriedades do MSBuild para projetos em estilo SDK.

## <a name="environment-variables"></a>Variáveis de ambiente

As variáveis de ambiente podem ser usadas para fornecer algumas informações de configuração de tempo de execução. A configuração de uma opção de tempo de execução usando uma variável de ambiente aplica a configuração a todos os aplicativos .NET Core. Os botões de configuração especificados como variáveis de ambiente geralmente têm o prefixo **COMPlus_**.

Você pode definir variáveis de ambiente no painel de controle do Windows, na linha de comando ou programaticamente chamando o <xref:System.Environment.SetEnvironmentVariable(System.String,System.String)?displayProperty=nameWithType> método em sistemas baseados no Windows e no UNIX.

Os exemplos a seguir mostram como definir uma variável de ambiente na linha de comando:

```shell
# Windows
set COMPlus_GCRetainVM=1

# Powershell
$env:COMPlus_GCRetainVM="1"

# Unix
export COMPlus_GCRetainVM=1
```
