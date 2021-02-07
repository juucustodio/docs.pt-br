---
description: 'Saiba mais sobre: Modelo de Dados de Entidade: namespaces'
title: 'Modelo de Dados de Entidade: Namespaces'
ms.date: 03/30/2017
ms.assetid: 98ab4226-bb9f-44e7-af46-61a9b1a4e47c
ms.openlocfilehash: c18178672ebab0e323c9712af2668c3cb92e0300
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672758"
---
# <a name="entity-data-model-namespaces"></a>Modelo de Dados de Entidade: Namespaces

Um namespace no Modelo de Dados de Entidade (EDM) é um contêiner abstrato para [tipos de entidade](entity-type.md), [tipos complexos](complex-type.md)e [associações](association-type.md). Namespaces em EDM são semelhantes aos espaços em uma linguagem de programação: fornecem o contexto para os objetos que contêm e fornecem uma maneira de torne os objetos que têm o mesmo nome (mas estão contidos em namespaces diferentes).  
  
## <a name="example"></a>Exemplo  

 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)(linguagem de definição de esquema conceitual) para definir modelos conceituais. O seguinte código de CSDL usar um namespace para identificar um tipo que é definido em um modelo conceitual diferente. O exemplo define um tipo de entidade (`Publisher`) que tenha uma propriedade do tipo complexo (`Address`) que é importado do espaço de `ExtendedBooksModel` . Observe que o elemento de `Using` indica que um namespace foi importado. Observe também que o tipo da propriedade de `Address` é definido usando seu nome totalmente qualificado (`ExtendedBooksModel.Address`), indicando que esse tipo está definido no namespace de `ExtendedBooksModel` .  
  
 [!code-xml[EDM_Example_Model#ImportedNamespace](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books6.edmx#importednamespace)]  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
