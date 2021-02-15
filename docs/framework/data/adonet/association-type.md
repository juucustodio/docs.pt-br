---
description: 'Saiba mais sobre: tipo de associação'
title: tipo de associação
ms.date: 03/30/2017
ms.assetid: 26c409f6-06e8-4441-ac78-1b1076a3c005
ms.openlocfilehash: 4df84d97c798e9f2d06e0f5dce442e05cb4c67b5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697550"
---
# <a name="association-type"></a>tipo de associação

Um *tipo de associação* (também chamado de associação) é o bloco de construção fundamental para descrever relações no modelo de dados de entidade (EDM). Em um modelo conceitual, uma associação representa uma relação entre dois [tipos de entidade](entity-type.md) (como `Customer` e `Order` ). Em um aplicativo, uma instância de uma associação representa uma associação específica (como uma associação entre uma instância de `Customer` e uma instância de `Order`). As instâncias de associação são agrupadas logicamente em um [conjunto de associação](association-set.md).  
  
 Uma definição de associação contém as informações a seguir:  
  
- Um nome exclusivo. (Obrigatória)  
  
- Duas [associações terminam](association-end.md), uma para cada tipo de entidade na relação. (Obrigatória)  
  
    > [!NOTE]
    > Uma associação não pode representar uma relação entre mais de dois tipos de entidade. Uma associação pode, no entanto, definir uma dica relação especificando o mesmo tipo de entidade para cada um das extremidades de associação.  
  
- Uma [restrição de integridade referencial](referential-integrity-constraint.md). (Opcional)  
  
 Cada extremidade de associação deve especificar uma [multiplicidade de extremidade de associação](association-end-multiplicity.md) que indica o número de instâncias de tipo de entidade que podem estar em uma extremidade da associação. Uma multiplicidade de extremidade de associação pode ter um valor de um (1), zero ou um (0.. 1) ou muitos ( \* ). Instâncias de tipo de entidade em uma extremidade de uma associação podem ser acessadas por meio de [Propriedades de navegação](navigation-property.md) ou chaves estrangeiras se forem expostas em um tipo de entidade. Para obter mais informações, consulte [modelo de dados de entidade: chaves estrangeiras](foreign-key-property.md).  
  
## <a name="example"></a>Exemplo  

 O diagrama a seguir mostra um modelo conceitual com duas associações: `PublishedBy` e `WrittenBy`. Terminar a associação para associação de `PublishedBy` são os tipos de entidade de `Book` e de `Publisher` . A multiplicidade do `Publisher` final é um (1) e a multiplicidade do `Book` final é Many ( \* ), indicando que um Publicador publica muitos livros e um livro é publicado por um Publicador.  
  
 ![Modelo de exemplo com três tipos de entidade](./media/association-type/example-model-three-entity-types.gif)  
  
 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)(linguagem de definição de esquema conceitual) para definir modelos conceituais. CSDL seguir define a associação de `PublishedBy` mostrada no diagrama anterior:  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
