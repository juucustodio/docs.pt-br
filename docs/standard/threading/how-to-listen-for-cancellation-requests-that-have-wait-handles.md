---
description: 'Saiba mais sobre: como escutar solicitações de cancelamento que têm identificadores de espera'
title: 'Como: ouvir solicitações de cancelamento que têm identificadores de espera'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cancellation, waiting with wait handles
ms.assetid: 6e2aa49b-fc84-4bcf-962b-17db98b7edcb
ms.openlocfilehash: d38e4892457873b3f918582bf154a6a596e9d361
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99666791"
---
# <a name="how-to-listen-for-cancellation-requests-that-have-wait-handles"></a>Como: ouvir solicitações de cancelamento que têm identificadores de espera

Se um método for bloqueado enquanto ele estiver aguardando que um evento seja sinalizado, ele não poderá verificar o valor do token de cancelamento e responder de maneira oportuna. O primeiro exemplo mostra como resolver esse problema quando você estiver trabalhando com eventos, como <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> que não dão suporte nativamente a estrutura de cancelamento unificado. O segundo exemplo mostra uma abordagem mais simples que usa <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType>, que dá suporte ao cancelamento unificado.  
  
> [!NOTE]
> Se a opção "Apenas Meu Código" estiver habilitada, o Visual Studio em alguns casos interromperá na linha que lança a exceção e exibirá uma mensagem de erro que diz "exceção não tratada pelo código do usuário". Esse erro é benigno. Você pode pressionar F5 para continuar a partir daí e ver o comportamento de tratamento de exceção, demonstrado nos exemplos a seguir. Para impedir que o Visual Studio seja interrompido no primeiro erro, basta desmarcar a caixa de seleção "Apenas Meu Código" em **Ferramentas, Opções, Depuração, Geral**.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa um <xref:System.Threading.ManualResetEvent> para demonstrar como desbloquear identificadores de espera que dão suporte ao cancelamento unificado.  
  
 [!code-csharp[Cancellation#9](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex9.cs#9)]
 [!code-vb[Cancellation#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex9.vb#9)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa um <xref:System.Threading.ManualResetEventSlim> para demonstrar como desbloquear primitivos de coordenação que dão suporte ao cancelamento unificado. A mesma abordagem pode ser usada com outros primitivos de coordenação leves, como <xref:System.Threading.Semaphore>`Slim` e <xref:System.Threading.CountdownEvent>.  
  
 [!code-csharp[Cancellation#10](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex10.cs#10)]
 [!code-vb[Cancellation#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex10.vb#10)]  
  
## <a name="see-also"></a>Consulte também

- [Cancelamento em threads gerenciados](cancellation-in-managed-threads.md)
