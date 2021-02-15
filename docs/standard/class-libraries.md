---
title: Bibliotecas de classes do .NET
description: Saiba como as bibliotecas de classes do .NET permitem que você agrupe funcionalidades úteis em módulos que podem ser usados por vários aplicativos.
author: richlander
ms.date: 06/20/2016
ms.assetid: a67484c3-fe92-44d8-8fa3-36fa2071d880
ms.openlocfilehash: bbf8d5fa44af931e39f2bf1344c13f9d9d9bfe05
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94823947"
---
# <a name="net-class-libraries"></a>Bibliotecas de classes do .NET

As bibliotecas de classe são o conceito de [biblioteca compartilhada](https://en.wikipedia.org/wiki/Library_%28computing%29#Shared_libraries) para .NET. Elas permitem que você componentize funcionalidades úteis em módulos que podem ser usados por vários aplicativos. Elas também podem ser usadas como um meio de carregar a funcionalidade não necessária ou não conhecida na inicialização do aplicativo. Bibliotecas de classe são descritas usando o [formato de arquivo do Assembly .NET](assembly/file-format.md).

Há três tipos de bibliotecas de classes que você pode usar:

* Bibliotecas de classe **específicas da plataforma** têm acesso a todas as APIs em uma determinada plataforma (por exemplo, .NET Framework, Xamarin iOS), mas só podem ser usadas por aplicativos e bibliotecas que direcionam essa plataforma.
* Bibliotecas de classe **portáteis** têm acesso a um subconjunto de APIs e podem ser usadas por aplicativos e bibliotecas voltados para várias plataformas.
* Bibliotecas de classe **.NET Standard** são uma fusão do conceito de biblioteca portátil e específica da plataforma em um único modelo que fornece o melhor dos dois mundos.

## <a name="platform-specific-class-libraries"></a>Bibliotecas de classes específicas da plataforma

Bibliotecas específicas da plataforma estão associadas a uma única implementação do .NET (por exemplo, .NET Framework no Windows) e, portanto, podem assumir dependências significativas em um ambiente de execução conhecido. Esse ambiente exporá um conjunto conhecido de APIs (.NET e APIs de SO) e manterá e exporá o estado esperado (por exemplo, o Registro do Windows).

Os desenvolvedores que criam bibliotecas específicas da plataforma podem explorar totalmente a plataforma subjacente. As bibliotecas só serão executadas na plataforma específica, fazendo verificações de plataforma ou outras formas de código condicional desnecessários (módulo de códigos de fornecimento únicos para várias plataformas).

Bibliotecas específicas da plataforma são o tipo de biblioteca de classes principal para o .NET Framework. Mesmo que outras implementações do .NET tenham surgido, as bibliotecas específicas da plataforma permaneceram o tipo de biblioteca dominante.

## <a name="portable-class-libraries"></a>Bibliotecas de classes portáteis

Há suporte para bibliotecas portáteis em várias implementações do .NET. Eles ainda podem assumir dependências em um ambiente de execução conhecido, no entanto, o ambiente é um sintético que é gerado pela interseção de um conjunto de implementações .NET concretas. APIs expostas e suposições de plataforma são um subconjunto do que estaria disponível para uma biblioteca específica da plataforma.

Você escolhe uma configuração de plataforma ao criar uma biblioteca portátil. A configuração de plataforma é o conjunto de plataformas para o qual você precisa dar suporte (por exemplo, .NET Framework 4.5 +, Windows Phone 8.0 +). Quanto mais plataformas você escolher dar suporte, menos suposições de plataforma terá que fazer e menor será o denominador comum. Essa característica pode ser confusa a princípio, uma vez que as pessoas costumam imaginar "mais é melhor", mas descubra que mais plataformas com suporte resultam em menos APIs disponíveis.

Muitos desenvolvedores de biblioteca mudam de produzir várias bibliotecas específicas de plataforma de uma origem (usando as diretivas de compilação condicional) para bibliotecas portáteis. Há [várias abordagens](https://blog.stephencleary.com/2012/11/portable-class-library-enlightenment.html) para acessar a funcionalidade específica da plataforma nas bibliotecas portáteis com a técnica bait-and-switch, a mais amplamente aceita neste momento.

## <a name="net-standard-class-libraries"></a>Bibliotecas de classe do .NET Standard

As bibliotecas do .NET Standard são uma substituição dos conceitos de bibliotecas específicas da plataforma e portáteis. Elas são específicas da plataforma no sentido de que expõem toda a funcionalidade da plataforma subjacente (sem plataformas sintéticas ou interseções de plataforma). Elas são portáteis no sentido de que funcionam em todas as plataformas de suporte.

.NET Standard expõe um conjunto de _contratos_ de biblioteca. As implementações do .NET devem dar suporte a cada contrato, completamente ou não dar nenhum suporte. Cada implementação, portanto, dá suporte a um conjunto de contratos do .NET Standard. O resultado é que há suporte para cada biblioteca de classes do .NET Standard nas plataformas compatíveis com suas dependências de contrato.

O .NET Standard não expõe toda a funcionalidade do .NET Framework (nem é uma meta), no entanto, eles expõem muitas APIs mais do que as bibliotecas de classes portáteis. Mais APIs serão adicionadas ao longo do tempo.

As seguintes plataformas dão suporte às bibliotecas de classes do .NET Standard:

* .NET Core
* .NET Framework
* Mono
* Xamarin.iOS, Xamarin.Mac, Xamarin.Android
* Plataforma Universal do Windows (UWP)
* Windows
* Windows Phone
* Windows Phone Silverlight

Para obter mais informações, confira [.NET Standard](net-standard.md).

## <a name="mono-class-libraries"></a>Bibliotecas de classes do Mono

As bibliotecas de classes têm suporte no mono, incluindo os três tipos de bibliotecas descritas anteriormente. O mono geralmente foi visto (corretamente) como uma implementação de plataforma cruzada de .NET Framework. Em parte, isso acontecia porque bibliotecas do .NET Framework específicas da plataforma podiam ser executadas no runtime Mono sem modificação ou recompilação. Essa característica estava em vigor antes da criação de bibliotecas de classes portáteis, portanto, era uma opção óbvia para habilitar a portabilidade binária entre o .NET Framework e o Mono (embora ele funcionasse apenas em uma direção).
