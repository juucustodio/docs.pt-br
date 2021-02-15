---
description: 'Saiba mais sobre: função declarada pelo modelo'
title: função declarada por modelo
ms.date: 03/30/2017
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
ms.openlocfilehash: c9a5cedb8c9706aa0d299635f60f762b92ca6d78
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786258"
---
# <a name="model-declared-function"></a>função declarada por modelo

Uma *função declarada por modelo* é uma função que é declarada em um modelo conceitual, mas não é definida nesse modelo conceitual. A função pode ser definida no ambiente de hospedagem ou de armazenamento. Por exemplo, uma função o declarada pode ser mapeada para uma função que está definida em uma base de dados, bem expõe a funcionalidade do lado do modelo conceitual.  
  
 A declaração de uma função declarada modelo contém as informações a seguir:  
  
- O nome da função. (Obrigatória)  
  
- O tipo do valor de retorno. (Opcional)  
  
    > [!NOTE]
    > Se nenhum valor de retorno for especificado, o tipo de retorno é vago.  
  
- Informações de parâmetro, incluindo o nome do parâmetro e o tipo. (Opcional)  
  
## <a name="example"></a>Exemplo  

 O [Entity Framework ADO.net](./ef/index.md) usa uma DSL (linguagem específica de domínio) chamada[CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)(linguagem de definição de esquema conceitual) para definir modelos conceituais. No CSDL, uma implementação de uma função declarada por modelo é uma importação de função (usando o [elemento FunctionImport](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#functionimport-element-csdl)). CSDL seguir define um contêiner de entidade com uma definição de importação de função. Observe que o tipo de retorno da função é vago desde que nenhum tipo de retorno é especificado.  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
