---
description: 'Saiba mais sobre: suporte à herança'
title: Suporte à herança
ms.date: 03/30/2017
ms.assetid: 19bb2794-b4e7-402e-8307-1d1517381a08
ms.openlocfilehash: ff6956441ab72f720151e42bd9358c8df1170e09
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803861"
---
# <a name="inheritance-support"></a>Suporte à herança

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dá suporte ao *mapeamento de tabela única*. Ou seja uma hierarquia completa de herança é armazenada em uma única tabela de base de dados. A tabela contém aplainada a união de todas as colunas de dados possíveis para a hierarquia inteira. (Uma União é o resultado da combinação de duas tabelas em uma tabela que tem as linhas que estavam presentes em qualquer uma das tabelas originais.) Cada linha tem nulos nas colunas que não se aplicam ao tipo da instância representada pela linha.  
  
 A estratégia de mapeamento de tabela única é a representação mais simples de herança e fornece características de desempenho bom para várias categorias diferentes de consultas.  
  
 Para implementar esse mapeamento em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], você deve especificar atributos e propriedades de atributo na classe raiz da hierarquia de herança. Para obter mais informações, consulte [como mapear hierarquias de herança](how-to-map-inheritance-hierarchies.md).  
  
 Os desenvolvedores que usam o Visual Studio também podem usar o Object Relational Designer para mapear hierarquias de herança.  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
