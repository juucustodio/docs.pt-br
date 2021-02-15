---
title: Introdução à portabilidade de aplicativos para o .NET Core
description: Este capítulo aborda uma lista de considerações para equipes que consideram a migração de aplicativos ASP.NET existentes para o .NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: a346d1c693389cc4ca682b41a3b7fc094cfa5482
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488373"
---
# <a name="introduction-to-porting-apps-to-net-core"></a>Introdução à portabilidade de aplicativos para o .NET Core

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

O .NET Core é um avanço revolucionário de .NET Framework. Ele oferece uma série de vantagens em .NET Framework em todo o quadro, desde a produtividade até o desempenho, desde o suporte de plataforma cruzada até a satisfação do desenvolvedor. ASP.NET Core foi até mesmo votada a estrutura da Web mais adorada na [pesquisa de 2020 Stack Overflow desenvolvedor](https://insights.stackoverflow.com/survey/2020#technology-most-loved-dreaded-and-wanted-web-frameworks). Claramente, há motivos fortes para se considerar a migração.

É importante ter em mente que [o .NET Core é o futuro do .net](https://devblogs.microsoft.com/dotnet/net-core-is-the-future-of-net/). Para citar este artigo:

> Novos aplicativos devem ser criados no .NET Core. O .NET Core é onde os investimentos futuros no .NET ocorrerão. Os aplicativos existentes têm segurança para permanecer em .NET Framework que terão suporte. Os aplicativos existentes que desejam aproveitar os novos recursos do .NET devem considerar a migração para o .NET Core. À medida que planejamos para o futuro, disponibilizaremos ainda mais recursos para a plataforma.

No entanto, atualizar seu aplicativo para ASP.NET Core exigirá algum esforço. Esse esforço deve ser equilibrado em relação ao valor e às metas de negócios. .NET Framework aplicativos têm uma vida longa, com suporte integrado ao Windows para o futuro próximo. Quais são algumas das perguntas que você deve considerar antes de decidir que a migração para o .NET Core é apropriada? Quais são as vantagens esperadas? Quais são as desvantagens? Quanto esforço está envolvido? Essas perguntas óbvias são apenas o começo, mas destinam-se a um ótimo ponto de partida, pois as equipes consideram como dar suporte às necessidades de seus clientes com aplicativos hoje e amanhã.

- A migração para o .NET Core é apropriada?
- Quando faz sentido permanecer em .NET Framework?
- Os aplicativos devem se direcionar ASP.NET Core 2,1 como uma pedra de revisão?
- Como as equipes devem escolher a versão correta do .NET Core para o destino?
- Quais estratégias são recomendadas para a migração incremental de aplicativos grandes?
- Quais estratégias de implantação devem ser consideradas ao portar para o .NET Core?
- Onde podemos encontrar recursos adicionais?

Este capítulo introdutório aborda todas essas perguntas e muito mais antes de passar para considerações mais específicas e técnicas em capítulos futuros.

## <a name="references"></a>Referências

- [2020 Stack Overflow pesquisa de desenvolvedor mais entes estruturas da Web](https://insights.stackoverflow.com/survey/2020#technology-most-loved-dreaded-and-wanted-web-frameworks)
- [O .NET Core é o futuro do .NET](https://devblogs.microsoft.com/dotnet/net-core-is-the-future-of-net/)

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](migration-considerations.md)
