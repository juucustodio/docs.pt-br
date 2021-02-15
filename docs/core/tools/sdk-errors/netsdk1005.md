---
title: 'NETSDK1005 e NETSDK1047: o arquivo de ativo está com destino ausente'
description: Como resolver o problema de um arquivo de ativo que não tem um destino.
author: sfoslund
ms.topic: error-reference
ms.date: 12/17/2020
f1_keywords:
- NETSDK1005
- NETSDK1047
ms.openlocfilehash: e3e7389adf6a9a715d44661a5f7cbae5efe299e4
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678166"
---
# <a name="netsdk1005-and-netsdk1047-asset-file-is-missing-target"></a>NETSDK1005 e NETSDK1047: o arquivo de ativo está com destino ausente

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

Quando o SDK do .NET emite o erro NETSDK1005 ou NETSDK1047, o arquivo de ativos do projeto não tem informações sobre uma de suas estruturas de destino. O NuGet grava um arquivo chamado *project.assets.js* na pasta *obj* e o SDK do .NET usa-o para obter informações sobre pacotes a serem passados para o compilador. No .NET 5, o NuGet adicionou um novo campo chamado `TargetFrameworkAlias` , de modo que as versões anteriores do MSBuild ou do NuGet gerem um arquivo de ativos sem o novo campo. Para obter mais informações, consulte [Error NETSDK1005](https://developercommunity.visualstudio.com/content/problem/1248649/error-netsdk1005-assets-file-projectassetsjson-doe.html).

Aqui estão algumas ações que podem ser tomadas para resolver o erro:

* Verifique se você está usando o MSBuild versão 16,8 ou posterior e a versão 5,8 ou posterior do NuGet e restaure o projeto depois de atualizar suas ferramentas. Quando estiver usando o NuGet versão 5,8 ou posterior, você deverá usar o Visual Studio 2019 versão 16,8 ou posterior, o MSBuild versão 16,8 ou posterior e o SDK do .NET 5,0 ou posterior.

* Se você receber o erro ao criar um projeto no Visual Studio 2019 pela primeira vez depois de instalar a versão 16,8 ou depois de alterar a estrutura de destino do projeto, compile o projeto uma segunda vez.

* Exclua a pasta *obj* antes de compilar o projeto.

* Verifique se o valor de destino ausente está incluído na `TargetFrameworks` Propriedade do seu projeto.
