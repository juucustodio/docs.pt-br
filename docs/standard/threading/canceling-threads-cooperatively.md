---
description: 'Saiba mais sobre: cancelando os threads de cooperativa'
title: Cancelando threads de forma cooperativa
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- threads, cancellation
ms.assetid: d2d6d5fd-e263-4fa0-847b-2fc3e0d82337
ms.openlocfilehash: e166e95f3b7e000b4ea57cbd690de439b2883123
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675488"
---
# <a name="canceling-threads-cooperatively"></a>Cancelando threads de forma cooperativa

Antes do .NET Framework 4, o .NET não fornecia uma maneira interna de cancelar um thread de forma cooperativa depois que ele foi iniciado. No entanto, a partir do .NET Framework 4, você pode usar um <xref:System.Threading.CancellationToken?displayProperty=nameWithType> para cancelar threads, assim como você pode usá-los para cancelar <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> objetos ou Consultas PLINQ. Embora a classe <xref:System.Threading.Thread?displayProperty=nameWithType> não ofereça suporte interno para tokens de cancelamento, você pode passar um token para um procedimento de thread usando o constructo <xref:System.Threading.Thread> que usa um representante <xref:System.Threading.ParameterizedThreadStart>. O exemplo a seguir demonstra como fazer isso.  
  
 [!code-csharp[Cancellation#14](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/CooperativeThreads.cs#14)]
 [!code-vb[Cancellation#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/CooperativeThreads.vb#14)]  
  
## <a name="see-also"></a>Consulte também

- [Usando threads e threading](using-threads-and-threading.md)
