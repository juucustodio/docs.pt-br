---
description: 'Saiba mais sobre: como especificar quais membros são testados para conflitos de simultaneidade'
title: 'Como: especificar quais membros são testados quanto a conflitos de simultaneidade'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d2cda293-1e2f-4878-af0e-5aaf0d092120
ms.openlocfilehash: f2623c1e6afcf97ee2de62b94b80145ca2a5cad3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785843"
---
# <a name="how-to-specify-which-members-are-tested-for-concurrency-conflicts"></a>Como: especificar quais membros são testados quanto a conflitos de simultaneidade

Aplique uma das três enums à [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> propriedade em um <xref:System.Data.Linq.Mapping.ColumnAttribute> atributo para especificar quais membros devem ser incluídos nas verificações de atualização para a detecção de conflitos de simultaneidade otimista.  
  
 A propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> (mapeada em tempo de design) é usada junto com recursos de simultaneidade de tempo de execução em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Para obter mais informações, consulte [simultaneidade otimista: visão geral](optimistic-concurrency-overview.md).  
  
> [!NOTE]
> Os valores membro original são comparados com o estado atual de base de dados como nenhum membro é designado como `IsVersion=true`. Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>.  
  
 Para exemplos de código, consulte <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>.  
  
### <a name="to-always-use-this-member-for-detecting-conflicts"></a>Para usar sempre esse membro para detectar conflitos  
  
1. Adicione a propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> ao atributo de <xref:System.Data.Linq.Mapping.ColumnAttribute> .  
  
2. Definir o valor da propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> a `Always`.  
  
### <a name="to-never-use-this-member-for-detecting-conflicts"></a>Para usar nunca esse membro para detectar conflitos  
  
1. Adicione a propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> ao atributo de <xref:System.Data.Linq.Mapping.ColumnAttribute> .  
  
2. Definir o valor da propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> a `Never`.  
  
### <a name="to-use-this-member-for-detecting-conflicts-only-when-the-application-has-changed-the-value-of-the-member"></a>Para usar este membro para detectar conflitos somente quando o aplicativo altere o valor do membro  
  
1. Adicione a propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> ao atributo de <xref:System.Data.Linq.Mapping.ColumnAttribute> .  
  
2. Definir o valor da propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> a `WhenChanged`.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir especifica que os objetos de `HomePage` nunca devem ser testados durante verificações de atualização. Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>.  
  
 [!code-csharp[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.mapping.updatecheck/cs/northwind.cs#1)]
 [!code-vb[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.mapping.updatecheck/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md)
- [Fazendo e enviando alterações de dados](making-and-submitting-data-changes.md)
