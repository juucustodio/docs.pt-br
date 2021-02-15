---
title: Ferramentas de portabilidade para o .NET Core
description: Conheça algumas das ferramentas que você pode usar para portar para o .NET Core
author: cartermp
ms.date: 05/03/2020
ms.openlocfilehash: b8678ec72fe5d910d5f8cff4768106e7496f9276
ms.sourcegitcommit: 1274a1a4a4c7e2eaf56b38da76ef7cec789726ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91406122"
---
# <a name="tools-to-help-with-porting-to-net-core"></a>Ferramentas para ajudar com a portabilidade para o .NET Core

As ferramentas listadas neste artigo podem ser úteis para portar:

- [Analisador de portabilidade .net](../../standard/analyzers/portability-analyzer.md) – um ferramentas que pode gerar um relatório de quão portátil seu código está entre .NET Framework e .NET Core:
  - Como uma [ferramenta de linha de comando](https://github.com/Microsoft/dotnet-apiport/releases)
  - Como uma [extensão do Visual Studio](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)
- [Analisador de compatibilidade de plataforma](../../standard/analyzers/platform-compat-analyzer.md) – um analisador de Roslyn que informa os desenvolvedores quando eles usam APIs específicas da plataforma de sites de chamada em que a API pode não estar disponível.
- [.NET API Analyzer](../../standard/analyzers/api-analyzer.md) – um analisador de Roslyn que pode ajudar a detectar problemas de compatibilidade de plataforma em aplicativos e bibliotecas de plataforma cruzada.
- [try – Convert](https://www.nuget.org/packages/try-convert/) – uma ferramenta global do .NET Core que pode converter um projeto ou uma solução completa para o SDK do .net, incluindo a movimentação de aplicativos da área de trabalho para o .NET Core. Não é recomendável se você tiver uma compilação mais complicada estabelecida (como tarefas personalizadas, destinos ou importações) e rejeitar muitos tipos de projeto que são incompatíveis com o .NET Core.
