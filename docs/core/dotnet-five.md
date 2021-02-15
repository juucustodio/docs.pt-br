---
title: Novidades do .NET 5
description: Saiba mais sobre o .NET 5, uma plataforma de desenvolvimento de plataforma cruzada e de software livre que é a próxima evolução do .NET Core.
ms.date: 11/30/2020
ms.topic: overview
ms.author: dapine
author: IEvangelist
ms.openlocfilehash: 7984f235044db5dfc7533343e7d43cd7745fba33
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97899450"
---
# <a name="whats-new-in-net-5"></a>Novidades do .NET 5

O .NET 5,0 é a próxima versão principal do .NET Core a seguir 3,1. Nomeamos essa nova versão do .NET 5,0 em vez do .NET Core 4,0 por dois motivos:

- Ignoramos os números de versão 4. x para evitar confusão com .NET Framework 4. x.
- Descartamos "Core" do nome para enfatizar que esta é a principal implementação do .NET em diante. O .NET 5,0 dá suporte a mais tipos de aplicativos e mais plataformas do que o .NET Core ou o .NET Framework.

ASP.NET Core 5,0 é baseado no .NET 5,0, mas mantém o nome "Core" para evitar confusão com o ASP.NET MVC 5. Da mesma forma, Entity Framework Core 5,0 mantém o nome "Core" para evitar confusão com Entity Framework 5 e 6.

O .NET 5,0 inclui os seguintes aprimoramentos e novos recursos em comparação com o .NET Core 3,1:

- [Atualizações em C#](#c-updates)
- [Atualizações de F #](#f-updates)
- [Atualizações de Visual Basic](#visual-basic-updates)
- [System.Text.Jssobre novos recursos](#systemtextjson-new-features)
- [Aplicativos de arquivo único](deploying/single-file.md)
- [Corte de aplicativo](https://devblogs.microsoft.com/dotnet/app-trimming-in-net-5)
- Intrínsecos do Windows ARM64 e ARM64
- Suporte de ferramentas para depuração de despejo
- As bibliotecas de tempo de execução são 80% anotadas para [tipos de referência anuláveis](../csharp/nullable-references.md)
- Aprimoramentos de desempenho:
  - [Coleta de lixo (GC)](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#gc)
  - [System.Text.Json](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#json)
  - [System.Text.RegularExpressions](https://devblogs.microsoft.com/dotnet/regex-performance-improvements-in-net-5)
  - [Pooling ValueTask assíncrona](https://devblogs.microsoft.com/dotnet/async-valuetask-pooling-in-net-5)
  - [Otimizações de tamanho de contêiner](https://github.com/dotnet/dotnet-docker/issues/1814#issuecomment-625294750)
  - [Muito mais áreas](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)

## <a name="net-50-doesnt-replace-net-framework"></a>O .NET 5,0 não substitui .NET Framework

O .NET 5,0 é a principal implementação do .NET no futuro e .NET Framework 4. x ainda tem suporte.

Não há planos de portar as tecnologias a seguir de .NET Framework para o .NET 5,0, mas há alternativas no .NET 5,0:

| Tecnologia            | Alternativa recomendada                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------|
| Web Forms             | ASP.NET Core [mais](/aspnet/core/blazor) ou [Razor Pages](/aspnet/core/tutorials/razor-pages) |
| Windows Workflow (WF) | [CoreWF de código-fonte aberto](https://github.com/UiPath-Open/corewf) ou [Elsa-Workflow](https://github.com/elsa-workflows/elsa-core) |

### <a name="windows-communication-foundation"></a>Windows Communication Foundation

A implementação original do [Windows Communication Foundation (WCF)](../framework/wcf/index.md) era suportada apenas no Windows. No entanto, há uma porta do cliente disponível no .NET Foundation. Ele é totalmente de software livre [, de plataforma](https://github.com/dotnet/wcf)cruzada e tem suporte da Microsoft. Os pacotes principais do NuGet estão listados abaixo:

- [System.ServiceModel.Duplex](https://www.nuget.org/packages/System.ServiceModel.Duplex)
- [System. ServiceModel. Federation](https://www.nuget.org/packages/System.ServiceModel.Federation)
- [System.ServiceModel.Http](https://www.nuget.org/packages/System.ServiceModel.Http)
- [System.ServiceModel.NetTcp](https://www.nuget.org/packages/System.ServiceModel.NetTcp)
- [System.ServiceModel.Primitives](https://www.nuget.org/packages/System.ServiceModel.Primitives)
- [{1&amp;gt;System.ServiceModel.Security&amp;lt;1}](https://www.nuget.org/packages/System.ServiceModel.Security)

A comunidade mantém os componentes de servidor que complementam as bibliotecas de cliente mencionadas anteriormente. O repositório GitHub pode ser encontrado em [CoreWCF](https://github.com/CoreWCF/CoreWCF). Os componentes do servidor _não_ são oficialmente suportados pela Microsoft. Para obter uma alternativa ao WCF, considere [gRPC](/aspnet/core/grpc).

## <a name="net-50-doesnt-replace-net-standard"></a>O .NET 5,0 não substitui .NET Standard

O novo desenvolvimento de aplicativos pode especificar o `net5.0` moniker do Framework de destino (TFM) para todos os tipos de projeto, incluindo bibliotecas de classes. O compartilhamento de código entre as cargas de trabalho do .NET 5 é simplificado, pois tudo o que você precisa é o `net5.0` TFM.

Para aplicativos e bibliotecas do .NET 5,0, o `net5.0` moniker da estrutura de destino (TFM) combina e substitui o `netcoreapp` e o `netstandard` TFMs. No entanto, se você planeja compartilhar o código entre as cargas de trabalho .NET Framework, .NET Core e .NET 5, poderá fazer isso especificando `netstandard2.0` como seu TFM. Para obter mais informações, confira [.NET Standard](../standard/net-standard.md).

## <a name="c-updates"></a>Atualizações em C#

Os desenvolvedores que escrevem aplicativos .NET 5 terão acesso à versão e aos recursos mais recentes do C#. O .NET 5 é emparelhado com o C# 9, que traz muitos recursos novos para a linguagem. Aqui estão alguns destaques:

- Registros: tipos de referência com semântica de igualdade baseada em valor e mutação não destrutiva com suporte por uma nova `with` expressão.
- Correspondência de padrão relacional: estende os recursos de correspondência de padrões para operadores relacionais para avaliações e expressões comparativa, incluindo padrões lógicos – novas palavras-chave `and` , `or` e `not` .
- Instruções de nível superior: como um meio para acelerar a adoção e o aprendizado do C#, o `Main` método pode ser omitido e o aplicativo tão simples quanto o seguinte é válido:

   ```csharp
   System.Console.Write("Hello world!");
   ```

- Ponteiros de função: constructos de linguagem que expõem os seguintes opcodes de linguagem intermediária (IL): `ldftn` e `calli` .

Para obter mais informações sobre os recursos disponíveis do C# 9, consulte [o que há de novo no c# 9](../csharp/whats-new/csharp-9.md).

### <a name="source-generators"></a>Geradores de origem

Além de alguns dos novos recursos do C# destacados, os geradores de origem estão fazendo seu caminho em projetos de desenvolvedor. Os geradores de origem permitem o código que é executado durante a compilação para inspecionar seu programa e produzir arquivos adicionais que são compilados junto com o restante do seu código.

Para obter mais informações sobre geradores de origem, consulte [introdução aos geradores de código](https://devblogs.microsoft.com/dotnet/introducing-c-source-generators) -fonte c# e [exemplos do gerador de código-fonte c#](https://devblogs.microsoft.com/dotnet/new-c-source-generator-samples).

## <a name="f-updates"></a>Atualizações de F #

O f # é a linguagem de programação funcional do .NET e, com o .NET 5, os desenvolvedores têm acesso ao F # 5. Aqui estão vários recursos novos do F # 5:

### <a name="interpolated-strings"></a>Cadeias de caracteres interpoladas

Semelhante à cadeia de caracteres interpolada em C# e até mesmo JavaScript, F # dá suporte à interpolação de cadeia de caracteres básica.

```fsharp
let name = "David"
let age = 36
let message = $"{name} is {age} years old."
```

Além da interpolação de cadeia de caracteres básica, há interpolação de tipo. Com a interpolação digitada, um determinado tipo deve corresponder ao especificador de formato.

```fsharp
let name = "David"
let age = 36
let message = $"%s{name} is %d{age} years old."
```

Isso é semelhante à [`sprintf`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-printfmodule.html#sprintf) função que formata uma cadeia de caracteres com base em entradas de tipo seguro. <!-- For more information, see [What's new in F# 5](fsharp/whats-new/fsharp-50.md). -->

## <a name="visual-basic-updates"></a>Atualizações de Visual Basic

Não há novos recursos de linguagem para Visual Basic no .NET 5. No entanto, com o .NET 5, Visual Basic suporte é estendido para:

| Descrição                            | Parâmetro `dotnet new` |
|----------------------------------------|------------------------|
| Aplicativo do Console                    | `console`              |
| Biblioteca de classes                          | `classlib`             |
| Aplicativo WPF                        | `wpf`                  |
| Biblioteca de classes do WPF                      | `wpflib`               |
| Biblioteca de Controles Personalizados do WPF             | `wpfcustomcontrollib`  |
| Biblioteca de controle de usuário WPF               | `wpfusercontrollib`    |
| Aplicativo Windows Forms (WinForms)   | `winforms`             |
| Biblioteca de classes do Windows Forms (WinForms) | `winformslib`          |
| Projeto de Teste de Unidade                      | `mstest`               |
| Projeto de Teste do NUnit 3                   | `nunit`                |
| Item de Teste do NUnit 3                      | `nunit-test`           |
| Projeto de Teste xUnit                     | `xunit`                |

Para obter mais informações sobre modelos de projeto da CLI do .NET, consulte [`dotnet new`](tools/dotnet-new.md) .

## <a name="systemtextjson-new-features"></a>System.Text.Jssobre novos recursos

Há novos recursos no e para o [System.Text.Jsem](../standard/serialization/system-text-json-overview.md):

- [Preservar referências e manipular referências circulares](../standard/serialization/system-text-json-preserve-references.md)
- [Métodos de extensão HttpClient e HttpContent](../standard/serialization/system-text-json-how-to.md#httpclient-and-httpcontent-extension-methods)
- [Permitir ou gravar números entre aspas](../standard/serialization/system-text-json-invalid-json.md#allow-or-write-numbers-in-quotes)
- [Suporte a tipos imutáveis e registros C# 9](../standard/serialization/system-text-json-immutability.md)
- [Suporte a acessadores de propriedade não públicos](../standard/serialization/system-text-json-immutability.md)
- [Campos de suporte](../standard/serialization/system-text-json-how-to.md#include-fields)
- [Ignorar as propriedades condicionalmente](../standard/serialization/system-text-json-ignore-properties.md)
- [Suporte a dicionários de chave não cadeia de caracteres](../standard/serialization/system-text-json-migrate-from-newtonsoft-how-to.md#dictionary-with-non-string-key)
- [Permitir que conversores personalizados manipulem NULL](../standard/serialization/system-text-json-converters-how-to.md#handle-null-values)
- [Copiar JsonSerializerOptions](../standard/serialization/system-text-json-configure-options.md#copy-jsonserializeroptions)
- [Criar JsonSerializerOptions com padrões da Web](../standard/serialization/system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions)

## <a name="see-also"></a>Veja também

- [A jornada para um .NET](https://channel9.msdn.com/Events/Build/2020/BOD106)
- [Melhorias de desempenho no .NET 5](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)
- [Baixar o SDK do .NET](https://dotnet.microsoft.com/download)
