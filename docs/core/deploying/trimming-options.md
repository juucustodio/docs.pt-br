---
title: Opções de corte
description: Saiba como controlar a remoção de aplicativos independentes.
author: sbomer
ms.author: svbomer
ms.date: 08/25/2020
ms.openlocfilehash: 89bd195a97c2f1bbbba9199fea51c917c4e4836b
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89515826"
---
# <a name="trimming-options"></a>Opções de corte

As seguintes propriedades e itens do MSBuild influenciam o comportamento de [implantações autocontidas cortadas](trim-self-contained.md). Algumas das opções mencionam `ILLink` , que é o nome da ferramenta subjacente que implementa a corte. Mais informações sobre a ferramenta subjacente podem ser encontradas na [documentação do vinculador](https://github.com/mono/linker/tree/master/docs).

## <a name="enable-trimming"></a>Habilitar corte

- `<PublishTrimmed>true</PublishTrimmed>`

   Habilitar corte durante a publicação, com as configurações padrão definidas pelo SDK.

Ao usar `Microsoft.NET.Sdk` o, isso executará o corte no nível do assembly dos assemblies do Framework do netcoreapp Runtime Pack. As bibliotecas código do aplicativo e não estrutura não são cortadas. Outros SDKs podem definir padrões diferentes.

## <a name="trimming-granularity"></a>Granularidade de corte

As configurações de granularidade a seguir controlam o quão agressivamente não usado IL é Descartado. Isso pode ser definido como uma propriedade ou como metadados em um [assembly individual](#trimmed-assemblies).

- `<TrimMode>copyused</TrimMode>`

   Habilite o corte em nível de assembly, que manterá um assembly inteiro se qualquer parte dele for usada (de forma estaticamente compreendida).

- `<TrimMode>link</TrimMode>`

    Habilitar corte em nível de membro, que remove Membros não utilizados dos tipos.

Assemblies com `<IsTrimmable>true</IsTrimmable>` metadados, mas nenhum explícito usarão `TrimMode` o global `TrimMode` . O padrão `TrimMode` para `Microsoft.NET.Sdk` é `copyused` .

## <a name="trimmed-assemblies"></a>Assemblies cortados

Ao publicar um aplicativo cortado, o SDK computa um `ItemGroup` chamado `ManagedAssemblyToLink` que representa o conjunto de arquivos a serem processados para corte. `ManagedAssemblyToLink` pode ter metadados que controlam o comportamento de corte por assembly. Para definir esses metadados, crie um destino que seja executado antes do destino interno `PrepareForILLink` . O exemplo a seguir mostra como habilitar o corte de `MyAssembly` .

```xml
<Target Name="ConfigureTrimming"
        BeforeTargets="PrepareForILLink">
  <ItemGroup>
    <ManagedAssemblyToLink Condition="'%(Filename)' == 'MyAssembly'">
      <IsTrimmable>true</IsTrimmable>
    </ManagedAssemblyToLink>
  </ItemGroup>
</Target>
```

Não adicione ou remova itens de/para `ManagedAssemblyToLink` , pois o SDK computa esse conjunto durante a publicação e espera que ele não seja alterado. Os metadados com suporte são:

- `<IsTrimmable>true</IsTrimmable>`

  Controle se o assembly fornecido é cortado.

- `<TrimMode>copyused</TrimMode>` ou `<TrimMode>link</TrimMode>`

  Controle a [granularidade de corte](#trimming-granularity) deste assembly. Isso tem precedência sobre o global `TrimMode` . `TrimMode`A configuração em um assembly implica `<IsTrimmable>true</IsTrimmable>` .

## <a name="root-assemblies"></a>Assemblies raiz

Todos os assemblies que não têm `<IsTrimmable>true</IsTrimmable>` são consideradas raízes para a análise, o que significa que elas e todas as suas dependências estaticamente compreendidas serão mantidas. Assemblies adicionais podem ser "com raiz" por nome (sem a `.dll` extensão):

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="MyAssembly" />
</ItemGroup>
```

## <a name="root-descriptors"></a>Descritores de raiz

Outra maneira de especificar raízes para análise é usando um arquivo XML que usa o formato do [descritor](https://github.com/mono/linker/blob/master/docs/data-formats.md#descriptor-format)do vinculador. Isso permite que você acesse membros específicos da raiz em vez de um assembly inteiro.

```xml
<ItemGroup>
  <TrimmerRootDescriptor Include="MyRoots.xml" />
</ItemGroup>
```

Por exemplo, `MyRoots.xml` pode raiz um método específico que é acessado dinamicamente pelo aplicativo:

```xml
<linker>
  <assembly fullname="MyAssembly">
    <type fullname="MyAssembly.MyClass">
      <method name="DynamicallyAccessedMethod" />
    </type>
  </assembly>
</linker>
```

## <a name="analysis-warnings"></a>Avisos de análise

A remoção removerá o IL que não está acessível estaticamente. Os aplicativos que usam reflexão ou outros padrões que criam dependências dinâmicas podem ser quebrados por corte. Para avisar sobre tais padrões:

- `<SuppressTrimAnalysisWarnings>false</SuppressTrimAnalysisWarnings>`

    Habilitar avisos de análise de corte.

Isso incluirá avisos sobre todo o aplicativo, incluindo seu próprio código, código de biblioteca e código de estrutura.

## <a name="warning-versions"></a>Versões de aviso

A análise de corte respeita a [`AnalysisLevel`](../project-sdk/msbuild-props.md#analysislevel) propriedade que controla a versão dos avisos de análise no SDK. Há outra propriedade que controla a versão dos avisos de análise de corte de forma independente (semelhante a `WarningLevel` para o compilador):

- `<ILLinkWarningLevel>5</ILLinkWarningLevel>`

    Emitir apenas avisos do nível determinado ou inferior. Isso pode ser `9999` incluir todas as versões de aviso.

## <a name="suppressing-warnings"></a>Suprimindo avisos

[Códigos de aviso](https://github.com/mono/linker/blob/master/docs/error-codes.md#warning-codes) individuais podem ser suprimidos usando as propriedades usuais do MSBuild respeitadas pelo ferramentas, incluindo `NoWarn` , `WarningsAsErrors` , `WarningsNotAsErrors` e `TreatWarningsAsErrors` . Há uma opção adicional que controla o comportamento de aviso como erro do ILLink de forma independente:

- `<ILLinkTreatWarningsAsErrors>false</ILLinkTreatWarningsAsErrors>`

    Não trate avisos ILLink como erros. Isso pode ser útil para evitar a desativação de avisos de análise de corte em erros ao tratar avisos do compilador como erros globalmente.

## <a name="removing-symbols"></a>Removendo símbolos

Os símbolos normalmente serão cortados para corresponder aos assemblies cortados. Você também pode remover todos os símbolos:

- `<TrimmerRemoveSymbols>true</TrimmerRemoveSymbols>`

    Remova os símbolos do aplicativo cortado, incluindo PDBs inseridos e arquivos PDB separados. Isso se aplica ao código do aplicativo e a qualquer dependência que venha com símbolos.

O SDK também torna possível desabilitar o suporte do depurador usando a propriedade `DebuggerSupport` . Quando o suporte ao depurador estiver desabilitado, a remoção removerá símbolos automaticamente ( `TrimmerRemoveSymbols` padrão será true).

## <a name="trimming-framework-library-features"></a>Aparando recursos da biblioteca da estrutura

Várias áreas de recursos das bibliotecas de estrutura vêm com diretivas de vinculador que possibilitam a remoção do código para recursos desabilitados.

- `<DebuggerSupport>false</DebuggerSupport>`

    Remover o código que permite melhores experiências de depuração. Isso também [removerá os símbolos](#removing-symbols).

- `<EnableUnsafeBinaryFormatterSerialization>false</EnableUnsafeBinaryFormatterSerialization>`

    Remova o suporte de serialização BinaryFormatter. Para obter mais informações, consulte [métodos de serialização BinaryFormatter são obsoletos](../compatibility/corefx.md#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps).

- `<EnableUnsafeUTF7Encoding>false</EnableUnsafeUTF7Encoding>`

    Remova o código de codificação UTF-7 inseguro. Para obter mais informações, consulte [caminhos de código UTF-7 são obsoletos](../compatibility/corefx.md#utf-7-code-paths-are-obsolete).

- `<EventSourceSupport>false</EventSourceSupport>`

    Remova a lógica ou o código relacionado à EventSource.

- `<HttpActivityPropagationSupport>false</HttpActivityPropagationSupport>`

    Remova o código relacionado ao suporte de diagnóstico para System .net. http.

- `<InvariantGlobalization>true</InvariantGlobalization>`

    Remover dados e código específicos de globalização. Para obter mais informações, consulte [modo invariável](../run-time-config/globalization.md#invariant-mode).

- `<UseSystemResourceKeys>true</UseSystemResourceKeys>`

    Remova as mensagens de exceção de `System.*` assemblies. Quando uma exceção é gerada de um `System.*` assembly, a mensagem será uma ID de recurso simplificada em vez da mensagem completa.

 Essas propriedades farão com que o código relacionado seja cortado e também desabilitará os recursos por meio do arquivo [runtimeconfig](../run-time-config/index.md) . Para obter mais informações sobre essas propriedades, incluindo as opções de runtimeconfig correspondentes, consulte Opções de [recurso](https://github.com/dotnet/runtime/blob/master/docs/workflow/trimming/feature-switches.md). Alguns SDKs podem ter valores padrão para essas propriedades.
