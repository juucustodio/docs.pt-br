---
title: Visão geral da implantação do ReadyToRun
description: Saiba o que são implantações ReadyToRun e por que você deve considerar usá-la como parte da publicação de seu aplicativo com o .NET 5 e o .NET Core 3,0 e posterior.
author: davidwr
ms.author: davidwr
ms.date: 09/21/2020
ms.openlocfilehash: 3302e5e18a20965a1eff1f09737910e924ed6d08
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188602"
---
# <a name="readytorun-compilation"></a>Compilação ReadyToRun

A latência e o tempo de inicialização do aplicativo .NET podem ser aprimorados com a compilação de seus assemblies de aplicativo como o formato ReadyToRun (R2R). R2R é uma forma de compilação antecipada (AOT).

Os binários R2R melhoram o desempenho de inicialização reduzindo a quantidade de trabalho que o compilador just-in-time (JIT) precisa fazer à medida que seu aplicativo é carregado. Os binários contêm código nativo similar comparado ao que o JIT produziria. Entretanto, os binários R2R são maiores porque contêm código de IL (linguagem intermediária), que ainda é necessário para alguns cenários, e a versão nativa do mesmo código. O R2R só está disponível quando você publica um aplicativo destinado a ambientes de tempo de execução específicos (RID), como Linux x64 ou Windows x64.

Para compilar seu projeto como ReadyToRun, o aplicativo deve ser publicado com a propriedade PublishReadyToRun definida como `true` .

Há duas maneiras de publicar seu aplicativo como ReadyToRun:

01. Especifique o sinalizador PublishReadyToRun diretamente para o comando dotnet publish. Consulte [dotnet Publish](../tools/dotnet-publish.md) para obter detalhes.

    ```dotnetcli
    dotnet publish -c Release -r win-x64 -p:PublishReadyToRun=true
    ```

02. Especifique a propriedade no projeto.

    - Adicione a `<PublishReadyToRun>` configuração ao seu projeto.

    ```xml
    <PropertyGroup>
      <PublishReadyToRun>true</PublishReadyToRun>
    </PropertyGroup>
    ```

    - Publique o aplicativo sem parâmetros especiais.

    ```dotnetcli
    dotnet publish -c Release -r win-x64
    ```

## <a name="impact-of-using-the-readytorun-feature"></a>Impacto do uso do recurso ReadyToRun

A compilação antecipada tem um impacto complexo no desempenho do aplicativo, o que pode ser difícil de prever. Em geral, o tamanho de um assembly aumentará entre dois a três vezes maior. Esse aumento no tamanho físico do arquivo pode reduzir o desempenho do carregamento do assembly do disco e aumentar o conjunto de trabalho do processo. No entanto, em retorno, o número de métodos compilados no tempo de execução normalmente é reduzido substancialmente. O resultado é que a maioria dos aplicativos que têm grandes quantidades de código recebem grandes benefícios de desempenho ao habilitar o ReadyToRun. Aplicativos que têm pequenas quantidades de código provavelmente não terão uma melhoria significativa da habilitação de ReadyToRun, já que as bibliotecas de tempo de execução do .NET ainda foram pré-compiladas com o ReadyToRun.

A melhoria da inicialização discutida aqui se aplica não apenas à inicialização do aplicativo, mas também ao primeiro uso de qualquer código no aplicativo. Por exemplo, ReadyToRun pode ser usado para reduzir a latência de resposta do primeiro uso da API Web em um aplicativo ASP.NET.

### <a name="interaction-with-tiered-compilation"></a>Interação com compilação em camadas

O código gerado antes do tempo não é tão otimizado quanto o código produzido pelo JIT. Para resolver esse problema, a compilação em camadas substituirá os métodos ReadyToRun usados com métodos gerados por JIT.

## <a name="how-is-the-set-of-precompiled-assemblies-chosen"></a>Como o conjunto de assemblies pré-compilados é escolhido?

O SDK irá pré-compilar os assemblies que são distribuídos com o aplicativo. Para aplicativos independentes, esse conjunto de assemblies incluirá a estrutura. Os binários C++/CLI não são elegíveis para compilação ReadyToRun.

## <a name="how-is-the-set-of-methods-to-precompile-chosen"></a>Como é escolhido o conjunto de métodos para pré-compilação?

O compilador tentará pré-compilar previamente o máximo de métodos possível. No entanto, por vários motivos, não se espera que o uso do recurso ReadyToRun impedirá que o JIT seja executado. Tais motivos podem incluir, mas não estão limitados a:

- Uso de tipos genéricos definidos em assemblies separados.
- Interoperabilidade com código nativo.
- O uso de intrínsecos de hardware que o compilador não pode provar é seguro para uso em um computador de destino.
- Determinados padrões de IL incomum.
- Criação dinâmica de métodos via reflexão ou LINQ.

## <a name="cross-platformarchitecture-restrictions"></a>Restrições de plataforma cruzada/arquitetura

Para algumas plataformas de SDK, o compilador ReadyToRun é capaz de Compilar várias plataformas de destino. Os destinos de compilação com suporte são descritos na tabela a seguir.

| Plataforma SDK | Plataformas de destino com suporte |
| ------------ | --------------------------- |
| Windows X64  | Windows x86, Windows x64, Windows ARM32, Windows ARM64 |
| Windows x86  | Windows x86, Windows ARM32 |
| Linux X64    | Linux x86, Linux x64, Linux ARM32, Linux ARM64 |
| Linux ARM32  | Linux ARM32 |
| ARM64 Linux  | ARM64 Linux |
| macOS x64    | macOS x64 |
