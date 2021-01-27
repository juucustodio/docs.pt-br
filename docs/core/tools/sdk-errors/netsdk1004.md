---
title: 'NETSDK1004: arquivo de ativos não encontrado'
description: Saiba mais sobre o erro NETSDK1004 do SDK do .NET, que ocorre quando o project.assets.jsno arquivo não é encontrado.
ms.topic: error-reference
ms.date: 01/26/2021
f1_keywords:
- NETSDK1004
ms.openlocfilehash: ed42ad0e8ebef7362cc029125fe51d3f300acbae
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98900353"
---
# <a name="netsdk1004-assets-file-not-found"></a>NETSDK1004: arquivo de ativos não encontrado

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

Esse erro ocorre quando o arquivo de ativos *project.assets.jsem* não é encontrado durante a compilação. A mensagem de erro completa é semelhante a:

**NETSDK1004: arquivo de ativos ' C:\IncorrectPath\project.assets.jsem ' não encontrado. Execute uma restauração de pacote NuGet para gerar esse arquivo.**

Um motivo pelo qual você pode encontrar o aviso NETSDK1004 é se você executar o `dotnet build` comando de um caminho de diretório que contém um `%` caractere.
