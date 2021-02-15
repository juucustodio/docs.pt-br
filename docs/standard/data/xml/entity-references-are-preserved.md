---
description: 'Saiba mais sobre: as referências de entidade são preservadas'
title: Referências a entidades são preservadas
ms.date: 03/30/2017
ms.assetid: 000a6cae-5972-40d6-bd6c-a9b7d9649b3c
ms.openlocfilehash: 189096d2dd87731a06fdb805ba5f041c041e26b9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99629624"
---
# <a name="entity-references-are-preserved"></a>Referências a entidades são preservadas

Quando a referência de entidade não é expandida, mas é preservada, o modelo de objeto (DOM) de documento XML cria um nó de **XmlEntityReference** quando encontra uma referência de entidade.  
  
 Usando o seguinte XML,  
  
```xml  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 o DOM cria um nó **XmlEntityReference** quando encontra a referência `&publisher;`. **XmlEntityReference** contém os nós filho copiados de conteúdo na declaração de entidade. O exemplo de código anterior contém o texto na declaração de entidade. Assim, um nó **XmlText** é criado como o nó filho do nó de referência de entidade.  
  
 ![Estrutura de árvore para referências de entidade preservadas](media/xmlentityref-notexpanded-nodes.gif "xmlentityref_notexpanded_nodes")  
Estrutura de árvore para as referências de entidade que são preservadas  
  
 Os nós filho de **XmlEntityReference** são cópias de todos os nós filho criados do nó **XmlEntity** quando a declaração de entidade foi encontrada.  
  
> [!NOTE]
> Os nós copiados de **XmlEntity** não são sempre cópias exatas quando colocados no nó de referência de entidade. Pode haver namespaces que estão no escopo no nó de referência de entidade, e que afetam a configuração final dos nós filho.  
  
 Por padrão, entidades gerais como `&abc;` são preservadas, e nós **XmlEntityReference** são sempre criados.  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
