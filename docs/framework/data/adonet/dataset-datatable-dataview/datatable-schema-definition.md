---
description: 'Saiba mais sobre: definição de esquema de DataTable'
title: Definição do esquema de DataTable
ms.date: 03/30/2017
ms.assetid: efbcdda4-f5a9-421d-8be2-4c194c74552f
ms.openlocfilehash: b1a48c8a129607dc8d683aa4735ea0e86ed32cc2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652608"
---
# <a name="datatable-schema-definition"></a>Definição do esquema de DataTable

O esquema, ou a estrutura, de uma tabela é representado por colunas e restrições. Você define o esquema de uma <xref:System.Data.DataTable> usando objetos <xref:System.Data.DataColumn>, bem como objetos <xref:System.Data.ForeignKeyConstraint> e <xref:System.Data.UniqueConstraint>. As colunas em uma tabela podem ser mapeadas para colunas em uma fonte de dados, contêm valores calculados de expressões, incrementam automaticamente seus valores ou contêm valores de chave primária.  
  
 As referências por nome a colunas, relações e restrições em uma tabela diferenciam maiúsculas de minúsculas. Duas ou mais colunas, relações ou restrições podem, portanto, existir em uma tabela que tenha o mesmo nome, mas que seja diferente quanto ao uso de maiúsculas e minúsculas. Por exemplo, você pode ter **Col1** e **Col1**. Nesse caso, uma referência a uma das colunas por nome deve corresponder ao uso exato de maiúsculas e minúsculas do nome da coluna; do contrário, uma exceção será lançada. Por exemplo, se a tabela **MyTable** contiver as colunas **Col1** e **Col1**, você referenciará **Col1** por nome como **MyTable. Columns ["Col1"]** e **Col1** como **MyTable. Columns ["Col1"]**. A tentativa de fazer referência a qualquer uma das colunas como **MyTable. Columns ["Col1"]** geraria uma exceção.  
  
 A regra de diferenciação de maiúsculas e minúsculas não se aplicará se houver apenas uma coluna, relação ou restrição com um nome específico. Ou seja, se nenhum outro objeto de coluna, relação ou restrição na tabela corresponder ao nome desse objeto de coluna, relação ou restrição específico, você poderá fazer referência ao objeto por nome usando qualquer uso de maiúsculas e minúsculas, e nenhuma exceção será lançada. Por exemplo, se a tabela tiver apenas **Col1**, você poderá fazer referência a ela usando **My. Colunas ["COL1"]**.  
  
> [!NOTE]
> A <xref:System.Data.DataTable.CaseSensitive%2A> propriedade da **DataTable** não afeta esse comportamento. A propriedade **CaseSensitive** aplica-se aos dados em uma tabela e afeta a classificação, a pesquisa, a filtragem, a imposição de restrições e assim por diante, mas não referências às colunas, relações e restrições.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Adicionando colunas a um DataTable](adding-columns-to-a-datatable.md)  
 Descreve como definir as colunas de uma tabela usando objetos **DataColumn** .  
  
 [Criando colunas de expressão](creating-expression-columns.md)  
 Explica como a propriedade **expression** de uma coluna pode ser usada para calcular valores com base nos valores de outras colunas na linha.  
  
 [Criar colunas AutoIncrement](creating-autoincrement-columns.md)  
 Descreve como uma coluna pode ser definida para incrementar automaticamente valores numéricos para garantir um valor de coluna exclusivo por linha.  
  
 [Definir chaves primárias](defining-primary-keys.md)  
 Descreve como especificar a chave primária de uma tabela de um ou mais objetos de **DataColumn** .  
  
 [Restrições de DataTable](datatable-constraints.md)  
 Descreve como definir a chave estrangeira e restrições exclusivas para colunas em uma tabela.  
  
## <a name="see-also"></a>Consulte também

- [DataTables](datatables.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
