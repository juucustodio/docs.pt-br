---
title: Propriedades do MSBuild para Microsoft. NET. Sdk
description: Referência para as propriedades e os itens do MSBuild que são compreendidos pelo SDK do .NET.
ms.date: 02/14/2020
ms.topic: reference
ms.custom: updateeachrelease
ms.openlocfilehash: 9cd387a4a8ad7f5b31a797d4d019a53799d926ff
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100432696"
---
# <a name="msbuild-reference-for-net-sdk-projects"></a>Referência do MSBuild para projetos do SDK do .NET

Esta página é uma referência para as propriedades e os itens do MSBuild que você pode usar para configurar projetos do .NET.

> [!NOTE]
> Esta página é um trabalho em andamento e não lista todas as propriedades de MSBuild úteis para o SDK do .NET. Para obter uma lista de propriedades comuns do MSBuild, consulte [Propriedades comuns do MSBuild](/visualstudio/msbuild/common-msbuild-project-properties).

## <a name="framework-properties"></a>Propriedades da estrutura

- [TargetFramework](#targetframework)
- [TargetFrameworks](#targetframeworks)
- [NetStandardImplicitPackageVersion](#netstandardimplicitpackageversion)

### <a name="targetframework"></a>TargetFramework

A `TargetFramework` propriedade especifica a versão do Framework de destino para o aplicativo. Para obter uma lista de monikers de estrutura de destino válidos, consulte [estruturas de destino em projetos em estilo SDK](../../standard/frameworks.md#supported-target-frameworks).

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

Para obter mais informações, consulte [estruturas de destino em projetos em estilo SDK](../../standard/frameworks.md).

### <a name="targetframeworks"></a>TargetFrameworks

Use a `TargetFrameworks` propriedade quando desejar que seu aplicativo direcione várias plataformas. Para obter uma lista de monikers de estrutura de destino válidos, consulte [estruturas de destino em projetos em estilo SDK](../../standard/frameworks.md#supported-target-frameworks).

> [!NOTE]
> Essa propriedade será ignorada se `TargetFramework` (singular) for especificado.

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
</PropertyGroup>
```

Para obter mais informações, consulte [estruturas de destino em projetos em estilo SDK](../../standard/frameworks.md).

### <a name="netstandardimplicitpackageversion"></a>NetStandardImplicitPackageVersion

> [!NOTE]
> Essa propriedade só se aplica a projetos que usam o `netstandard1.x` . Ele não se aplica a projetos que usam o `netstandard2.x` .

Use a `NetStandardImplicitPackageVersion` propriedade quando desejar especificar uma versão de estrutura inferior à versão do metapacote. O arquivo de projeto no exemplo a seguir tem `netstandard1.3` como destino, mas usa a versão 1.6.0 do `NETStandard.Library` .

```xml
<PropertyGroup>
  <TargetFramework>netstandard1.3</TargetFramework>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

## <a name="package-properties"></a>Propriedades do pacote

Você pode especificar propriedades como `PackageId` ,, `PackageVersion` , `PackageIcon` `Title` e `Description` para descrever o pacote que é criado a partir do seu projeto. Para obter informações sobre essas e outras propriedades, consulte [pacote de destino](/nuget/reference/msbuild-targets#pack-target).

```xml
<PropertyGroup>
  ...
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>John Doe</Authors>
  <Company>Contoso</Company>
</PropertyGroup>
```

## <a name="publish-properties-items-and-metadata"></a>Publicar Propriedades, itens e metadados

- [AppendRuntimeIdentifierToOutputPath](#appendruntimeidentifiertooutputpath)
- [AppendTargetFrameworkToOutputPath](#appendtargetframeworktooutputpath)
- [CopyLocalLockFileAssemblies](#copylocallockfileassemblies)
- [CopyToPublishDirectory](#copytopublishdirectory)
- [LinkBase](#linkbase)
- [PreserveCompilationContext](#preservecompilationcontext)
- [PreserveCompilationReferences](#preservecompilationreferences)
- [RuntimeIdentifier](#runtimeidentifier)
- [RuntimeIdentifiers](#runtimeidentifiers)
- [TrimmerRootAssembly](#trimmerrootassembly)
- [UseAppHost](#useapphost)

### <a name="copytopublishdirectory"></a>CopyToPublishDirectory

Os `CopyToPublishDirectory` metadados em um item do MSBuild controlam quando o item é copiado para o diretório de publicação. Os valores permitidos são `PreserveNewest` , que só copia o item se ele tiver mudado, `Always` , que sempre copia o item e `Never` , que nunca copia o item. Do ponto de vista do desempenho, `PreserveNewest` é preferível porque permite uma compilação incremental.

```xml
<ItemGroup>
  <None Update="appsettings.Development.json" CopyToOutputDirectory="PreserveNewest" CopyToPublishDirectory="PreserveNewest" />
</ItemGroup>
```

### <a name="linkbase"></a>LinkBase

Para um item que está fora do diretório do projeto e seus subdiretórios, o destino de publicação usa os [metadados de link](/visualstudio/msbuild/common-msbuild-item-metadata) do item para determinar para onde copiar o item. `Link` também determina como os itens fora da árvore do projeto são exibidos na janela de Gerenciador de Soluções do Visual Studio.

Se `Link` não for especificado para um item que está fora do cone do projeto, o padrão será `%(LinkBase)\%(RecursiveDir)%(Filename)%(Extension)` . `LinkBase` permite especificar uma pasta base sensata para itens fora do cone do projeto. A hierarquia de pastas sob a pasta base é preservada via `RecursiveDir` . Se `LinkBase` não for especificado, ele será omitido do `Link` caminho.

```xml
<ItemGroup>
  <Content Include="..\Extras\**\*.cs" LinkBase="Shared"/>
</ItemGroup>
```

A imagem a seguir mostra como um arquivo incluído por meio do item glob anterior é `Include` exibido em Gerenciador de soluções.

:::image type="content" source="media/solution-explorer-linkbase.png" alt-text="Gerenciador de Soluções mostrando o item com metadados de LinkBase.":::

### <a name="appendtargetframeworktooutputpath"></a>AppendTargetFrameworkToOutputPath

A `AppendTargetFrameworkToOutputPath` propriedade controla se o [moniker da estrutura de destino (TFM)](../../standard/frameworks.md) é anexado ao caminho de saída (que é definido por [OutputPath](/visualstudio/msbuild/common-msbuild-project-properties#list-of-common-properties-and-parameters)). O SDK do .NET acrescenta automaticamente a estrutura de destino e, se presente, o identificador de tempo de execução ao caminho de saída. `AppendTargetFrameworkToOutputPath`A configuração para `false` impede que o TFM seja anexado ao caminho de saída. No entanto, sem o TFM no caminho de saída, vários artefatos de compilação podem substituir um ao outro.

Por exemplo, para um aplicativo .NET 5,0, o caminho de saída muda de `bin\Debug\net5.0` para `bin\Debug` com a seguinte configuração:

```xml
<PropertyGroup>
  <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
</PropertyGroup>
```

### <a name="appendruntimeidentifiertooutputpath"></a>AppendRuntimeIdentifierToOutputPath

A `AppendRuntimeIdentifierToOutputPath` propriedade controla se o [RID (identificador de tempo de execução)](../rid-catalog.md) é anexado ao caminho de saída. O SDK do .NET acrescenta automaticamente a estrutura de destino e, se presente, o identificador de tempo de execução ao caminho de saída. `AppendRuntimeIdentifierToOutputPath`A configuração para `false` impede que o RID seja anexado ao caminho de saída.

Por exemplo, para um aplicativo .NET 5,0 e um RID do `win10-x64` , o caminho de saída muda de `bin\Debug\net5.0\win10-x64` para `bin\Debug\net5.0` com a seguinte configuração:

```xml
<PropertyGroup>
  <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
</PropertyGroup>
```

### <a name="copylocallockfileassemblies"></a>CopyLocalLockFileAssemblies

A `CopyLocalLockFileAssemblies` propriedade é útil para projetos de plug-in que têm dependências em outras bibliotecas. Se você definir essa propriedade como `true` , todas as dependências de pacote NuGet serão copiadas para o diretório de saída. Isso significa que você pode usar a saída de `dotnet build` para executar o plug-in em qualquer computador.

```xml
<PropertyGroup>
  <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
</PropertyGroup>
```

> [!TIP]
> Como alternativa, você pode usar `dotnet publish` para publicar a biblioteca de classes. Para obter mais informações, consulte [dotnet Publish](../tools/dotnet-publish.md).

### <a name="preservecompilationcontext"></a>PreserveCompilationContext

A `PreserveCompilationContext` propriedade permite que um aplicativo compilado ou publicado compile mais código em tempo de execução usando as mesmas configurações que foram usadas no momento da compilação. Os assemblies referenciados no momento da compilação serão copiados para o subdiretório de *referência* do diretório de saída. Os nomes dos assemblies de referência são armazenados na.deps.jsdo aplicativo *no* arquivo, juntamente com as opções passadas para o compilador. Você pode recuperar essas informações usando as <xref:Microsoft.Extensions.DependencyModel.DependencyContext.CompileLibraries?displayProperty=nameWithType> <xref:Microsoft.Extensions.DependencyModel.DependencyContext.CompilationOptions?displayProperty=nameWithType> Propriedades e.

Essa funcionalidade é basicamente usada internamente pelas páginas ASP.NET Core MVC e Razor para dar suporte à compilação em tempo de execução de arquivos Razor.

```xml
<PropertyGroup>
  <PreserveCompilationContext>true</PreserveCompilationContext>
</PropertyGroup>
```

### <a name="preservecompilationreferences"></a>PreserveCompilationReferences

A `PreserveCompilationReferences` propriedade é semelhante à propriedade [PreserveCompilationContext](#preservecompilationcontext) , exceto que ela apenas copia os assemblies referenciados para o diretório de publicação, e não o *.deps.jsno* arquivo.

```xml
<PropertyGroup>
  <PreserveCompilationReferences>true</PreserveCompilationReferences>
</PropertyGroup>
```

Para obter mais informações, consulte [Propriedades do SDK do Razor](/aspnet/core/razor-pages/sdk#properties).

### <a name="runtimeidentifier"></a>RuntimeIdentifier

A `RuntimeIdentifier` propriedade permite que você especifique um único [identificador de tempo de execução (RID)](../rid-catalog.md) para o projeto. O RID permite a publicação de uma implantação autossuficiente.

```xml
<PropertyGroup>
  <RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
</PropertyGroup>
```

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers

A `RuntimeIdentifiers` propriedade permite que você especifique uma lista delimitada por ponto-e-vírgula de [RIDs (identificadores de tempo de execução)](../rid-catalog.md) para o projeto. Use essa propriedade se você precisar publicar para vários tempos de execução. `RuntimeIdentifiers` é usado no momento da restauração para garantir que os ativos corretos estejam no grafo.

> [!TIP]
> `RuntimeIdentifier` (singular) pode fornecer compilações mais rápidas quando apenas um único tempo de execução é necessário.

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="trimmerrootassembly"></a>TrimmerRootAssembly

O `TrimmerRootAssembly` Item permite que você exclua um assembly de [*corte*](../deploying/trim-self-contained.md). O corte é o processo de remover partes não usadas do tempo de execução de um aplicativo empacotado. Em alguns casos, a remoção pode remover incorretamente as referências necessárias.

O XML a seguir exclui o `System.Security` assembly de corte.

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="useapphost"></a>UseAppHost

A `UseAppHost` propriedade controla se um executável nativo é criado para uma implantação ou não. Um executável nativo é necessário para implantações independentes.

No .NET Core 3,0 e versões posteriores, um executável dependente da estrutura é criado por padrão. Defina a `UseAppHost` propriedade como `false` para desabilitar a geração do executável.

```xml
<PropertyGroup>
  <UseAppHost>false</UseAppHost>
</PropertyGroup>
```

Para obter mais informações sobre a implantação, consulte [implantação de aplicativos .net](../deploying/index.md).

## <a name="compile-properties"></a>Compilar propriedades

- [EmbeddedResourceUseDependentUponConvention](#embeddedresourceusedependentuponconvention)
- [LangVersion](#langversion)

### <a name="embeddedresourceusedependentuponconvention"></a>EmbeddedResourceUseDependentUponConvention

A `EmbeddedResourceUseDependentUponConvention` propriedade define se os nomes de arquivo de manifesto de recurso são gerados a partir de informações de tipo em arquivos de origem que são colocados com arquivos de recursos. Por exemplo, se *Form1. resx* estiver na mesma pasta que *Form1.cs* e `EmbeddedResourceUseDependentUponConvention` for definido como `true` , o arquivo *. Resources* gerado usará seu nome do primeiro tipo definido em *Form1.cs*. Por exemplo, se `MyNamespace.Form1` for o primeiro tipo definido em *Form1.cs*, o nome de arquivo gerado *será MyNamespace. Form1. Resources*.

> [!NOTE]
> Se `LogicalName` `ManifestResourceName` os metadados,, ou `DependentUpon` forem especificados para um `EmbeddedResource` Item, o nome do arquivo de manifesto gerado para esse arquivo de recurso será baseado nesses metadados em vez disso.

Por padrão, em um novo projeto .NET, essa propriedade é definida como `true` . Se for definido como `false` , e não `LogicalName` , ou os `ManifestResourceName` `DependentUpon` metadados forem especificados para o `EmbeddedResource` item no arquivo de projeto, o nome do arquivo de manifesto de recurso será baseado no namespace raiz do projeto e no caminho de arquivo relativo para o arquivo *. resx* . Para obter mais informações, consulte [como os arquivos de manifesto de recurso são nomeados](../resources/manifest-file-names.md).

```xml
<PropertyGroup>
  <EmbeddedResourceUseDependentUponConvention>true</EmbeddedResourceUseDependentUponConvention>
</PropertyGroup>
```

### <a name="langversion"></a>LangVersion

A `LangVersion` propriedade permite especificar uma versão de linguagem de programação específica. Por exemplo, se você quiser acessar os recursos do C# Preview, defina `LangVersion` como `preview` .

```xml
<PropertyGroup>
  <LangVersion>preview</LangVersion>
</PropertyGroup>
```

Para obter mais informações, consulte [controle de versão da linguagem C#](../../csharp/language-reference/configure-language-version.md#override-a-default).

## <a name="default-item-inclusion-properties"></a>Propriedades de inclusão de item padrão

- [DefaultExcludesInProjectFolder](#defaultexcludesinprojectfolder)
- [DefaultItemExcludes](#defaultitemexcludes)
- [EnableDefaultCompileItems](#enabledefaultcompileitems)
- [EnableDefaultEmbeddedResourceItems](#enabledefaultembeddedresourceitems)
- [EnableDefaultItems](#enabledefaultitems)
- [EnableDefaultNoneItems](#enabledefaultnoneitems)

Para obter mais informações, consulte [inclusões e exclusões padrão](overview.md#default-includes-and-excludes).

### <a name="defaultitemexcludes"></a>DefaultItemExcludes

Use a `DefaultItemExcludes` propriedade para definir padrões de glob para arquivos e pastas que devem ser excluídos do globs de inclusão, exclusão e remoção. Por padrão, as pastas *./bin* e *./obj* são excluídas dos padrões de glob.

```xml
<PropertyGroup>
  <DefaultItemExcludes>$(DefaultItemExcludes);**/*.myextension</DefaultItemExcludes>
</PropertyGroup>
```

### <a name="defaultexcludesinprojectfolder"></a>DefaultExcludesInProjectFolder

Use a `DefaultExcludesInProjectFolder` propriedade para definir padrões de glob para arquivos e pastas na pasta do projeto que deve ser excluída da inclusão, exclusão e remoção de globs. Por padrão, as pastas que começam com um ponto ( `.` ), como *. git* e *. vs*, são excluídas dos padrões de glob.

Essa propriedade é muito semelhante à `DefaultItemExcludes` propriedade, exceto pelo fato de que ela só considera arquivos e pastas na pasta do projeto. Quando um padrão glob não corresponde intencionalmente a itens fora da pasta do projeto com um caminho relativo, use a `DefaultExcludesInProjectFolder` propriedade em vez da `DefaultItemExcludes` propriedade.

```xml
<PropertyGroup>
  <DefaultExcludesInProjectFolder>$(DefaultExcludesInProjectFolder);**/myprefix*/**</DefaultExcludesInProjectFolder>
</PropertyGroup>
```

### <a name="enabledefaultitems"></a>EnableDefaultItems

A `EnableDefaultItems` propriedade controla se os itens de compilação, itens de recursos inseridos e `None` itens são incluídos implicitamente no projeto. O valor padrão é `true`. Defina a `EnableDefaultItems` propriedade como `false` para desabilitar toda a inclusão de arquivo implícita.

```xml
<PropertyGroup>
  <EnableDefaultItems>false</EnableDefaultItems>
</PropertyGroup>
```

### <a name="enabledefaultcompileitems"></a>EnableDefaultCompileItems

A `EnableDefaultCompileItems` propriedade controla se os itens de compilação são incluídos implicitamente no projeto. O valor padrão é `true`. Defina a `EnableDefaultCompileItems` propriedade como `false` para desabilitar a inclusão implícita de *. cs e outros arquivos de extensão de idioma.

```xml
<PropertyGroup>
  <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```

### <a name="enabledefaultembeddedresourceitems"></a>EnableDefaultEmbeddedResourceItems

A `EnableDefaultEmbeddedResourceItems` propriedade controla se os itens de recurso incorporados estão implicitamente incluídos no projeto. O valor padrão é `true`. Defina a `EnableDefaultEmbeddedResourceItems` propriedade como `false` para desabilitar a inclusão implícita de arquivos de recursos inseridos.

```xml
<PropertyGroup>
  <EnableDefaultEmbeddedResourceItems>false</EnableDefaultEmbeddedResourceItems>
</PropertyGroup>
```

### <a name="enabledefaultnoneitems"></a>EnableDefaultNoneItems

A `EnableDefaultNoneItems` propriedade controla se os `None` itens (arquivos que não têm nenhuma função no processo de compilação) são incluídos implicitamente no projeto. O valor padrão é `true`. Defina a `EnableDefaultNoneItems` propriedade como `false` para desabilitar a inclusão implícita de `None` itens.

```xml
<PropertyGroup>
  <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
</PropertyGroup>
```

## <a name="code-analysis-properties"></a>Propriedades de análise de código

- [AnalysisLevel](#analysislevel)
- [Analysismode](#analysismode)
- [CodeAnalysisTreatWarningsAsErrors](#codeanalysistreatwarningsaserrors)
- [EnableNETAnalyzers](#enablenetanalyzers)
- [EnforceCodeStyleInBuild](#enforcecodestyleinbuild)

### <a name="analysislevel"></a>AnalysisLevel

A `AnalysisLevel` propriedade permite que você especifique um nível de análise de código. Por exemplo, se você quiser acessar analisadores de código de visualização, defina `AnalysisLevel` como `preview` .

Valor padrão:

- Se o projeto tiver como alvo o .NET 5,0 ou posterior, ou se você tiver adicionado a propriedade [analysismode](#analysismode) , o valor padrão será `latest` .
- Caso contrário, essa propriedade será omitida a menos que você a adicione explicitamente ao arquivo de projeto.

```xml
<PropertyGroup>
  <AnalysisLevel>preview</AnalysisLevel>
</PropertyGroup>
```

A tabela a seguir mostra as opções disponíveis.

| Valor | Significado |
|-|-|
| `latest` | Os analisadores de código mais recentes que foram lançados são usados. Este é o padrão. |
| `preview` | Os analisadores de código mais recentes são usados, mesmo se estiverem em versão prévia. |
| `5.0` | O conjunto de regras que foi habilitado para a versão 5,0 do .NET é usado, mesmo se as regras mais recentes estiverem disponíveis. |
| `5` | O conjunto de regras que foi habilitado para a versão 5,0 do .NET é usado, mesmo se as regras mais recentes estiverem disponíveis. |

> [!NOTE]
> Essa propriedade não tem efeito sobre a análise de código em projetos que não fazem referência a um [SDK de projeto](overview.md), por exemplo, projetos herdados .NET Framework que fazem referência ao pacote NuGet Microsoft. CodeAnalysis. netanalyzers.

### <a name="analysismode"></a>Analysismode

A partir do .NET 5,0, o SDK do .NET é fornecido com todas as [regras de qualidade de código "CA"](../../fundamentals/code-analysis/quality-rules/index.md). Por padrão, somente [algumas regras são habilitadas](../../fundamentals/code-analysis/overview.md#enabled-rules) como avisos de compilação. A `AnalysisMode` propriedade permite que você personalize o conjunto de regras habilitadas por padrão. Você pode alternar para um modo de análise mais agressivo (recusar) ou um modo de análise mais conservador (opcional). Por exemplo, se você quiser habilitar todas as regras por padrão como avisos de compilação, defina o valor como `AllEnabledByDefault` .

```xml
<PropertyGroup>
  <AnalysisMode>AllEnabledByDefault</AnalysisMode>
</PropertyGroup>
```

A tabela a seguir mostra as opções disponíveis.

| Valor | Significado |
|-|-|
| `Default` | Modo padrão, em que determinadas regras são habilitadas como avisos de compilação, determinadas regras são habilitadas como sugestões de IDE do Visual Studio e o restante é desabilitado. |
| `AllEnabledByDefault` | Modo agressivo ou de aceitação, em que todas as regras são habilitadas por padrão como avisos de compilação. Você pode [recusar](../../fundamentals/code-analysis/configuration-options.md) seletivamente as regras individuais para desabilitá-las. |
| `AllDisabledByDefault` | Modo conservador ou opt, onde todas as regras estão desabilitadas por padrão. Você pode [optar](../../fundamentals/code-analysis/configuration-options.md) seletivamente por regras individuais para habilitá-las. |

> [!NOTE]
> Essa propriedade não tem efeito sobre a análise de código em projetos que não fazem referência a um [SDK de projeto](overview.md), por exemplo, projetos herdados .NET Framework que fazem referência ao pacote NuGet Microsoft. CodeAnalysis. netanalyzers.

### <a name="codeanalysistreatwarningsaserrors"></a>CodeAnalysisTreatWarningsAsErrors

A `CodeAnalysisTreatWarningsAsErrors` propriedade permite que você configure se os avisos de análise de qualidade de código (CAxxxx) devem ser tratados como avisos e interromper a compilação. Se você usar o `-warnaserror` sinalizador ao compilar seus projetos, os avisos de [análise de qualidade de código do .net](../../fundamentals/code-analysis/overview.md#code-quality-analysis) também serão tratados como erros. Se você não quiser que os avisos de análise de qualidade de código sejam tratados como erros, você poderá definir a `CodeAnalysisTreatWarningsAsErrors` Propriedade do MSBuild como `false` em seu arquivo de projeto.

```xml
<PropertyGroup>
  <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
</PropertyGroup>
```

### <a name="enablenetanalyzers"></a>EnableNETAnalyzers

A [análise de qualidade de código .net](../../fundamentals/code-analysis/overview.md#code-quality-analysis) está habilitada, por padrão, para projetos direcionados ao .NET 5,0 ou posterior. Você pode habilitar a análise de código do .NET para projetos em estilo SDK destinados a versões anteriores do .NET, definindo a `EnableNETAnalyzers` propriedade como `true` . Para desabilitar a análise de código em qualquer projeto, defina essa propriedade como `false` .

```xml
<PropertyGroup>
  <EnableNETAnalyzers>true</EnableNETAnalyzers>
</PropertyGroup>
```

### <a name="enforcecodestyleinbuild"></a>EnforceCodeStyleInBuild

> [!NOTE]
> Este recurso está experimental no momento e pode ser alterado entre as versões do .NET 5 e do .NET 6.

A [análise de estilo de código .net](../../fundamentals/code-analysis/overview.md#code-style-analysis) está desabilitada, por padrão, na compilação para todos os projetos .net. Você pode habilitar a análise de estilo de código para projetos .NET definindo a `EnforceCodeStyleInBuild` propriedade como `true` .

```xml
<PropertyGroup>
  <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
</PropertyGroup>
```

Todas as regras de estilo de código [configuradas](../../fundamentals/code-analysis/overview.md#code-style-analysis) para serem avisos ou erros serão executadas em violações de compilação e relatório.

## <a name="run-time-configuration-properties"></a>Propriedades de configuração de tempo de execução

Você pode configurar alguns comportamentos de tempo de execução especificando as propriedades do MSBuild no arquivo de projeto do aplicativo. Para obter informações sobre outras maneiras de configurar o comportamento de tempo de execução, consulte [definições de configuração de tempo de execução](../run-time-config/index.md).

- [ConcurrentGarbageCollection](#concurrentgarbagecollection)
- [InvariantGlobalization](#invariantglobalization)
- [RetainVMGarbageCollection](#retainvmgarbagecollection)
- [ServerGarbageCollection](#servergarbagecollection)
- [ThreadPoolMaxThreads](#threadpoolmaxthreads)
- [ThreadPoolMinThreads](#threadpoolminthreads)
- [TieredCompilation](#tieredcompilation)
- [TieredCompilationQuickJit](#tieredcompilationquickjit)
- [TieredCompilationQuickJitForLoops](#tieredcompilationquickjitforloops)

### <a name="concurrentgarbagecollection"></a>ConcurrentGarbageCollection

A `ConcurrentGarbageCollection` propriedade define se a [coleta de lixo em segundo plano (simultânea)](../../standard/garbage-collection/background-gc.md) está habilitada. Defina o valor como `false` para desabilitar a coleta de lixo em segundo plano. Para obter mais informações, consulte [background GC](../run-time-config/garbage-collector.md#background-gc).

```xml
<PropertyGroup>
  <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
</PropertyGroup>
```

### <a name="invariantglobalization"></a>InvariantGlobalization

A `InvariantGlobalization` propriedade define se o aplicativo é executado no modo *invariável-globalização* , o que significa que ele não tem acesso a dados específicos de cultura. Defina o valor a `true` ser executado no modo invariável-Globally. Para obter mais informações, consulte [modo invariável](../run-time-config/globalization.md#invariant-mode).

```xml
<PropertyGroup>
  <InvariantGlobalization>true</InvariantGlobalization>
</PropertyGroup>
```

### <a name="retainvmgarbagecollection"></a>RetainVMGarbageCollection

A `RetainVMGarbageCollection` Propriedade configura o coletor de lixo para colocar os segmentos de memória excluídos em uma lista em espera para uso futuro ou liberá-los. Definir o valor para `true` instruir o coletor de lixo a colocar os segmentos em uma lista de espera. Para obter mais informações, consulte [reter VM](../run-time-config/garbage-collector.md#retain-vm).

```xml
<PropertyGroup>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
</PropertyGroup>
```

### <a name="servergarbagecollection"></a>ServerGarbageCollection

A `ServerGarbageCollection` propriedade define se o aplicativo usa a coleta de lixo da [estação de trabalho ou a coleta de lixo do servidor](../../standard/garbage-collection/workstation-server-gc.md). Defina o valor como para `true` usar a coleta de lixo do servidor. Para obter mais informações, consulte [estação de trabalho versus servidor](../run-time-config/garbage-collector.md#workstation-vs-server).

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

### <a name="threadpoolmaxthreads"></a>ThreadPoolMaxThreads

A `ThreadPoolMaxThreads` Propriedade configura o número máximo de threads para o pool de threads de trabalho. Para obter mais informações, consulte [Maximum threads](../run-time-config/threading.md#maximum-threads).

```xml
<PropertyGroup>
  <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
</PropertyGroup>
```

### <a name="threadpoolminthreads"></a>ThreadPoolMinThreads

A `ThreadPoolMinThreads` Propriedade configura o número mínimo de threads para o pool de threads de trabalho. Para obter mais informações, consulte [mínimo de threads](../run-time-config/threading.md#minimum-threads).

```xml
<PropertyGroup>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
</PropertyGroup>
```

### <a name="tieredcompilation"></a>TieredCompilation

A `TieredCompilation` propriedade define se o compilador JIT (just-in-time) usa compilação em [camadas](../whats-new/dotnet-core-3-0.md#tiered-compilation). Defina o valor como `false` para desabilitar a compilação em camadas. Para obter mais informações, consulte [compilação em camadas](../run-time-config/compilation.md#tiered-compilation).

```xml
<PropertyGroup>
  <TieredCompilation>false</TieredCompilation>
</PropertyGroup>
```

### <a name="tieredcompilationquickjit"></a>TieredCompilationQuickJit

A `TieredCompilationQuickJit` propriedade define se o compilador JIT usa o JIT rápido. Defina o valor como `false` para desabilitar o JIT rápido. Para obter mais informações, consulte [Quick JIT](../run-time-config/compilation.md#quick-jit).

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>false</TieredCompilationQuickJit>
</PropertyGroup>
```

### <a name="tieredcompilationquickjitforloops"></a>TieredCompilationQuickJitForLoops

A `TieredCompilationQuickJitForLoops` propriedade define se o compilador JIT usa o JIT rápido em métodos que contêm loops. Defina o valor como `true` para habilitar o JIT rápido em métodos que contêm loops. Para obter mais informações, consulte [Quick JIT for loops](../run-time-config/compilation.md#quick-jit-for-loops).

```xml
<PropertyGroup>
  <TieredCompilationQuickJitForLoops>true</TieredCompilationQuickJitForLoops>
</PropertyGroup>
```

## <a name="reference-properties-and-items"></a>Propriedades e itens de referência

- [AssetTargetFallback](#assettargetfallback)
- [DisableImplicitFrameworkReferences](#disableimplicitframeworkreferences)
- [PackageReference](#packagereference)
- [ProjectReference](#projectreference)
- [Referência](#reference)
- [Propriedades relacionadas a restauração](#restore-related-properties)

### <a name="assettargetfallback"></a>AssetTargetFallback

A `AssetTargetFallback` propriedade permite que você especifique versões de estrutura compatíveis adicionais para referências de projeto e pacotes NuGet. Por exemplo, se você especificar uma dependência de pacote usando `PackageReference` , mas esse pacote não contiver ativos que são compatíveis com seus projetos `TargetFramework` , a `AssetTargetFallback` Propriedade entrará em cena. A compatibilidade do pacote referenciado é verificada novamente usando cada estrutura de destino especificada em `AssetTargetFallback` . Essa propriedade substitui a propriedade preterida `PackageTargetFallback` .

Você pode definir a `AssetTargetFallback` propriedade para uma ou mais [versões da estrutura de destino](../../standard/frameworks.md#supported-target-frameworks).

```xml
<PropertyGroup>
  <AssetTargetFallback>net461</AssetTargetFallback>
</PropertyGroup>
```

### <a name="disableimplicitframeworkreferences"></a>DisableImplicitFrameworkReferences

A `DisableImplicitFrameworkReferences` propriedade controla itens implícitos `FrameworkReference` ao direcionar o .net Core 3,0 e versões posteriores. Ao direcionar o .NET Core 2,1 ou .NET Standard 2,0 e versões anteriores, ele controla os itens [PackageReference](#packagereference) implícitos em pacotes em um metapacote. (Um metapacote é um pacote baseado em estrutura que consiste apenas em dependências em outros pacotes.) Essa propriedade também controla referências implícitas, como `System` e `System.Core` ao direcionamento de .NET Framework.

Defina essa propriedade como `true` para Desabilitar itens implícitos `FrameworkReference` ou [PackageReference](#packagereference) . Se você definir essa propriedade como `true` , poderá adicionar referências explícitas apenas às estruturas ou aos pacotes necessários.

```xml
<PropertyGroup>
  <DisableImplicitFrameworkReferences>true</DisableImplicitFrameworkReferences>
</PropertyGroup>
```

### <a name="packagereference"></a>PackageReference

O `PackageReference` Item define uma referência a um pacote NuGet.

O atributo `Include` especifica a ID do pacote. O `Version` atributo especifica a versão ou o intervalo de versão. Para obter informações sobre como especificar uma versão mínima, a versão máxima, o intervalo ou a correspondência exata, consulte [intervalos de versão](/nuget/concepts/package-versioning#version-ranges). Você também pode adicionar [atributos de ativo](#asset-attributes) a uma referência de pacote.

O trecho do arquivo de projeto no exemplo a seguir faz referência ao pacote [System. Runtime](https://www.nuget.org/packages/System.Runtime/) .

```xml
<ItemGroup>
  <PackageReference Include="System.Runtime" Version="4.3.0" />
</ItemGroup>
```

Para obter mais informações, consulte [referências de pacote em arquivos de projeto](/nuget/consume-packages/package-references-in-project-files).

#### <a name="asset-attributes"></a>Atributos de ativo

Os `IncludeAssets` `ExcludeAssets` metadados, e `PrivateAssets` podem ser adicionados a uma referência de pacote.

| Atributo | Descrição |
| - | - |
| `IncludeAssets` | Especifica quais ativos pertencentes ao pacote especificado por `<PackageReference>` devem ser consumidos. Por padrão, todos os ativos de pacote estão incluídos. |
| `ExcludeAssets`| Especifica quais ativos pertencentes ao pacote especificado por `<PackageReference>` não devem ser consumidos. |
| `PrivateAssets` | Especifica quais ativos pertencentes ao pacote especificado por `<PackageReference>` devem ser consumidos, mas não fluir para o próximo projeto. Os `Analyzers` `Build` ativos, e `ContentFiles` são privados por padrão quando esse atributo não está presente. |

Esses atributos podem conter um ou mais dos seguintes itens, separados por um ponto e vírgula, `;` se houver mais de um listado:

- `Compile` – o conteúdo da pasta *lib* está disponível para a compilação.
- `Runtime` – o conteúdo da pasta de *tempo de execução* é distribuído.
- `ContentFiles` – o conteúdo da pasta *contentfiles* é usado.
- `Build` – as props/destinos na pasta *Build* são usados.
- `Native` – o conteúdo de ativos nativos é copiado para a pasta de *saída* para tempo de execução.
- `Analyzers` – os analisadores são usados.

Como alternativa, o atributo pode conter:

- `None` – nenhum dos ativos é usado.
- `All` – todos os ativos são usados.

### <a name="projectreference"></a>ProjectReference

O `ProjectReference` Item define uma referência a outro projeto. O projeto referenciado é adicionado como uma dependência de pacote NuGet, ou seja, é tratado da mesma forma que um `PackageReference` .

O `Include` atributo especifica o caminho para o projeto. Você também pode adicionar os seguintes metadados a uma referência de projeto: `IncludeAssets` , `ExcludeAssets` e `PrivateAssets` .

O trecho do arquivo de projeto no exemplo a seguir faz referência a um projeto chamado `Project2` .

```xml
<ItemGroup>
  <ProjectReference Include="..\Project2.csproj" />
</ItemGroup>
```

### <a name="reference"></a>Referência

O `Reference` Item define uma referência a um arquivo de assembly.

O `Include` atributo especifica o nome do arquivo e os `HintPath` metadados especificam o caminho para o assembly.

```xml
<ItemGroup>
  <Reference Include="MyAssembly">
    <HintPath>..\..\Assemblies\MyAssembly.dll</HintPath>
  </Reference>
</ItemGroup>
```

### <a name="restore-related-properties"></a>Propriedades relacionadas a restauração

A restauração de um pacote referenciado instala todas as suas dependências diretas e todas as dependências dessas dependências. Você pode personalizar a restauração do pacote especificando propriedades como `RestorePackagesPath` e `RestoreIgnoreFailedSources` . Para obter mais informações sobre essas e outras propriedades, consulte [Restore Target](/nuget/reference/msbuild-targets#restore-target).

```xml
<PropertyGroup>
  <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

## <a name="run-properties"></a>Propriedades da execução

As propriedades a seguir são usadas para iniciar um aplicativo com o [`dotnet run`](../tools/dotnet-run.md) comando:

- [RunArguments](#runarguments)
- [RunWorkingDirectory](#runworkingdirectory)

### <a name="runarguments"></a>RunArguments

A `RunArguments` propriedade define os argumentos que são passados para o aplicativo quando ele é executado.

```xml
<PropertyGroup>
  <RunArguments>-mode dryrun</RunArguments>
</PropertyGroup>
```

> [!TIP]
> Você pode especificar argumentos adicionais a serem passados para o aplicativo usando a [ `--` opção para `dotnet run` ](../tools/dotnet-run.md#options).

### <a name="runworkingdirectory"></a>RunWorkingDirectory

A `RunWorkingDirectory` propriedade define o diretório de trabalho no qual o processo do aplicativo será iniciado. Pode ser um caminho absoluto ou um caminho relativo ao diretório do projeto. Se você não especificar um diretório, `OutDir` será usado como o diretório de trabalho.

```xml
<PropertyGroup>
  <RunWorkingDirectory>c:\temp</RunWorkingDirectory>
</PropertyGroup>
```

## <a name="hosting-properties"></a>Propriedades de hospedagem

- [EnableComHosting](#enablecomhosting)
- [EnableDynamicLoading](#enabledynamicloading)

### <a name="enablecomhosting"></a>EnableComHosting

A `EnableComHosting` propriedade indica que um assembly fornece um servidor com. Definir o `EnableComHosting` como `true` também implica que [EnableDynamicLoading](#enabledynamicloading) é `true` .

```xml
<PropertyGroup>
  <EnableComHosting>True</EnableComHosting>
</PropertyGroup>
```

Para obter mais informações, consulte [expor componentes .net ao com](../native-interop/expose-components-to-com.md).

### <a name="enabledynamicloading"></a>EnableDynamicLoading

A `EnableDynamicLoading` propriedade indica que um assembly é um componente carregado dinamicamente. O componente pode ser uma [biblioteca com](/windows/win32/com/the-component-object-model) ou uma biblioteca não com que pode ser [usada em um host nativo](../tutorials/netcore-hosting.md). Definir essa propriedade como `true` tem os seguintes efeitos:

- Um *.runtimeconfig.jsno* arquivo é gerado.
- [Roll forward](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward) é definido como `LatestMinor` .
- As referências do NuGet são copiadas localmente.

```xml
<PropertyGroup>
  <EnableDynamicLoading>true</EnableDynamicLoading>
</PropertyGroup>
```

## <a name="see-also"></a>Consulte também

- [Referência de esquema do MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [Propriedades comuns do MSBuild](/visualstudio/msbuild/common-msbuild-project-properties)
- [Propriedades do MSBuild para o pacote NuGet](/nuget/reference/msbuild-targets#pack-target)
- [Propriedades do MSBuild para restauração do NuGet](/nuget/reference/msbuild-targets#restore-properties)
- [Personalizar uma compilação](/visualstudio/msbuild/customize-your-build)
