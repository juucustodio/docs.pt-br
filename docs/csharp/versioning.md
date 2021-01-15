---
title: Controle de versão de C# – Guia de C#
description: Compreender o funcionamento do controle de versão em C# e .NET
ms.date: 01/08/2017
ms.technology: csharp-advanced-concepts
ms.assetid: aa8732d7-5cd0-46e1-994a-78017f20d861
ms.openlocfilehash: dc192337e4eaa5f9f1d6509ea8c15deeac34a48c
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645463"
---
# <a name="versioning-in-c"></a>Controle de versão em C\#

Neste tutorial, você aprenderá o que significa o controle de versão no .NET. Você também aprenderá sobre os fatores a serem considerados ao fazer o controle de versão de sua biblioteca, bem como ao atualizar para uma nova versão de uma biblioteca.

## <a name="authoring-libraries"></a>Criando bibliotecas

Como um desenvolvedor que criou a bibliotecas .NET para uso público, provavelmente você esteve em situações em que precisa distribuir novas atualizações. Como você realiza esse processo é muito importante, pois você precisa garantir que haja uma transição suave do código existente para a nova versão da biblioteca. Aqui estão Vários aspectos a considerar ao criar uma nova versão:

### <a name="semantic-versioning"></a>Controle de Versão Semântico

[Controle de versão semântico](https://semver.org/) (SemVer, de forma abreviada) é uma convenção de nomenclatura aplicada a versões de sua biblioteca para indicar eventos com marcos específicos.
Idealmente, as informações de versão que você fornece a sua biblioteca devem ajudar os desenvolvedores a determinar a compatibilidade com seus projetos que usam versões mais antigas da mesma biblioteca.

A abordagem mais básica ao SemVer é o formato de 3 componentes `MAJOR.MINOR.PATCH`, em que:

- `MAJOR` é incrementado quando você faz alterações em APIs incompatíveis
- `MINOR` é incrementado quando você adiciona funcionalidades de maneira compatível com versões anteriores
- `PATCH` é incrementado quando você faz correções de bugs compatíveis com versões anteriores

Também há maneiras de especificar outros cenários, como versões de pré-lançamento etc. ao aplicar informações de versão à sua biblioteca .NET.

### <a name="backwards-compatibility"></a>Compatibilidade com versões anteriores

Conforme você lança novas versões de sua biblioteca, a compatibilidade com versões anteriores provavelmente será uma de suas principais preocupações.
Uma nova versão da biblioteca será compatível com a origem de uma versão anterior se o código que depende da versão anterior puder, quando recompilado, trabalhar com a nova versão.
Uma nova versão da biblioteca será compatível de forma binária se um aplicativo que dependia da versão anterior puder, sem recompilação, trabalhar com a nova versão.

Aqui estão algumas coisas a serem consideradas ao tentar manter a compatibilidade com versões mais antigas de sua biblioteca:

- Métodos virtuais: quando você torna um método em virtual não virtual na nova versão, significa que projetos que substituem esse método precisarão ser atualizados. Essa é uma alteração muito grande e significativa que é altamente desaconselhável.
- Assinaturas de método: ao atualizar um comportamento de método exige que você altere sua assinatura também, em vez disso, você deve criar uma sobrecarga para que o código que chama esse método ainda funcione.
Você sempre pode manipular a assinatura de método antiga para chamar a nova assinatura de método para que a implementação permaneça consistente.
- [Atributo obsoleto](language-reference/attributes/general.md#obsolete-attribute): você pode usar esse atributo no seu código para especificar classes ou membros da classe que foram preteridos e provavelmente serão removidos em versões futuras. Isso garante que os desenvolvedores que utilizam sua biblioteca estarão melhor preparados para alterações significativas.
- Argumentos de método opcionais: quando você tornar argumentos de método que antes eram opcionais em compulsórios ou alterar seu valor padrão, todo código que não fornece esses argumentos precisará ser atualizado.

> [!NOTE]
> Tornar os argumentos compulsórios opcionais deve ter muito pouco efeito, especialmente se ele não alterar o comportamento do método.

Quanto mais fácil for para os usuários atualizarem para a nova versão da sua biblioteca, mais provável será que eles atualizem o quanto antes.

### <a name="application-configuration-file"></a>Arquivo de Configuração do Aplicativo

Como um desenvolvedor de .NET, há uma chance muito grande de você já ter encontrado o [arquivo o `app.config`](../framework/configure-apps/file-schema/index.md) na maioria dos tipos de projeto.
Esse arquivo de configuração simples pode fazer muita diferença para melhorar a distribuição de novas atualizações. Em geral, você deve criar suas bibliotecas de forma que as informações que provavelmente forem alteradas regularmente sejam armazenadas no `app.config` arquivo, dessa forma, quando essas informações forem atualizadas, o arquivo de configuração das versões mais antigas precisará ser substituído pelo novo sem a necessidade de recompilação da biblioteca.

## <a name="consuming-libraries"></a>Consumindo bibliotecas

Como um desenvolvedor que consome bibliotecas .NET criadas por outros desenvolvedores, vocês provavelmente está ciente de que uma nova versão de uma biblioteca pode não ser totalmente compatível com seu projeto e pode acabar precisando atualizar seu código para trabalhar com essas alterações.

Para sua sorte, o ecossistema do C# e do .NET tem recursos e técnicas que permitem facilmente atualizar nosso aplicativo para trabalhar com novas versões das bibliotecas que podem introduzir alterações interruptivas.

### <a name="assembly-binding-redirection"></a>Redirecionamento de associação de assembly

Você pode usar o arquivo de *app.config* para atualizar a versão de uma biblioteca que seu aplicativo usa. Ao adicionar o que é chamado de [*redirecionamento de associação*](../framework/configure-apps/redirect-assembly-versions.md), você pode usar a nova versão da biblioteca sem precisar recompilar seu aplicativo. O exemplo a seguir mostra como você atualizará o arquivo de *app.config* do seu aplicativo para usar a `1.0.1` versão de patch do `ReferencedLibrary` em vez da `1.0.0` versão com a qual ele foi originalmente compilado.

```xml
<dependentAssembly>
    <assemblyIdentity name="ReferencedLibrary" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" />
    <bindingRedirect oldVersion="1.0.0" newVersion="1.0.1" />
</dependentAssembly>
```

> [!NOTE]
> Essa abordagem só funcionará se a nova versão do `ReferencedLibrary` for compatível de forma binária com seu aplicativo.
> Consulte a seção [Compatibilidade com versões anteriores](#backwards-compatibility) acima para ver as alterações importantes ao determinar a compatibilidade.

### <a name="new"></a>novo

Você usa o modificador `new` para ocultar membros herdados de uma classe base. Essa é uma maneira das classes derivadas responderem a atualizações em classes base.

Veja o exemplo seguinte:

[!code-csharp[Sample usage of the 'new' modifier](~/samples/snippets/csharp/versioning/new/Program.cs#sample)]

**Saída**

```console
A base method
A derived method
```

No exemplo acima, você pode ver como `DerivedClass` oculta o método `MyMethod` presente em `BaseClass`.
Isso significa que quando uma classe base na nova versão de uma biblioteca adiciona um membro que já existe em sua classe derivada, você pode simplesmente usar o modificador `new` no membro de sua classe derivada para ocultar o membro da classe base.

Quando nenhum modificador `new` é especificado, uma classe derivada ocultará por padrão membros conflitantes em uma classe base e, embora um aviso do compilador seja gerado, o código ainda será compilado. Isso significa que simplesmente adicionar novos membros a uma classe existente torna a nova versão da biblioteca compatível com a origem e de forma binária com o código que depende dela.

### <a name="override"></a>override

O modificador `override` significa que uma implementação derivada estende a implementação de um membro da classe base, em vez de ocultá-lo. O membro da classe base precisa ter o modificador `virtual` aplicado a ele.

[!code-csharp[Sample usage of the 'override' modifier](../../samples/snippets/csharp/versioning/override/Program.cs#sample)]

**Saída**

```console
Base Method One: Method One
Derived Method One: Derived Method One
```

O modificador `override` é avaliado em tempo de compilação e o compilador gerará um erro se não encontrar um membro virtual para substituir.

Seu conhecimento das técnicas discutidas e sua compreensão das situações em que elas serão usadas, será um longo caminho para facilitar a transição entre as versões de uma biblioteca.
