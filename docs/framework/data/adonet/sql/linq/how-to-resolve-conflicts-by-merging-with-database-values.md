---
description: 'Saiba mais sobre: como resolver conflitos mesclando com valores de banco de dados'
title: 'Como: resolver conflitos mesclando com valores de banco de dados'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1988b79c-3bfc-4c5c-a08a-86cf638bbe17
ms.openlocfilehash: 83cae4c98fdd2e51065c66d36ef04202bdc86c9e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767759"
---
# <a name="how-to-resolve-conflicts-by-merging-with-database-values"></a>Como: resolver conflitos mesclando com valores de banco de dados

Para reconciliar diferenças entre valores esperados e reais de base de dados antes que você submeter tente novamente suas alterações, você pode usar <xref:System.Data.Linq.RefreshMode.KeepChanges> para mesclar valores de base de dados com os valores atuais do membro de cliente. Para obter mais informações, consulte [simultaneidade otimista: visão geral](optimistic-concurrency-overview.md).  
  
> [!NOTE]
> Em todos os casos, o registro no cliente é atualizado primeiro recuperando os dados atualizados de base de dados. Esta ação certifique-se de que a seguir tentativa de atualização não falhará nas mesmas verificação de simultaneidade.  
  
## <a name="example"></a>Exemplo  

 Nesse cenário, uma exceção é lançada de <xref:System.Data.Linq.ChangeConflictException> quando tenta User1 para enviar alterações, porque Usuário2 tiver alterado entretanto as colunas do assistente e departamento. A tabela a seguir mostra a situação.  
  
||Gerente|Assistente|department|  
|------|-------------|---------------|----------------|  
|Estado original de base de dados quando consultado por User1 e por Usuário2.|Alfreds|Maria|Sales|  
|User1 prepara-se para enviar essas alterações.|Alfred||Marketing|  
|Usuário2 já tiver enviado essas alterações.||Mary|Serviço|  
  
 User1 decidir resolver esse conflito de mesclagem valores base de dados com os valores atuais do membro de cliente. O resultado é que os valores de base de dados são substituídos somente quando o conjunto de alterações atual também alterou o valor.  
  
 Quando User1 resolver o conflito usando <xref:System.Data.Linq.RefreshMode.KeepChanges>, o resultado na base de dados é como na tabela a seguir:  
  
||Gerente|Assistente|department|  
|------|-------------|---------------|----------------|  
|Novo estado após a resolução do conflito.|Alfred<br /><br /> (de User1)|Mary<br /><br /> (de Usuário2)|Marketing<br /><br /> (de User1)|  
  
 O exemplo a seguir mostra como mesclar valores de base de dados com os valores atuais do membro de cliente (a menos que o cliente também alterou o valor). Nenhuma inspeção ou manipulação personalizada de conflitos de membro individual ocorrem.  
  
 [!code-csharp[System.Data.Linq.RefreshMode#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#3)]
 [!code-vb[System.Data.Linq.RefreshMode#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Como: resolver conflitos substituindo valores de banco de dados](how-to-resolve-conflicts-by-overwriting-database-values.md)
- [Como: resolver conflitos mantendo valores de banco de dados](how-to-resolve-conflicts-by-retaining-database-values.md)
- [Como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md)
