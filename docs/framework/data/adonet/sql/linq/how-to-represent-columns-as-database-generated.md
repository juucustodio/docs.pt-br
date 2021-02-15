---
description: 'Saiba mais sobre: como representar colunas como Database-Generated'
title: 'Como: declarar colunas como geradas por banco de dados'
ms.date: 03/30/2017
ms.assetid: 6524b8a6-e5d2-4a3b-8e08-beafc4a84fd2
ms.openlocfilehash: 01828ef3f73257d20023168f0ea471ee7e3863c5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695626"
---
# <a name="how-to-represent-columns-as-database-generated"></a>Como: declarar colunas como geradas por banco de dados

Use a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> propriedade no <xref:System.Data.Linq.Mapping.ColumnAttribute> atributo para designar um campo ou propriedade como representando uma coluna gerada pelo banco de dados.  
  
 Para exemplos de código, consulte <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>.  
  
### <a name="to-designate-a-field-or-property-as-representing-a-database-generated-column"></a>Para designar um campo ou propriedade como a representação de uma coluna base de dados - gerado  
  
1. Adicione a propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> ao atributo de <xref:System.Data.Linq.Mapping.ColumnAttribute> .  
  
2. Defina o valor da propriedade `true`.  
  
## <a name="see-also"></a>Consulte também

- [Modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md)
- [Como: personalizar classes de entidade usando o editor de códigos](how-to-customize-entity-classes-by-using-the-code-editor.md)
