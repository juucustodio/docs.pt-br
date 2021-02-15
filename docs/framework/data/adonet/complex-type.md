---
description: 'Saiba mais sobre: tipo complexo'
title: tipo complexo
ms.date: 03/30/2017
ms.assetid: 63efbd23-11d4-4871-bc88-ad01b9837553
ms.openlocfilehash: 06bb6f54f488e4c6038382707a2ad3e85f000bc2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663892"
---
# <a name="complex-type"></a>tipo complexo

Um *tipo complexo* é um modelo para definir propriedades ricas e estruturadas em [tipos de entidade](entity-type.md) ou em outros tipos complexos. Cada modelo contém o seguinte:  
  
- Um nome exclusivo. (Obrigatória)  
  
    > [!NOTE]
    > O nome de um tipo complexo não pode ser o mesmo que um nome de tipo de entidade dentro do mesmo namespace.  
  
- Dados na forma de uma ou mais [Propriedades](property.md). (Opcional).  
  
    > [!NOTE]
    > Uma propriedade de um tipo complexo pode ser outro tipo complexo.  
  
 Um tipo complexo é semelhante a um tipo de entidade que um tipo complexo pode levar uma carga útil de dados na forma das propriedades do tipo primitivo ou outros tipos complexos. No entanto, há algumas diferenças entre tipos complexos e tipos de entidade:  
  
- Os tipos complexos não têm identidades e portanto não podem existir independente. Os tipos complexos podem existir somente como propriedades em tipos de entidade ou em outros tipos complexos.  
  
- Tipos complexos não podem participar de [associações](association-type.md). Nenhuma extremidade de uma associação pode ser um tipo complexo e, portanto, [as propriedades de navegação](navigation-property.md) não podem ser definidas em tipos complexos.  
  
## <a name="example"></a>Exemplo  

 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)(linguagem de definição de esquema conceitual) para definir modelos conceituais. CSDL seguir define um tipo complexo, endereço, com as propriedades `StreetAddress`, `City`, `StateOrProvince`, `Country`, e `PostalCode`de tipo primitivo.  
  
 [!code-xml[EDM_Example_Model#ComplexTypeExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#complextypeexample)]  
  
 Para definir o tipo complexo `Address` (acima) como uma propriedade em um tipo de entidade, você deve declarar a propriedade na definição de tipo de entidade. CSDL seguir declara a propriedade de `Address` como um tipo complexo em um tipo de entidade (Publisher):  
  
 [!code-xml[EDM_Example_Model#EntityWithComplexType](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#entitywithcomplextype)]  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
