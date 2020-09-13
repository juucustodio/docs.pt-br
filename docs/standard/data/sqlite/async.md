---
title: Limitações assíncronas
ms.date: 09/04/2020
description: Explica as limitações das APIs assíncronas e algumas alternativas que você pode usar em vez disso.
ms.openlocfilehash: 8b14fcfeb12d331d8d43ca6d77332007a12ae5dc
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89515989"
---
# <a name="async-limitations"></a>Limitações assíncronas

SQLite não dá suporte a e/s assíncrona. Os métodos Async ADO.NET serão executados de forma síncrona em Microsoft. Data. sqlite. Evite chamá-los.

Em vez disso, use um [cache compartilhado](connection-strings.md#cache) e um [log write-ahead](https://www.sqlite.org/wal.html) para melhorar o desempenho e a simultaneidade.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/AsyncSample/Program.cs?name=snippet_WAL)]

> [!TIP]
> O registro em log write-ahead é habilitado por padrão em bancos de dados criados usando [Entity Framework Core](/ef/core/).
