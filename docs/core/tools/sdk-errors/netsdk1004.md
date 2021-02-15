---
title: 'NETSDK1004: arquivo de ativos não encontrado'
description: Saiba mais sobre o erro NETSDK1004 do SDK do .NET, que ocorre quando o project.assets.jsno arquivo não é encontrado.
ms.topic: error-reference
ms.date: 01/29/2021
f1_keywords:
- NETSDK1004
ms.openlocfilehash: 8416063fe318106cbcb4dbccacef3ecaaff5bba2
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99216429"
---
# <a name="netsdk1004-assets-file-not-found"></a>NETSDK1004: arquivo de ativos não encontrado

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

O NuGet grava um arquivo chamado *project.assets.js* na pasta *obj* e o SDK do .NET usa-o para obter informações sobre pacotes a serem passados para o compilador. Esse erro ocorre quando o arquivo de ativos *project.assets.jsem* não é encontrado durante a compilação. A mensagem de erro completa é semelhante ao exemplo a seguir:

**NETSDK1004: arquivo de ativos ' C:\path\to\project.assets.jsem ' não encontrado. Execute uma restauração de pacote NuGet para gerar esse arquivo.**

Estas são algumas das possíveis causas do erro:

* Você está executando o `dotnet build` comando de um caminho de diretório que contém um `%` caractere. Para resolver o erro, remova o `%` do nome da pasta e execute novamente `dotnet build` .
* Uma alteração no arquivo de projeto não foi detectada e restaurada automaticamente pelo sistema de projeto. Para resolver o erro, abra um prompt de comando e execute- `dotnet restore` o no projeto.
* Um projeto foi restaurado separadamente por uma versão mais antiga do Nuget.exe. Para resolver o erro, abra um prompt de comando e execute- `dotnet restore` o no projeto.
* Um erro anterior, como NETSDK1045 (a versão do SDK que você está usando não dá suporte à estrutura de destino do projeto), impediu que o NuGet criasse o arquivo de ativos do projeto. Para resolver o erro NETSDK1004, resolva o erro anterior e, em seguida, execute `dotnet restore` no projeto.
* App Center CI está compilando um projeto que tem um assembly externo que não está no NuGet. Para resolver o erro, use um pacote NuGet para o assembly.
