---
title: Identificar sequência de projetos a serem migrados
description: Aplicativos grandes normalmente não são migrados para novas plataformas, tudo de uma só vez, mas em uma série de etapas menores. Saiba como planejar as etapas para migrar um aplicativo MVC ASP.NET para ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 70a2389786456fdf0e2c6d7d4ac768d37f1ce233
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488380"
---
# <a name="identify-sequence-of-projects-to-migrate"></a>Identificar sequência de projetos a serem migrados

Para soluções que envolvem vários aplicativos de front-end, é melhor migrar os aplicativos um a um. Por exemplo, crie uma solução que inclua apenas um aplicativo de front-end e suas dependências para que você possa identificar facilmente o escopo do trabalho envolvido. As soluções são leves e você pode incluir projetos em várias soluções, se necessário. Aproveite as soluções como uma ferramenta organizacional ao migrar.

Depois de identificar o aplicativo ASP.NET para migrar e ter seus projetos dependentes localizados com ele (idealmente em uma solução), a próxima etapa é identificar as dependências do Framework e do NuGet. Depois de identificar todas as dependências, a abordagem de migração mais simples é uma abordagem "de baixo para cima". Com essa abordagem, o nível mais baixo de dependências é migrado primeiro. Em seguida, o próximo nível de dependências é migrado, até que eventualmente a única coisa restante seja o aplicativo front-end. A Figura 3-1 mostra um conjunto de exemplos de projetos que compõem um aplicativo. As bibliotecas de classe de nível baixo estão na parte inferior e o projeto MVC do ASP.NET está na parte superior.

![Dependências do projeto](./media/Figure3-1.png)

**Figura 3-1.** Grafo de dependências do projeto.

Escolha um aplicativo de front-end específico, um projeto do ASP.NET MVC 5/API Web 2. Identifique suas dependências na solução e mapeie suas dependências até que você tenha uma lista completa. Um diagrama como aquele mostrado na Figura 3-1 pode ser útil ao mapear dependências do projeto. O Visual Studio pode produzir um [diagrama de dependência para sua solução](https://docs.microsoft.com/visualstudio/modeling/create-layer-diagrams-from-your-code), dependendo da edição que você estiver usando. [O .net Portability Analyzer](https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer) também pode produzir diagramas de dependência.

A Figura 3-2 mostra o instalador para a [extensão do Visual Studio do analisador de portabilidade .net](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer):

![Instalar extensão do analisador de portabilidade .NET](./media/Figure3-2.png)

**Figura 3-2.** Instalador do analisador de portabilidade .NET.

A extensão oferece suporte ao Visual Studio 2017 e posterior. Uma vez instalado, você o configura no menu **analisar**  >  **configurações do analisador de portabilidade** , como mostra a Figura 3-3.

![Configurar a extensão do analisador de portabilidade .NET](./media/Figure3-3.png)

**Figura 3-3.** Configurar o analisador de portabilidade .NET.

O analisador produz um relatório detalhado para cada assembly. O relatório:

* Descreve como cada projeto é compatível com uma determinada estrutura de destino, como .NET Core 3,1 ou .NET Standard 2,0.
* Ajuda as equipes a avaliar o esforço necessário para portar um determinado projeto para uma estrutura de destino específica.

Os detalhes dessa análise são abordados na próxima seção.

Depois de mapear os projetos e suas relações uns com os outros, você estará pronto para determinar a ordem na qual você migrará os projetos. Comece com projetos que não têm dependências. Em seguida, trabalhe até a árvore até os projetos que dependem desses projetos.

No exemplo mostrado na Figura 3-1, você começaria com o projeto *contoso. utils* , pois ele não depende de outros projetos. Em seguida, *contoso. Data* , pois só depende de "utils". Em seguida, migre a biblioteca "BusinessLogic" e, por fim, o projeto de front-end ASP.NET "Web". Seguir essa abordagem "de baixo para cima" funciona bem para aplicativos relativamente pequenos e bem fatorados que podem ser migrados como uma unidade uma vez que todos os seus projetos foram migrados. Aplicativos maiores com mais complexidade, ou mais código que levará mais tempo para migrar, talvez precisem considerar mais estratégias incrementais.

## <a name="unit-tests"></a>Testes de unidade

Os diagramas anteriores estão ausentes dos projetos de teste de unidade. Espero que haja testes que abrangem pelo menos um comportamento existente das bibliotecas que estão sendo portadas.

Se você tiver testes de unidade, será melhor converter esses projetos primeiro. Convém continuar testando as alterações no projeto em que você está trabalhando. Lembre-se de que a portabilidade para o .NET Core é uma alteração significativa na base de código.

MSTest, xUnit e NUnit funcionam no .NET Core. Se você não tiver testes no momento para seu aplicativo, considere a criação de alguns testes de caracterização que verificam o comportamento atual do sistema. O benefício é que, quando a migração for concluída, você poderá confirmar se o comportamento do aplicativo permanece inalterado.

## <a name="considerations-for-migrating-many-apps"></a>Considerações sobre a migração de muitos aplicativos

Algumas organizações terão muitos aplicativos diferentes para migrar e a migração de cada uma delas pode exigir que muitos recursos sejam tenabledos. Nessas situações, é recomendável algum grau de automação. As etapas seguidas neste capítulo podem ser automatizadas. Alterações estruturais, como diferenças de arquivo de projeto e atualizações para pacotes comuns, podem ser aplicadas por scripts. Esses scripts podem ser refinados à medida que são executados iterativamente em mais projetos. Em cada execução, examine quaisquer etapas manuais necessárias para cada projeto. Automatize essas etapas manuais, se possível. Usando essa abordagem, a organização deve crescer mais rápido e melhor na portabilidade de seus aplicativos ao longo do tempo, com suporte à automação aprimorada a cada etapa.

Assista a uma visão geral de como empregar essa abordagem nesta [apresentação de dotNetConf de Lizzy Gallagher da MasterCard](https://www.youtube.com/watch?v=C-2haqb60No). As cinco fases empregadas nesta apresentação incluíram:

- Migrar dependências de NuGet de terceiros
- Migrar aplicativos para usar o novo formato de arquivo *. csproj*
- Migrar aplicativos para ASP.NET Core (direcionamento .NET Framework)
- Atualizar dependências internas do NuGet para .NET Standard
- Atualizar todos os aplicativos para o .NET Core 3,1 de destino

Ao automatizar um grande pacote de aplicativos, ele ajuda significativamente se seguir as diretrizes de codificação consistentes e a organização do projeto. Os esforços de automação dependem dessa consistência para entrar em vigor. Além de analisar e migrar arquivos de projeto, os padrões de código comuns podem ser migrados automaticamente. Alguns exemplos de padrão de código incluem diferenças em como as ações do controlador são declaradas ou como retornam os resultados.

Por exemplo, um script de migração pode pesquisar arquivos que correspondem a *Controller.cs* para linhas de código que correspondam a um destes padrões:

```csharp
   return new HttpStatusCodeResult(200);
   // or
   return new HttpStatusCodeResult(HttpStatusCode.OK);
```

No ASP.NET Core, qualquer uma das linhas de código precedentes pode ser substituída por:

```csharp
    return Ok();
```

## <a name="summary"></a>Resumo

A melhor abordagem para portar um aplicativo de .NET Framework grande para o .NET Core é:

1. Identificar dependências do projeto.
1. Analise o que é necessário para a porta de cada projeto.
1. Comece de baixo para cima.

Você pode usar o .NET Portability Analyzer para determinar como as bibliotecas existentes compatíveis podem estar com plataformas de destino. Os testes automatizados ajudarão a garantir que nenhuma alteração significativa seja introduzida à medida que o aplicativo for portado. Esses projetos de teste devem estar entre os primeiros projetos portados.

## <a name="references"></a>Referências

- [Portabilidade do .NET Framework para o .NET Core](https://docs.microsoft.com/dotnet/core/porting/)
- [O .NET Portability Analyzer](https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer)
- [Channel 9: uma breve visão do analisador de portabilidade do .NET (vídeo)](https://channel9.msdn.com/Blogs/Seth-Juarez/A-Brief-Look-at-the-NET-Portability-Analyzer)
- [2 anos, 200 aplicativos: uma migração do .NET Core em escala (vídeo)](https://www.youtube.com/watch?v=C-2haqb60No)

>[!div class="step-by-step"]
>[Anterior](migrate-large-solutions.md) 
> [Avançar](understand-update-dependencies.md)
