---
title: Extensões
ms.date: 12/08/2020
description: Saiba como carregar extensões do SQLite.
ms.openlocfilehash: 68d31093662f373d6ebf4460d6a5d44029c27c5c
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110839"
---
# <a name="extensions"></a>Extensões

O SQLite dá suporte ao carregamento de extensões em tempo de execução. As extensões incluem itens como funções SQL adicionais, agrupamentos, tabelas virtuais e muito mais.

O .NET Core inclui lógica adicional para a localização de bibliotecas nativas em locais adicionais, como pacotes NuGet referenciados. Infelizmente, o SQLite não pode aproveitar essa lógica; Ele chama a API da plataforma diretamente para carregar bibliotecas. Por isso, talvez seja necessário modificar o caminho, LD_LIBRARY_PATH ou DYLD_LIBRARY_PATH variáveis de ambiente antes de carregar as extensões do SQLite. Há [um exemplo](https://github.com/dotnet/docs/blob/master/samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs) no GitHub que demonstra a localização de binários para o tempo de execução atual dentro de um pacote NuGet referenciado.

Para carregar uma extensão, chame o <xref:Microsoft.Data.Sqlite.SqliteConnection.LoadExtension%2A> método. Microsoft. Data. sqlite garantirá que a extensão permaneça carregada mesmo se a conexão for fechada e reaberta.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs?name=snippet_LoadExtension)]

> [!NOTE]
> O método LoadExtension foi adicionado na versão 3,0.

## <a name="see-also"></a>Veja também

* [Extensões carregáveis de tempo de execução](https://www.sqlite.org/loadext.html)
