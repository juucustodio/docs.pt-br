---
description: 'Saiba mais sobre: elemento XML e verificação de nome de atributo ao criar novos nós'
title: Verificação de nome de elemento XML e de atributo para criar novos nós
ms.date: 03/30/2017
ms.assetid: b489f647-a175-4659-ada4-170058bb41d0
ms.openlocfilehash: 07b878424df57c34c5dc2b614fdff9a5dcef26bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782709"
---
# <a name="xml-element-and-attribute-name-verification-when-creating-new-nodes"></a>Verificação de nome de elemento XML e de atributo para criar novos nós

O modelo de objeto de documento XML (DOM) verifica a validade de nomes ao criar novos nós ou nós de atributo do elemento. Se os nomes contenham caracteres inválidos, uma exceção é lançada. Para garantir que os nomes sejam válidos e codificados corretamente, você precisa usar a classe **XmlConvert** para codificar o nome e descodificá-lo de volta para o nível de aplicativo. **XmlWriter** tem métodos que realizam trabalho adicional para garantir que XML corretamente formado seja gerado.  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
