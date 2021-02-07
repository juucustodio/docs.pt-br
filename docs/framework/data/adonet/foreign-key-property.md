---
description: 'Saiba mais sobre: propriedade de chave estrangeira'
title: propriedade de chave estrangeira
ms.date: 03/30/2017
ms.assetid: 23cb6729-544d-4f67-9ee7-44e8a6545587
ms.openlocfilehash: 1666e4477c09dd5d0ed3d2c35a93ca21824e8a0e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724122"
---
# <a name="foreign-key-property"></a>propriedade de chave estrangeira

Uma *propriedade de chave estrangeira* no modelo de dados de entidade (EDM) é uma [Propriedade](property.md) de tipo primitivo (ou um conjunto de propriedades de tipo primitivo) em um [tipo de entidade](entity-type.md) que contém a chave de [entidade](entity-key.md) de outro tipo de entidade.  
  
 Uma propriedade de chave externa é análogo a uma coluna de chave externa em uma base de dados relacional. Da mesma forma que as colunas de chave estrangeira são usadas em um banco de dados relacional para criar relações entre linhas em tabelas, as propriedades de chave estrangeira em um modelo conceitual são usadas para estabelecer [associações](association-type.md) entre tipos de entidade. Uma [restrição de integridade referencial](referential-integrity-constraint.md) é usada para definir uma associação entre dois tipos de entidade quando um dos tipos tem uma propriedade de chave estrangeira.  
  
## <a name="example"></a>Exemplo  

 O diagrama a seguir mostra um modelo conceitual com três tipos de entidade: `Book`, `Publisher`, e `Author`. O tipo de entidade de `Book` tem uma propriedade, `PublisherId`, que faz referência a chave de entidade do tipo de entidade de `Publisher` quando você define uma restrição de integridade referencial em associação de `PublishedBy` .  
  
 ![RefConstraintModel](./media/foreign-key-property/reference-constraint-model.gif "Exemplo de um modelo de restrição referencial")  
  
 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)(linguagem de definição de esquema conceitual) para definir modelos conceituais. CSDL seguir usa a propriedade `PublisherId` de chave externa para definir uma restrição de integridade referencial em associação de `PublishedBy` mostrada no modelo conceitual mostrado acima.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
