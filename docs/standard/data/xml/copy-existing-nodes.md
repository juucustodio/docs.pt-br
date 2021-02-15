---
description: 'Saiba mais sobre: copiar nós existentes'
title: Copiar nós existentes
ms.date: 03/30/2017
ms.assetid: 2aa8f65c-cc62-4638-9c46-129dc15be786
ms.openlocfilehash: 48bc1fd4f0eeb16691d6f9c0631998db9a54bba1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783424"
---
# <a name="copy-existing-nodes"></a>Copiar nós existentes

Há vários métodos e propriedades no modelo de objeto (DOM) de documento XML você pode usar para selecionar um nó, como **SelectSingleNode**, **ChildNodes[int i]**, **Attributes[int i]**. Uma vez que o nó é selecionado, você pode inseri-lo na árvore usando um dos métodos de inserção que funcionam para esse tipo de nó específico. A única limitação para inserir um nó na árvore é que o documento ainda deve ser bem formado depois que o nó é inserido. Quando um nó existente é inserido na árvore DOM, é removido da sua posição original e adicionado à sua posição de destino.  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
