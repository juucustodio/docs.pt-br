---
description: 'Saiba mais sobre: criar um pool de objetos usando um ConcurrentBag'
title: Criar um pool de objetos usando um ConcurrentBag
ms.date: 05/01/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
ms.openlocfilehash: c14f77fcedaab8e7e1ac09eb065d1a8d0198e127
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676034"
---
# <a name="create-an-object-pool-by-using-a-concurrentbag"></a>Criar um pool de objetos usando um ConcurrentBag

Este exemplo mostra como usar um <xref:System.Collections.Concurrent.ConcurrentBag%601> para implementar um pool de objetos. Pools de objeto podem melhorar o desempenho do aplicativo em situações em que exigem várias instâncias de uma classe e nos quais criar ou destruir a classe é um processo caro. Quando um programa cliente solicita um novo objeto, o pool de objetos primeiro tenta fornecer um que já foi criado e retornado ao pool. Se nenhum estiver disponível, só então um novo objeto será criado.

O <xref:System.Collections.Concurrent.ConcurrentBag%601> é usado para armazenar os objetos porque ele dá suporte à rápida inserção e remoção, especialmente quando o mesmo thread está adicionando e removendo itens. Esse exemplo poderia ser aumentado ainda mais para ser criado em torno de um <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>, que a estrutura de dados do recipiente implementa, como <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601> fazem.

> [!TIP]
> Este artigo define como escrever sua própria implementação de um pool de objetos com um tipo simultâneo subjacente para armazenar objetos para reutilização. No entanto, o <xref:Microsoft.Extensions.ObjectPool.ObjectPool%601?displayProperty=nameWithType> tipo já existe no <xref:Microsoft.Extensions.ObjectPool?displayProperty=fullName> namespace. Considere o uso do tipo disponível antes de criar sua própria implementação, que inclui muitos recursos adicionais.

## <a name="example"></a>Exemplo

[!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
[!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]

## <a name="see-also"></a>Consulte também

- [Coleções thread-safe](index.md)
