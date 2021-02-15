---
description: 'Saiba mais sobre: Personalizando operações: visão geral'
title: 'Personalizar operações: Visão geral'
ms.date: 03/30/2017
ms.assetid: a3546296-1443-4b88-aa6e-d41011041ba7
ms.openlocfilehash: bdcaf482f49b9c55fb7a1834b19b683ac2fa16bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729595"
---
# <a name="customizing-operations-overview"></a>Personalizar operações: Visão geral

Por padrão, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] gera SQL dinâmico para operações de inserção, atualização e exclusão com base no mapeamento. No entanto, na prática, normalmente você desejará adicionar sua própria lógica de negócios para fornecer segurança, validação e assim por diante.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] as técnicas para personalizar essas operações incluem o seguinte.  
  
## <a name="loading-options"></a>Opções de carregamento  

 Nas consultas, você pode controlar como os dados relacionados ao seu destino principal são recuperados quando você se conecta ao base de dados. Essa funcionalidade é implementada amplamente usando <xref:System.Data.Linq.DataLoadOptions>. Para obter mais informações, veja [carregamento deferido versus imediato](deferred-versus-immediate-loading.md).  
  
## <a name="partial-methods"></a>Métodos parciais  

 No mapeamento padrão, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornece métodos parciais para ajudá-lo a implementar a lógica corporativa. Para obter mais informações, consulte [adicionando lógica de negócios usando métodos parciais](adding-business-logic-by-using-partial-methods.md).  
  
## <a name="stored-procedures-and-user-defined-functions"></a>Procedimentos e funções definidas pelo usuário armazenados  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dá suporte ao uso de procedimentos armazenados e funções definidas pelo usuário. Os procedimentos armazenados são usados para personalizar operações. Para obter mais informações, consulte [Procedimentos armazenados](stored-procedures.md).  
  
## <a name="see-also"></a>Consulte também

- [Personalizando a inserção, atualiazação, e as operações de exclusão](customizing-insert-update-and-delete-operations.md)
