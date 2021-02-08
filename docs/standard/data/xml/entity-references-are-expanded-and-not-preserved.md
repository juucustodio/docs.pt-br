---
description: 'Saiba mais sobre: as referências de entidade são expandidas e não preservadas'
title: Referências a entidades são expandidos e não preservadas
ms.date: 03/30/2017
ms.assetid: ffd97806-ab43-4538-8de2-5828bfbbde57
ms.openlocfilehash: 85152acb8ff91fd8b42f73434a1807fd23ceb2e0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783346"
---
# <a name="entity-references-are-expanded-and-not-preserved"></a>Referências a entidades são expandidos e não preservadas

Quando a referência de entidade é expandida e substituído pelo texto que representa, o nó de **XmlEntityReference** não é criado. Em vez disso, a declaração de entidade é processada e os nós criados na declaração de conteúdo são copiados no lugar de **XmlEntityReference**. Portanto, no exemplo de `&publisher;`, `&publisher;` não é salvo, mas em vez disso, um nó de **XmlText** é criado.  
  
 ![estrutura de árvore expandida](media/xmlentityref-expanded-nodes.gif "xmlentityref_expanded_nodes")  
Estrutura de árvore para as referências de entidade que são expandidas  
  
 As entidades de caractere como `B` ou `<` não são preservados. Em vez disso, sempre são expandidos e representados como nós de texto.  
  
 Para preservar nós **XmlEntityReference** e nós filho da referência de entidade anexada a eles, defina o sinalizador **EntityHandling** como **ExpandCharEntities**. Caso contrário, deixe o sinalizador **EntityHandling** com o padrão, que é **ExpandEntities**. Nesse caso, você não verá nós de referência de entidade em DOM. Os nós são substituídos pelos nós que são cópias dos nós filho da declaração de entidade.  
  
 Um efeito colateral de não preservar referências a entidades é que quando o documento é salvo e passado sobre a outro aplicativo, o aplicativo de receptor não sabe que os nós foram gerados por uma referência de entidade. No entanto, quando as referências a entidades são preservadas, um aplicativo de receptor considera uma referência de entidade e ler os nós filho. É aparente que os nós filhos representam informações que estava na declaração de entidade. Por exemplo, os DOM têm teoricamente a seguinte estrutura se as referências a entidades são preservadas.  
  
 XmlElement: editor  
  
 XmlEntityReference: `&publisher;`  
  
 XmlText: Pressione da Microsoft  
  
 Se as referências a entidades são expandidas em DOM, que é o método padrão, a estrutura tem esse tipo de árvore:  
  
 XmlElement: editor  
  
 XmlText: Pressione da Microsoft  
  
 Observe que o nó de referência de entidade não está mais presente, e o aplicativo receptor não pode determinar que o nó **XmlText** que contém "Microsoft Press" foi criado com base em uma declaração de entidade.  
  
 Se você usar um leitor que não possa resolver entidades, o método **Load** lançará uma exceção quando encontrar uma referência de entidade.  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
