---
title: 'NETSDK1064: pacote não encontrado'
description: Saiba mais sobre o erro NETSDK1064 do SDK do .NET, que ocorre quando um pacote não é encontrado.
ms.topic: error-reference
ms.date: 02/10/2021
f1_keywords:
- NETSDK1064
ms.openlocfilehash: 1a155db1aacbceb9878401dbcac61ece5f1f9824
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488274"
---
# <a name="netsdk1064-package-not-found"></a>NETSDK1064: pacote não encontrado

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

Esse erro ocorre quando as ferramentas de compilação não conseguem localizar um pacote NuGet necessário para criar um projeto. Isso normalmente ocorre devido a um problema de restauração de pacote. A mensagem de erro completa é semelhante ao exemplo a seguir:

> NETSDK1064: o pacote ' PackageName ', versão x. x. x não foi encontrado. Ele pode ter sido excluído desde a restauração do NuGet. Caso contrário, a restauração do NuGet pode ter sido concluída parcialmente, o que pode ter sido devido a restrições de comprimento máximo do caminho.

Aqui estão algumas ações que você pode executar para resolver esse erro:

* Adicione a `/restore` opção ao seu comando *MSBuild.exe* . Não use `/t:Restore;Build` , pois isso pode resultar em Bugs sutis. Uma alternativa é usar o `dotnet build` comando, já que ele faz automaticamente uma restauração de pacote.
* Se você estiver executando a restauração do pacote usando o Visual Studio 2019 ou *MSBuild.exe*, o erro poderá ser causado por restrições de comprimento máximo do caminho. Para obter mais informações, consulte [suporte a longo caminho (CLI do NuGet)](/nuget/reference/cli-reference/cli-ref-long-path) e o [problema do nuget/Home #3324](https://github.com/NuGet/Home/issues/3324).
* Se você estiver restaurando com o *nuget.exe* x86 e compilando com o *MSBuild.exe* x64, o bit de bits incompatível poderá causar esse erro. A compilação não pode localizar os pacotes que a restauração alega que ele adquiriu porque o caminho em *project.assets.jsem* não funciona em um processo de diferentes bits. Para resolver o erro, use as ferramentas do mesmo bit de bit para restaurar e compilar, ou configure o NuGet para restaurar pacotes em uma pasta que não faz a virtualização entre x86 e x64. Para obter mais informações, consulte o [problema dotnet/principal #4332](https://github.com/dotnet/core/issues/4332).
* Se você estiver criando uma imagem do Docker, verifique se o arquivo *. dockerignore* ignora os diretórios *bin* e *obj* . Para obter mais informações, consulte [NETSDK1064: Package DnsClient, 1.2.0 não foi encontrado](https://stackoverflow.com/questions/61167032/error-netsdk1064-package-dnsclient-1-2-0-was-not-found).
