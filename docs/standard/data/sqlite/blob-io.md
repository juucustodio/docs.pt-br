---
title: E/S de Blob
ms.date: 12/08/2020
description: Saiba como usar O recurso de e/s de BLOB do SQLite.
ms.openlocfilehash: 8b305669f3155d2366215e9a05beb5ed51533d81
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110039"
---
# <a name="blob-io"></a>E/S de Blob

> [!NOTE]
> A classe SqliteBlob foi adicionada na versão 3,0.

Você pode reduzir o uso de memória durante a leitura e a gravação de objetos grandes transmitindo os dados para dentro e fora dele. Isso pode ser especialmente útil ao analisar ou transformar os dados.

Comece inserindo uma linha como normal. Use a `zeroblob()` função SQL para alocar espaço no banco de dados para conter o objeto grande. A `last_insert_rowid()` função fornece uma maneira conveniente de obter seu ROWID.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Insert)]

Depois de inserir a linha, abra um fluxo para gravar o objeto grande usando <xref:Microsoft.Data.Sqlite.SqliteBlob> .

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Write)]

Para transmitir o objeto grande para fora do banco de dados, você deve selecionar o ROWID ou um de seus aliases, como mostrado aqui, além da coluna do objeto grande. Se você não selecionar o ROWID, todo o objeto será carregado na memória. O objeto retornado por `GetStream()` será um `SqliteBlob` quando feito corretamente.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Read)]
