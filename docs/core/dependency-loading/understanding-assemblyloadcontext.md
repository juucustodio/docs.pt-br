---
title: Entendendo o AssemblyLoadContext-.NET Core
description: Conceitos principais para entender a finalidade e o comportamento do AssemblyLoadContext no .NET Core.
ms.date: 08/09/2019
author: sdmaclea
ms.author: stmaclea
ms.openlocfilehash: 4d3f0e50e7c336469bd9af4d1589427388684434
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92332816"
---
# <a name="understanding-systemruntimeloaderassemblyloadcontext"></a>Compreendendo System. Runtime. Loader. AssemblyLoadContext

A <xref:System.Runtime.Loader.AssemblyLoadContext> classe é exclusiva do .NET Core. Este artigo tenta complementar a <xref:System.Runtime.Loader.AssemblyLoadContext> documentação da API com informações conceituais.

Este artigo é relevante para os desenvolvedores que implementam o carregamento dinâmico, especialmente os desenvolvedores de estrutura de carregamento dinâmico.

## <a name="what-is-the-assemblyloadcontext"></a>O que é o AssemblyLoadContext?

Cada aplicativo .NET Core usa implicitamente o <xref:System.Runtime.Loader.AssemblyLoadContext> .
É o provedor do tempo de execução para localizar e carregar dependências. Sempre que uma dependência é carregada, uma <xref:System.Runtime.Loader.AssemblyLoadContext> instância é invocada para localizá-la.

- Ele fornece um serviço de localizar, carregar e armazenar em cache assemblies gerenciados e outras dependências.

- Para dar suporte ao carregamento e descarregamento de código dinâmico, ele cria um contexto isolado para carregar código e suas dependências em sua própria <xref:System.Runtime.Loader.AssemblyLoadContext> instância.

## <a name="when-do-you-need-multiple-assemblyloadcontext-instances"></a>Quando você precisa de várias instâncias de AssemblyLoadContext?

Uma única <xref:System.Runtime.Loader.AssemblyLoadContext> instância é limitada a carregar exatamente uma versão de um <xref:System.Reflection.Assembly> por nome de assembly simples, <xref:System.Reflection.AssemblyName.Name?displayProperty=nameWithType> .

Essa restrição pode se tornar um problema ao carregar módulos de código dinamicamente. Cada módulo é compilado de forma independente e pode depender de versões diferentes de um <xref:System.Reflection.Assembly> . Esse problema geralmente ocorre quando diferentes módulos dependem de versões diferentes de uma biblioteca comumente usada.

Para dar suporte ao carregamento dinâmico de código, a <xref:System.Runtime.Loader.AssemblyLoadContext> API fornece o carregamento de versões conflitantes de um <xref:System.Reflection.Assembly> no mesmo aplicativo. Cada <xref:System.Runtime.Loader.AssemblyLoadContext> instância fornece um mapeamento de dicionário exclusivo <xref:System.Reflection.AssemblyName.Name?displayProperty=nameWithType> para uma <xref:System.Reflection.Assembly> instância específica.

Ele também fornece um mecanismo conveniente para agrupar dependências relacionadas a um módulo de código para descarregamento posterior.

## <a name="what-is-special-about-the-assemblyloadcontextdefault-instance"></a>O que é especial sobre a instância AssemblyLoadContext. Default?

A <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> instância é preenchida automaticamente pelo tempo de execução na inicialização.  Ele usa a [investigação padrão](default-probing.md) para localizar e localizar todas as dependências estáticas.

Ele resolve os cenários de carregamento de dependência mais comuns.

## <a name="how-does-assemblyloadcontext-support-dynamic-dependencies"></a>Como o AssemblyLoadContext dá suporte a dependências dinâmicas?

<xref:System.Runtime.Loader.AssemblyLoadContext> tem vários eventos e funções virtuais que podem ser substituídos.

A <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> instância só dá suporte à substituição de eventos.

Os artigos [algoritmos de carregamento de assembly gerenciado](loading-managed.md), [algoritmo de carregamento de assembly satélite](loading-resources.md)e [algoritmo de carregamento de biblioteca não gerenciada (nativa)](loading-unmanaged.md) referem-se a todos os eventos e funções virtuais disponíveis.  Os artigos mostram cada evento e a posição relativa da função nos algoritmos de carregamento. Este artigo não reproduz essas informações.

Esta seção aborda os princípios gerais para os eventos e funções relevantes.

- **Ser repetível**. Uma consulta para uma dependência específica sempre deve resultar na mesma resposta. A mesma instância de dependência carregada deve ser retornada. Esse requisito é fundamental para a consistência do cache. Para assemblies gerenciados em particular, estamos criando um <xref:System.Reflection.Assembly> cache. A chave de cache é um nome de assembly simples, <xref:System.Reflection.AssemblyName.Name?displayProperty=nameWithType> .
- **Normalmente não geram**.  Espera-se que essas funções retornem `null` em vez de throw quando não é possível localizar a dependência solicitada. A geração encerrará prematuramente a pesquisa e será propagada uma exceção para o chamador. O lançamento deve ser restrito a erros inesperados, como um assembly corrompido ou uma condição de memória insuficiente.
- **Evite a recursão**. Lembre-se de que essas funções e manipuladores implementam as regras de carregamento para localizar dependências. Sua implementação não deve chamar APIs que disparam a recursão. Seu código normalmente deve chamar funções de carregamento **AssemblyLoadContext** que exigem um caminho específico ou um argumento de referência de memória.
- **Carregue no AssemblyLoadContext correto**. A escolha de onde carregar dependências é específica do aplicativo.  A escolha é implementada por esses eventos e funções. Quando seu código chama o **AssemblyLoadContext** , as funções carregadas por caminho as chamam na instância em que você deseja que o código seja carregado. Algum tempo retornando `null` e permitindo que o <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> identificador da carga seja a opção mais simples.
- **Lembre-se de corridas de thread**. O carregamento pode ser disparado por vários threads. O AssemblyLoadContext lida com corridas de thread por meio da adição atômica de assemblies ao seu cache. A instância do perdedor da corrida é descartada. Na lógica de implementação, não adicione uma lógica extra que não manipule vários threads corretamente.

## <a name="how-are-dynamic-dependencies-isolated"></a>Como as dependências dinâmicas são isoladas?

Cada <xref:System.Runtime.Loader.AssemblyLoadContext> instância representa um escopo exclusivo para <xref:System.Reflection.Assembly> instâncias e <xref:System.Type> definições.

Não há nenhum isolamento binário entre essas dependências. Eles são isolados apenas por não encontrar um ao outro por nome.

Em cada <xref:System.Runtime.Loader.AssemblyLoadContext> :

- <xref:System.Reflection.AssemblyName.Name?displayProperty=nameWithType> pode se referir a uma <xref:System.Reflection.Assembly> instância diferente.
- <xref:System.Type.GetType%2A?displayProperty=nameWithType> pode retornar uma instância de tipo diferente para o mesmo tipo `name` .

## <a name="how-are-dependencies-shared"></a>Como as dependências são compartilhadas?

As dependências podem ser facilmente compartilhadas entre <xref:System.Runtime.Loader.AssemblyLoadContext> instâncias. O modelo geral é para um <xref:System.Runtime.Loader.AssemblyLoadContext> carregar uma dependência.  O outro compartilha a dependência usando uma referência ao assembly carregado.

Esse compartilhamento é necessário para os assemblies de tempo de execução. Esses assemblies só podem ser carregados no <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> . O mesmo é necessário para estruturas como `ASP.NET` , `WPF` ou `WinForms` .

É recomendável que as dependências compartilhadas sejam carregadas no <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> . Esse compartilhamento é o padrão de design comum.

O compartilhamento é implementado na codificação da instância personalizada <xref:System.Runtime.Loader.AssemblyLoadContext> . <xref:System.Runtime.Loader.AssemblyLoadContext> tem vários eventos e funções virtuais que podem ser substituídos. Quando qualquer uma dessas funções retorna uma referência a uma <xref:System.Reflection.Assembly> instância que foi carregada em outra <xref:System.Runtime.Loader.AssemblyLoadContext> instância, a <xref:System.Reflection.Assembly> instância é compartilhada. O algoritmo de carga padrão adia <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> o carregamento para simplificar o padrão de compartilhamento comum.  Consulte [algoritmo de carregamento de assembly gerenciado](loading-managed.md).

## <a name="complications"></a>Complicações

### <a name="type-conversion-issues"></a>Problemas de conversão de tipo

Quando duas <xref:System.Runtime.Loader.AssemblyLoadContext> instâncias contêm definições de tipo com o mesmo `name` , elas não são do mesmo tipo. Eles são do mesmo tipo se forem provenientes da mesma <xref:System.Reflection.Assembly> instância.

Para complicar as coisas, as mensagens de exceção sobre esses tipos incompatíveis podem ser confusas. Os tipos são referenciados nas mensagens de exceção por seus nomes de tipo simples. A mensagem de exceção comum, neste caso, seria a forma:

> O objeto do tipo ' Isolatype ' não pode ser convertido para o tipo ' Isolatype '.

### <a name="debugging-type-conversion-issues"></a>Problemas de conversão de tipo de depuração

Dado um par de tipos incompatíveis, é importante também saber:

- Cada tipo <xref:System.Type.Assembly?displayProperty=nameWithType>
- Cada tipo <xref:System.Runtime.Loader.AssemblyLoadContext> , que pode ser obtido por meio da <xref:System.Runtime.Loader.AssemblyLoadContext.GetLoadContext(System.Reflection.Assembly)?displayProperty=nameWithType> função.

Considerando-se dois objetos `a` e `b` , a avaliação do seguinte no depurador será útil:

```csharp
// In debugger look at each assembly's instance, Location, and FullName
a.GetType().Assembly
b.GetType().Assembly
// In debugger look at each AssemblyLoadContext's instance and name
System.Runtime.Loader.AssemblyLoadContext.GetLoadContext(a.GetType().Assembly)
System.Runtime.Loader.AssemblyLoadContext.GetLoadContext(b.GetType().Assembly)
```

### <a name="resolving-type-conversion-issues"></a>Resolvendo problemas de conversão de tipo

Há dois padrões de design para resolver esses problemas de conversão de tipo.

1. Use tipos compartilhados comuns. Esse tipo compartilhado pode ser um tipo de tempo de execução primitivo ou pode envolver a criação de um novo tipo compartilhado em um assembly compartilhado.  Geralmente, o tipo compartilhado é uma [interface](../../csharp/language-reference/keywords/interface.md) definida em um assembly de aplicativo. Consulte também: [como as dependências são compartilhadas?](#how-are-dependencies-shared).

2. Use técnicas de marshaling para converter de um tipo para outro.
