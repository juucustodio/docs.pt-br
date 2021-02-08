---
description: 'Saiba mais sobre: removendo nós do DOM'
title: Removendo os nós DOM
ms.date: 03/30/2017
ms.assetid: 0a98e0ca-0555-45c1-ab69-0d8d20ca1abd
ms.openlocfilehash: b5e85157c194b034289a46140a44d2a9d1109061
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783086"
---
# <a name="removing-nodes-from-the-dom"></a>Removendo os nós DOM

Para remover um nó de (DOM) modelo de objeto de documento, use o método de <xref:System.Xml.XmlNode.RemoveChild%2A> para remover um nó específico. Quando você remove um nó, o método remove a subárvore que pertence ao nó que está sendo removido; isto é, se não é um nó folha.  
  
 Para remover os vários nós DOM, use o método de <xref:System.Xml.XmlNode.RemoveAll%2A> para remover todos os filhos e atributos, se aplicável, do nó atual.  
  
 Se você estiver trabalhando com <xref:System.Xml.XmlNamedNodeMap>, você pode remover um nó usando o método <xref:System.Xml.XmlNamedNodeMap.RemoveNamedItem%2A> .  
  
 Para remover os atributos, confira [Removendo os atributos de um nó no elemento DOM](removing-attributes-from-an-element-node-in-the-dom.md).  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
