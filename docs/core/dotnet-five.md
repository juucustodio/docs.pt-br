---
title: A evolução do .NET Core para o .NET 5
description: Saiba mais sobre o .NET 5, uma plataforma de desenvolvimento de plataforma cruzada e de software livre que é a próxima evolução do .NET Core.
ms.date: 09/02/2020
ms.topic: overview
ms.author: dapine
author: IEvangelist
ms.openlocfilehash: 9318b1afbe22c97f056bd38732306c6a6b60ad00
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598121"
---
# <a name="the-evolution-of-net-core-to-net-5"></a>A evolução do .NET Core para o .NET 5

Este artigo fornece detalhes sobre o que está incluído no .NET 5, que é a próxima versão do .NET Core a seguir 3,1. O número de versão é 5,0 para evitar confusão com .NET Framework 4. x. E "Core" é descartado do nome porque é a principal implementação do .NET em frente. ASP.NET Core retém o nome "Core" para evitar confusão com o ASP.NET MVC 5. Além disso, Entity Framework Core retém o nome "Core" para evitar confusão com Entity Framework 5 e 6. O .NET 5 dá suporte a mais tipos de aplicativos e mais plataformas do que o .NET Core ou o .NET Framework.

O advento do .NET Core evoluiu o ecossistema do .NET de maneiras atraentes. Ele amadureceu como um projeto de software livre no GitHub, comemorando contribuições da Comunidade e humildemente melhorando com o tempo.

O .NET Core tem várias características principais:

> [!div class="checklist"]
>
> - Plataforma cruzada
> - Software livre
> - Instalação lado a lado
> - Arquivos de projeto pequenos (estilo de SDK)
> - Implantação flexível

O .NET 5 estende essas características, fazendo melhorias incrementais:

- Aplicativos de arquivo único
- Intrínsecos do Windows ARM64 e ARM64
- Aprimoramentos de desempenho de limpeza para:
  - [Coleta de lixo (GC)](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#gc)
  - [System.Text.Json](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#json)
  - [System.Text.RegularExpressions](https://devblogs.microsoft.com/dotnet/regex-performance-improvements-in-net-5)
  - [Pooling ValueTask assíncrona](https://devblogs.microsoft.com/dotnet/async-valuetask-pooling-in-net-5)
  - [Muito mais áreas](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)
- Otimizações de tamanho de contêiner
- [Corte de aplicativo](https://devblogs.microsoft.com/dotnet/app-trimming-in-net-5)
- [Aprimoramentos do compilador C#](https://devblogs.microsoft.com/dotnet/automatically-find-latent-bugs-in-your-code-with-net-5)
- Suporte de ferramentas para depuração de despejo
- A plataforma é 80% anotada para [tipos de referência anuláveis](../csharp/nullable-references.md)

### <a name="what-net-5-is-not"></a>O que o .NET 5 não é

O .NET 5 não é uma substituição para .NET Framework. Não há planos de portar as seguintes tecnologias de .NET Framework para o .NET 5, mas há alternativas com suporte incluídas no .NET 5:

| Tecnologia                             | Recomendação                                              |
|----------------------------------------|-------------------------------------------------------------|
| Web Forms                              | [ASP.NET Core mais](/aspnet/core/blazor)                  |
| Windows Communication Foundation (WCF) | [gRPC](/aspnet/core/grpc)                                   |
| Windows Workflow (WF)                  | [CoreWF de código-fonte aberto](https://github.com/UiPath-Open/corewf) |

## <a name="net-standard"></a>.NET Standard

O novo desenvolvimento de aplicativos pode especificar o `net5.0` moniker do Framework de destino (TFM) para todos os tipos de projeto, incluindo bibliotecas de classes. O compartilhamento de código entre as cargas de trabalho do .NET 5 é simplificado, pois tudo o que você precisa é o `net5.0` TFM.

O `net5.0` TFM combina e substitui os `netcoreapp` `netstandard` nomes e. Esse TFM geralmente incluirá apenas tecnologias que funcionam entre plataformas, como foi feito com .NET Standard. No entanto, se você planeja compartilhar o código entre as cargas de trabalho .NET Framework, .NET Core e .NET 5, poderá fazer isso especificando `netstandard2.0` como seu TFM. Para obter mais informações, consulte [como especificar estruturas de destino](../standard/frameworks.md#how-to-specify-a-target-framework).

## <a name="language-updates"></a>Atualizações de linguagem

Com o .NET 5, as linguagens de programação do .NET continuam a melhorar.

### <a name="c-updates"></a>Atualizações em C#

Os desenvolvedores que escrevem aplicativos .NET 5 terão acesso à versão e aos recursos mais recentes do C#. O .NET 5 é emparelhado com o C# 9, que traz muitos recursos novos para a linguagem. Aqui estão alguns destaques:

- Registros: tipos de referência imutáveis que se comportam como tipos de valor e apresentam a nova `with` palavra-chave à linguagem.
- Correspondência de padrão relacional: estende os recursos de correspondência de padrões para operadores relacionais para avaliações e expressões comparativa, incluindo padrões lógicos – novas palavras-chave `and` , `or` e `not` .
- Instruções de nível superior: como um meio para acelerar a adoção e o aprendizado do C#, o `Main` método pode ser omitido e o aplicativo tão simples quanto o seguinte é válido:

   ```csharp
   System.Console.Write("Hello world!");
   ```

- Ponteiros de função: constructos de linguagem que expõem os seguintes opcodes de linguagem intermediária (IL): `ldftn` e `calli` .

Para obter mais informações sobre os recursos disponíveis do C# 9, consulte [o que há de novo no c# 9](../csharp/whats-new/csharp-9.md).

#### <a name="source-generators"></a>Geradores de origem

Além de alguns dos novos recursos do C# destacados, os geradores de origem estão fazendo seu caminho em projetos de desenvolvedor. Os geradores de origem permitem o código que é executado durante a compilação para inspecionar seu programa e produzir arquivos adicionais que são compilados junto com o restante do seu código.

Para obter mais informações sobre geradores de origem, consulte [introdução aos geradores de código](https://devblogs.microsoft.com/dotnet/introducing-c-source-generators) -fonte c# e [exemplos do gerador de código-fonte c#](https://devblogs.microsoft.com/dotnet/new-c-source-generator-samples).

### <a name="f-updates"></a>Atualizações de F #

O f # é a linguagem de programação funcional do .NET e, com o .NET 5, os desenvolvedores têm acesso ao F # 5. Aqui estão vários recursos novos do F # 5:

#### <a name="interpolated-strings"></a>Cadeias de caracteres interpoladas

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

### <a name="visual-basic-updates"></a>Atualizações de Visual Basic

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

## <a name="net-maui"></a>.NET MAUI

O .NET MAUI é uma evolução do mais popular Xamarin. Forms Toolkit e é de software livre no GitHub em [dotnet/Maui](https://github.com/dotnet/maui). Com o .NET MAUI, a escolha para desenvolvedores .NET é simplificada, fornecendo uma única pilha que dá suporte a todas as cargas de trabalho modernas: Android, iOS, macOS e Windows. Com o .NET MAUI, você obtém uma experiência de desenvolvedor de projeto único que tem como alvo várias plataformas e dispositivos.

> [!IMPORTANT]
> O .NET MAUI está na visualização inicial. O código-fonte de exemplo pode ser encontrado em [xamarin/net6-Samples](https://github.com/xamarin/net6-samples).

### <a name="model-view-update-pattern"></a>Modelo-exibição-padrão de atualização

Os desenvolvedores adoram padrões de desenvolvimento modernos. Uma abordagem fluente do desenvolvimento da interface do usuário, inspirado pela "arquitetura Elm", é o padrão [Model-View-Update](https://elmprogramming.com/model-view-update-part-1.html) ou MVU. O MVU promove um fluxo unidirecional de gerenciamento de dados e estado, bem como uma experiência de desenvolvimento de primeiro código que atualiza rapidamente a interface do usuário aplicando apenas as alterações necessárias.

Como exemplo, considere o seguinte contador escrito em .NET MAUI usando o padrão MVU:

```csharp
readonly State<int> _count = 0;

[Body]
View body() => new StackLayout
{
    new Label("Welcome to .NET MAUI!"),
    new Button(
        () => $"You clicked {_count} times.",
        () => ++ _count.Value)
    )
};
```

Para obter mais informações, consulte o [roteiro do .net Maui](https://github.com/dotnet/maui/wiki/Roadmap)e apresentando o artigo do [.net Maui](https://devblogs.microsoft.com/dotnet/introducing-net-multi-platform-app-ui) .

## <a name="see-also"></a>Confira também

- [A jornada para um .NET](https://channel9.msdn.com/Events/Build/2020/BOD106)
- [Melhorias de desempenho no .NET 5](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)
