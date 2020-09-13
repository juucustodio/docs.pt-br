---
title: Programação funcional vs. de procedimentos
description: O LINQ to XML dá suporte à construção funcional e técnicas de procedimento para a criação de aplicativos XML. A construção funcional é uma abordagem declarativa. As técnicas de procedimento dão suporte à modificação na memória de árvores XML.
ms.date: 07/20/2015
ms.assetid: fc64e39c-a487-4882-9169-da4de97917d9
ms.openlocfilehash: a2753a31e88fd338dad61063f559431869b9e17f
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551877"
---
# <a name="functional-vs-procedural-programming-linq-to-xml"></a>Programação funcional vs. de procedimentos (LINQ to XML)

Há vários tipos de aplicativos XML:

- Alguns aplicativos utilizam documentos XML de origem e geram novos documentos XML que estão em um formato diferente do que os documentos de origem.
- Alguns aplicativos utilizam documentos XML de origem e produzem documentos de resultado em um formato totalmente diferente, como arquivos de texto HTML ou CSV.
- Alguns aplicativos utilizam documentos XML de origem e inserem registros em um banco de dados.
- Alguns aplicativos utilizam dados de outra origem, como um banco de dados e criam documentos XML a partir deles.

Esses não são todos os tipos de aplicativos XML, mas são um conjunto representativo dos tipos de funcionalidade que um programador de XML precisa implementar.

Com todos esses tipos de aplicativos, há duas abordagens contrastantes que um desenvolvedor pode utilizar:

- Construção funcional usando uma abordagem declarativa.
- Modificação da árvore XML na memória usando código procedural.

O LINQ to XML oferece suporte às duas abordagens.

Ao usar a abordagem funcional, você escreve as transformações que utilizam os documentos de origem e geram documentos de resultado completamente novos com o formato desejado.

Ao modificar uma árvore XML no lugar, você escreve o código que percorre e navega por meio de nós em uma árvore XML na memória, inserindo, excluindo e modificando os nós conforme o necessário.

Você pode usar LINQ to XML com qualquer abordagem. Você usa as mesmas classes e, em alguns casos, os mesmos métodos. No entanto, a estrutura e os objetivos das duas abordagens são diferentes. Por exemplo, em situações diferentes, uma ou outra abordagem terá geralmente melhor desempenho, e usará mais ou menos memória. Além disso, uma ou outra abordagem será mais fácil de escrever e produzirá um código mais sustentável.

Para ver as duas abordagens contrastadas, consulte [modificação da árvore XML na memória versus construção funcional](in-memory-xml-tree-modification-vs-functional-construction.md).

Para obter um tutorial sobre como escrever transformações funcionais, consulte [introdução às transformações funcionais puras](introduction-pure-functional-transformations.md).
