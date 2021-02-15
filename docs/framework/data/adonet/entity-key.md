---
description: 'Saiba mais sobre: chave de entidade'
title: chave de entidade
ms.date: 03/30/2017
ms.assetid: 0d447a6d-fa7a-4db0-8e7a-fd45e385fca0
ms.openlocfilehash: 588f18a2f76ca11c797b9b2aaab00b090c99e345
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724434"
---
# <a name="entity-key"></a>chave de entidade

Uma *chave de entidade* é uma [Propriedade](property.md) ou um conjunto de propriedades de um [tipo de entidade](entity-type.md) que são usadas para determinar a identidade. As propriedades que compõem uma chave de entidade são escolhidas em tempo de design. Os valores das propriedades de chave de entidade devem identificar exclusivamente uma instância de tipo de entidade dentro de uma [entidade definida](entity-set.md) em tempo de execução. As propriedades que compõem uma chave de entidade devem ser escolhidas para garantir a exclusividade de instâncias em um conjunto de entidades.  
  
 A seguir estão os requisitos para um conjunto de propriedades ser uma chave de entidade:  
  
- Nenhuma chave de duas entidades em um conjunto de entidades pode ser idêntica. Ou seja, para as duas entidades em um conjunto de entidades, os valores para todas as propriedades que constituem uma chave não podem ser os mesmos. No entanto, alguns (mas não todos os valores) que compõem uma chave de entidade podem ser os mesmos.  
  
- Uma chave de entidade deve consistir em um conjunto de [Propriedades de tipo primitivos](entity-data-model-primitive-data-types.md), imutáveis e não anuláveis.  
  
- As propriedades que compõem uma chave de entidade para um tipo de dado entidade não pode ser alterado. Você não pode permitir mais de uma chave possível de entidade para um tipo de dado; entidade as chaves substitutas não são suportadas.  
  
- Quando uma entidade é empacotada em uma hierarquia de herança, a entidade raiz deve conter todas as propriedades que compõem a chave de entidade, e a chave de entidade deve ser definida no tipo de entidade raiz. Para obter mais informações, consulte [modelo de dados de entidade: herança](entity-data-model-inheritance.md).  
  
## <a name="example"></a>Exemplo  

 O diagrama a seguir mostra um modelo conceitual com três tipos de entidade: `Book`, `Publisher`, e `Author`. As propriedades de cada tipo de entidade que compõem sua chave de entidade são denotadas com chave (“”). Observe que o tipo de entidade de `Author` tem uma chave de entidade que consiste em duas propriedades, `Name` e `Address`.  
  
 ![Modelo de exemplo com três tipos de entidade](./media/entity-key/example-model-three-entity-types.gif)  
  
 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)(linguagem de definição de esquema conceitual) para definir modelos conceituais. CSDL a seguir define o tipo de entidade de `Book` mostrado no diagrama anterior. Observe que a chave de entidade é definida pela propriedade de `ISBN` do tipo de objeto.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 A propriedade de `ISBN` é uma boa opção para a chave de entidade como um número de livro (ISBN) de padrão internacional identifica um livro.  
  
 CSDL a seguir define o tipo de entidade de `Author` mostrado no diagrama anterior. Observe que a chave de entidade consiste em duas propriedades, `Name` e `Address`.  
  
 [!code-xml[EDM_Example_Model#CompositeKeyExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#compositekeyexample)]  
  
 Usar `Name` e `Address` para a chave de entidade é uma opção razoável, porque dois autores de mesmo nome é improvável de viver no mesmo endereço. No entanto, esta opção para uma chave de entidade não garante absolutamente chaves exclusivas de entidade em um conjunto de entidades. Adicione uma propriedade, como `AuthorId`, que pode ser usado para identificar exclusivamente um autor seria recomendado nesse caso.  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
