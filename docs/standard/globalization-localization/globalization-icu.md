---
description: 'Saiba mais sobre: .NET Globalization e ICU'
title: Globalização e ICU
ms.date: 05/21/2020
helpviewer_keywords:
- globalization [.NET], about globalization
- global applications, globalization
- international applications [.NET], globalization
- world-ready applications, globalization
- application development [.NET], globalization
- culture, globalization
- icu, icu on windows, ms-icu
ms.openlocfilehash: 9ff6219a06cb05c743089e56b379de1f98bbc42c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99702256"
---
# <a name="net-globalization-and-icu"></a>Globalização e ICU do .NET

No passado, as APIs de globalização do .NET usavam diferentes bibliotecas subjacentes em diferentes plataformas. No UNIX, as APIs usaram os [componentes internacionais para Unicode (ICU)](http://site.icu-project.org/home)e no Windows, eles usaram [NLS (suporte ao idioma nacional)](/windows/win32/intl/national-language-support). Isso resultou em algumas diferenças comportamentais em várias APIs de globalização ao executar aplicativos em diferentes plataformas. As diferenças de comportamento foram evidentes nessas áreas:

- Culturas e dados de cultura
- Maiúsculas e minúsculas
- Classificação e pesquisa de cadeia de caracteres
- Chaves de classificação
- Normalização de cadeia de caracteres
- Suporte a IDNs (nomes de domínio internacionalizados)
- Nome de exibição de fuso horário no Linux

A partir do .NET 5,0, os desenvolvedores têm mais controle sobre qual biblioteca subjacente é usada, permitindo que os aplicativos evitem diferenças entre plataformas.

## <a name="icu-on-windows"></a>ICU no Windows

O Windows 10 pode 2019 atualização e as versões posteriores incluem [icu.dll](/windows/win32/intl/international-components-for-unicode--icu-) como parte do sistema operacional, e o .NET 5,0 e versões posteriores usam o ICU por padrão. Ao executar no Windows, o .NET 5,0 e versões posteriores tentam carregar `icu.dll` e, se estiver disponível, usá-lo para a implementação da globalização. Se a biblioteca ICU não puder ser encontrada ou carregada, como quando executada em versões mais antigas do Windows, o .NET 5,0 e versões posteriores retornem à implementação baseada em NLS.

> [!NOTE]
> Mesmo ao usar o ICU, `CurrentCulture` os `CurrentUICulture` Membros, e `CurrentRegion` ainda usam as APIs do sistema operacional Windows para honrar as configurações do usuário.

### <a name="behavioral-differences"></a>Diferenças de comportamento

Se você atualizar seu aplicativo para o .NET 5 de destino, poderá ver as alterações em seu aplicativo mesmo se não perceber que está usando instalações de globalização. Esta seção lista uma das alterações comportamentais que você pode ver, mas também há outras.

##### <a name="stringindexof"></a>String.IndexOf

Considere o código a seguir que chama <xref:System.String.IndexOf(System.String)?displayProperty=nameWithType> para localizar o índice do caractere de nova linha em uma cadeia de caracteres.

```csharp
string s = "Hello\r\nworld!";
int idx = s.IndexOf("\n");
Console.WriteLine(idx);
```

- Nas versões anteriores do .NET no Windows, o trecho é impresso `6` .
- No .NET 5,0 e versões posteriores no Windows 10 podem ser 2019 atualização e versões posteriores, o trecho de código é impresso `-1` .

Para corrigir esse código realizando uma pesquisa ordinal em vez de uma pesquisa sensível à cultura, chame a <xref:System.String.IndexOf(System.String,System.StringComparison)> sobrecarga e passe <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> como um argumento.

Você pode executar as regras [de análise de código CA1307: especificar StringComparison para clareza](../../../docs/fundamentals/code-analysis/quality-rules/ca1307.md) e [CA1309: Use o ordinal StringComparison](../../../docs/fundamentals/code-analysis/quality-rules/ca1309.md) para encontrar esses sites de chamada em seu código.

Para obter mais informações, consulte [comportamento de alterações ao comparar cadeias de caracteres no .NET 5 +](../base-types/string-comparison-net-5-plus.md).

### <a name="use-nls-instead-of-icu"></a>Usar NLS em vez de ICU

Usar o ICU em vez do NLS pode resultar em diferenças comportamentais com algumas operações relacionadas à globalização. Para reverter para o uso do NLS, um desenvolvedor pode recusar a implementação do ICU. Os aplicativos podem habilitar o modo NLS de qualquer uma das seguintes maneiras:

- No arquivo de projeto:

  ```xml
  <ItemGroup>
    <RuntimeHostConfigurationOption Include="System.Globalization.UseNls" Value="true" />
  </ItemGroup>
  ```

- No arquivo `runtimeconfig.json`:

  ```json
  {
    "runtimeOptions": {
       "configProperties": {
         "System.Globalization.UseNls": true
        }
    }
  }
  ```

- Definindo a variável de ambiente `DOTNET_SYSTEM_GLOBALIZATION_USENLS` para o valor `true` ou `1` .

> [!NOTE]
> Um valor definido no projeto ou no `runtimeconfig.json` arquivo tem precedência sobre a variável de ambiente.

Para obter mais informações, consulte [definições de configuração de tempo de execução](../../core/run-time-config/globalization.md#nls).

## <a name="app-local-icu"></a>ICU de aplicativo local

Cada versão do ICU pode trazer suas correções de bug de ti, bem como dados de CLDR (repositório de dados de localidade comum) que descrevem os idiomas do mundo. A movimentação entre versões do ICU pode afetar sutilmente o comportamento do aplicativo quando se trata de operações relacionadas à globalização. Para ajudar os desenvolvedores de aplicativos a garantir a consistência em todas as implantações, o .NET 5,0 e versões posteriores permitem que os aplicativos no Windows e no UNIX executem e usem sua própria cópia do ICU.

Os aplicativos podem aceitar um modo de implementação do ICU local do aplicativo de qualquer uma das seguintes maneiras:

- No arquivo de projeto:

  ```xml
  <ItemGroup>
    <RuntimeHostConfigurationOption Include="System.Globalization.AppLocalIcu" Value="<suffix>:<version> or <version>" />
  </ItemGroup>
  ```

- No arquivo `runtimeconfig.json`:

  ```json
  {
    "runtimeOptions": {
       "configProperties": {
         "System.Globalization.AppLocalIcu": "<suffix>:<version> or <version>"
       }
    }
  }
  ```

- Definindo a variável de ambiente `DOTNET_SYSTEM_GLOBALIZATION_APPLOCALICU` para o valor `<suffix>:<version>` ou `<version>` .

  `<suffix>`: Sufixo opcional com menos de 36 caracteres de comprimento, seguindo as convenções de empacotamento do ICU público. Ao criar um ICU personalizado, você pode personalizá-lo para produzir os nomes de lib e os nomes de símbolo exportados para conter um sufixo, por exemplo, `libicuucmyapp` , em que `myapp` é o sufixo.

  `<version>`: Uma versão do ICU válida, por exemplo, 67,1. Esta versão é usada para carregar os binários e obter os símbolos exportados.

Para carregar o ICU quando a opção de aplicativo local é definida, o .NET usa o <xref:System.Runtime.InteropServices.NativeLibrary.TryLoad%2A?displayProperty=nameWithType> método, que investiga vários caminhos. O método primeiro tenta localizar a biblioteca na `NATIVE_DLL_SEARCH_DIRECTORIES` propriedade, que é criada pelo host dotnet com base no `deps.json` arquivo para o aplicativo. Para obter mais informações, consulte [investigação padrão](../../core/dependency-loading/default-probing.md).

Para aplicativos independentes, nenhuma ação especial é exigida pelo usuário, a não ser garantir que o ICU esteja no diretório do aplicativo (para aplicativos independentes, o diretório de trabalho usa como padrão `NATIVE_DLL_SEARCH_DIRECTORIES` ).

Se você estiver consumindo o ICU por meio de um pacote NuGet, isso funcionará em aplicativos dependentes da estrutura. O NuGet resolve os ativos nativos e os inclui no `deps.json` arquivo e no diretório de saída para o aplicativo no `runtimes` diretório. O .NET o carrega a partir daí.

Para aplicativos dependentes da estrutura (não independentes) em que o ICU é consumido de uma compilação local, você deve executar etapas adicionais. O SDK do .NET ainda não tem um recurso para binários nativos "flexíveis" a serem incorporados ao `deps.json` (consulte [este problema do SDK](https://github.com/dotnet/sdk/issues/11373)). Em vez disso, você pode habilitar isso adicionando informações adicionais ao arquivo de projeto do aplicativo. Por exemplo:

```xml
<ItemGroup>
  <IcuAssemblies Include="icu\*.so*" />
  <RuntimeTargetsCopyLocalItems Include="@(IcuAssemblies)" AssetType="native" CopyLocal="true" DestinationSubDirectory="runtimes/linux-x64/native/" DestinationSubPath="%(FileName)%(Extension)" RuntimeIdentifier="linux-x64" NuGetPackageId="System.Private.Runtime.UnicodeData" />
</ItemGroup>
```

Isso deve ser feito para todos os binários do ICU para os tempos de execução com suporte. Além disso, os `NuGetPackageId` metadados no `RuntimeTargetsCopyLocalItems` grupo de itens precisam corresponder a um pacote NuGet que o projeto realmente referencia.

### <a name="macos-behavior"></a>comportamento do macOS

`macOS` tem um comportamento diferente para resolver bibliotecas dinâmicas dependentes dos comandos de carregamento especificados no `match-o` arquivo do que o carregador do Linux. No carregador do Linux, o .NET pode tentar `libicudata` , `libicuuc` e `libicui18n` (nessa ordem) para satisfazer o grafo de dependências do ICU. No entanto, no macOS, isso não funciona. Ao criar o ICU no macOS, você, por padrão, obtém uma biblioteca dinâmica com esses comandos de carregamento no `libicuuc` . O trecho a seguir mostra um exemplo.

```sh
~/ % otool -L /Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib
/Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib:
 libicuuc.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 libicudata.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
 /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
```

Esses comandos apenas referenciam o nome das bibliotecas dependentes para os outros componentes do ICU. O carregador executa a pesquisa seguindo as `dlopen` convenções, que envolve ter essas bibliotecas nos diretórios do sistema ou definir os `LD_LIBRARY_PATH` VARs de env ou ter o ICU no diretório de nível de aplicativo. Se você não puder definir `LD_LIBRARY_PATH` ou garantir que os binários ICU estejam no diretório de nível de aplicativo, será necessário fazer um trabalho extra.

Há algumas diretivas para o carregador, como `@loader_path` , que dizem ao carregador para pesquisar essa dependência no mesmo diretório que o binário com esse comando de carregamento. Há duas maneiras de fazer isso:

- `install_name_tool -change`

  Execute os seguintes comandos:

  ```bash
  install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicuuc.67.1.dylib
  install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicui18n.67.1.dylib
  install_name_tool -change "libicuuc.67.dylib" "@loader_path/libicuuc.67.dylib" /path/to/libicui18n.67.1.dylib
  ```

- Patch ICU para produzir os nomes de instalação `@loader_path`

  Antes de executar autoconf ( `./runConfigureICU` ), altere [estas linhas](https://github.com/unicode-org/icu/blob/ef91cc3673d69a5e00407cda94f39fcda3131451/icu4c/source/config/mh-darwin#L32-L37) para:

  ```
  LD_SONAME = -Wl,-compatibility_version -Wl,$(SO_TARGET_VERSION_MAJOR) -Wl,-current_version -Wl,$(SO_TARGET_VERSION) -install_name @loader_path/$(notdir $(MIDDLE_SO_TARGET))
  ```

## <a name="icu-on-webassembly"></a>ICU no Webassembly

Uma versão do ICU está disponível especificamente para cargas de trabalho do Webassembly. Esta versão fornece compatibilidade de globalização com perfis de área de trabalho. Para reduzir o tamanho do arquivo de dados ICU de 24 MB a 1,4 MB (ou ~ 0,3 MB se estiver compactado com Brotli), essa carga de trabalho tem algumas limitações.

Não há suporte para as seguintes APIs:

- <xref:System.Globalization.CultureInfo.EnglishName?displayProperty=nameWithType>
- <xref:System.Globalization.CultureInfo.NativeName?displayProperty=nameWithType>
- <xref:System.Globalization.DateTimeFormatInfo.NativeCalendarName?displayProperty=nameWithType>
- <xref:System.Globalization.RegionInfo.NativeName?displayProperty=nameWithType>

As seguintes APIs têm suporte com limitações:

- <xref:System.String.Normalize(System.Text.NormalizationForm)?displayProperty=nameWithType> e <xref:System.String.IsNormalized(System.Text.NormalizationForm)?displayProperty=nameWithType> não dão suporte às raramente usadas <xref:System.Text.NormalizationForm.FormKC> e <xref:System.Text.NormalizationForm.FormKD> formulários.
- <xref:System.Globalization.RegionInfo.CurrencyNativeName?displayProperty=nameWithType> retorna o mesmo valor que <xref:System.Globalization.RegionInfo.CurrencyEnglishName?displayProperty=nameWithType>.

Além disso, uma lista de localidades com suporte pode ser encontrada no [repositório dotnet/ICU](https://github.com/dotnet/icu/blob/0f49268ddfd3331ca090f1c51d2baa2f75f6c6c0/icu-filters/optimal.json#L6-L54).
