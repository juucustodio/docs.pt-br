---
description: 'Saiba mais sobre: removendo o conteúdo do nó no DOM'
title: Removendo conteúdo do nó em DOM
ms.date: 03/30/2017
ms.assetid: 615d81a7-f44f-416c-a9ab-bfe03f85e6e4
ms.openlocfilehash: 44f8e0ee63ae8317d6b19558829ff3b676867845
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783112"
---
# <a name="removing-node-content-in-the-dom"></a>Removendo conteúdo do nó em DOM

Para os tipos de nós que herdam de <xref:System.Xml.XmlCharacterData>, que são <xref:System.Xml.XmlComment>, <xref:System.Xml.XmlText>, <xref:System.Xml.XmlCDataSection>, <xref:System.Xml.XmlWhitespace>, e os tipos de nós de <xref:System.Xml.XmlSignificantWhitespace> , você pode remover os caracteres usando o método de <xref:System.Xml.XmlCharacterData.DeleteData%2A> , que remove um intervalo de caracteres de nó. Se você deseja remover completamente o conteúdo, você remover o nó que contém o conteúdo. Se você desejar manter o nó, mas o conteúdo está incorreto, então modificar o conteúdo. Para saber mais sobre como alterar o conteúdo de um nó, confira [Modificando nós, conteúdo e valores em um documento XML](modifying-nodes-content-and-values-in-an-xml-document.md).  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
