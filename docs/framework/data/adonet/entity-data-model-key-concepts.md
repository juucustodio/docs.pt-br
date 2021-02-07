---
description: 'Saiba mais sobre: Modelo de Dados de Entidade conceitos principais'
title: Conceitos chave do Modelo de Dados de Entidade
ms.date: 03/30/2017
ms.assetid: c635a16d-6674-45aa-9344-dcb7df992bab
ms.openlocfilehash: 4b97a39a5989689662db7be92b259b9a08d84cc7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672786"
---
# <a name="entity-data-model-key-concepts"></a>Conceitos chave do Modelo de Dados de Entidade

O Modelo de Dados de Entidade (EDM) usa três conceitos principais para descrever a estrutura de dados: *tipo de entidade*, *tipo de associação* e *Propriedade*. Esses são os conceitos mais importantes para descrever a estrutura dos dados em qualquer implementação do EDM.  
  
## <a name="entity-type"></a>Tipo de entidade  

 O [tipo de entidade](entity-type.md) é o bloco de construção fundamental para descrever a estrutura de dados com o modelo de dados de entidade. Em um modelo conceitual, os tipos de entidade são construídos a partir de [Propriedades](property.md) e descrevem a estrutura de conceitos de nível superior, como clientes e pedidos em um aplicativo de negócios. Da mesma forma que uma definição de classe em um programa de computador é um modelo para instâncias da classe, um tipo de entidade é um modelo para entidades. Uma entidade representa um objeto específico (como um cliente ou um pedido específico.) Cada entidade deve ter uma [chave de entidade](entity-key.md) exclusiva dentro de um [conjunto de entidades](entity-set.md).  Um conjunto de entidades é uma coleção de instâncias de um tipo de entidade específico. Conjuntos de entidades (e [conjuntos de associação](association-set.md)) são logicamente agrupados em um contêiner de [entidade](entity-container.md).  
  
 A herança é suportada com tipos de entidade: isto é, um tipo de entidade pode ser derivado de outro. Para obter mais informações, consulte [modelo de dados de entidade: herança](entity-data-model-inheritance.md).  
  
## <a name="association-type"></a>Tipo de associação  

 Um [tipo de associação](association-type.md) (também chamado de associação) é o bloco de construção fundamental para descrever relações no modelo de dados de entidade. Em um modelo conceitual, uma associação representa uma relação entre dois tipos de entidade (como cliente e pedido). Cada associação tem duas [extremidades de associação](association-end.md) que especificam os tipos de entidade envolvidos na associação. Cada extremidade de associação também especifica uma [multiplicidade de extremidade de associação](association-end-multiplicity.md) que indica o número de entidades que podem estar nessa extremidade da associação. Uma multiplicidade de extremidade de associação pode ter um valor de um (1), zero ou um (0.. 1) ou muitos ( \* ). As entidades em uma extremidade de uma associação podem ser acessadas por meio de [Propriedades de navegação](navigation-property.md)ou por meio de chaves estrangeiras se forem expostas em um tipo de entidade. Para obter mais informações, consulte [Propriedade Foreign Key](foreign-key-property.md).  
  
 Em um aplicativo, uma instância de uma associação representa uma associação específica (como uma associação entre uma instância de cliente e instâncias de pedido). As instâncias de associação são agrupadas logicamente em um [conjunto de associação](association-set.md). Os conjuntos de associação (e [conjuntos de entidades](entity-set.md)) são logicamente agrupados em um [contêiner de entidade](entity-container.md).  
  
## <a name="property"></a>Propriedade  

 Os [tipos de entidade](entity-type.md) contêm [Propriedades](property.md) que definem sua estrutura e características. Por exemplo, um tipo de entidade de cliente pode ter propriedades como CustomerId, Name e Address.  
  
 As propriedades em um modelo conceitual são análogas às propriedades definidas em uma classe em um programa de computador. Da mesma forma que as propriedades em uma classe definem a forma da classe e transportam informações sobre objetos, as propriedades em um modelo conceitual definem a forma de um tipo de entidade e transportam informações sobre as instâncias dos tipos de entidade.  
  
 Uma propriedade pode conter dados primitivos (como uma cadeia de caracteres, um número inteiro ou um valor booliano) ou dados estruturados (como um tipo complexo). Para obter mais informações, consulte [modelo de dados de entidade: tipos de dados primitivos](entity-data-model-primitive-data-types.md).  
  
## <a name="representations-of-a-conceptual-model"></a>Representações de um modelo conceitual  

 Um *modelo conceitual* é uma representação específica da estrutura de alguns dados como entidades e relações. Uma maneira de representar um modelo conceitual é com um diagrama. O diagrama a seguir representa um modelo conceitual com três tipos de entidade (`Book`, `Publisher` e `Author`) e duas associações (`PublishedBy` e `WrittenBy`):  
  
 ![Diagrama mostrando um modelo conceitual com três tipos de entidade.](./media/entity-data-model-key-concepts/conceptual-model-entity-types-associations.gif)  
  
 Essa representação, no entanto, tem alguns defeitos quando se trata de transmitir alguns detalhes sobre o modelo. Por exemplo, o tipo de propriedade e as informações do conjunto de entidades não são transportados no diagrama. A sofisticação de um modelo conceitual pode ser transmitida mais claramente com um DSL (linguagem específica do domínio). O [Entity Framework ADO.net](./ef/index.md) usa uma DSL baseada em XML chamada *linguagem de definição de esquema conceitual* ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) para definir modelos conceituais. O seguinte é a definição CSDL do modelo conceitual no diagrama anterior:  
  
 [!code-xml[EDM_Example_Model#EDMExampleCSDL](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#edmexamplecsdl)]  
  
## <a name="see-also"></a>Consulte também

- [Modelo de Dados de Entidade](entity-data-model.md)
