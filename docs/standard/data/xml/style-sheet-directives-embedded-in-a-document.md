---
description: 'Saiba mais sobre: diretivas de folha de estilo inseridas em um documento'
title: Diretivas de folha de estilos inseridas em um documento
ms.date: 03/30/2017
ms.assetid: d79fb295-ebc7-438d-ba1b-05be7d534834
ms.openlocfilehash: 3585cc2f9e7d931a89c1f81283282712195720f0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782930"
---
# <a name="style-sheet-directives-embedded-in-a-document"></a>Diretivas de folha de estilos inseridas em um documento

Ocasionalmente, existir XML contém a política de folha de estilos de `<?xml:stylesheet?>`. O Microsoft Internet Explorer aceita isso como uma alternativa à sintaxe `<?xml-stylesheet?>`. Quando os dados XML contém uma diretiva de `<?xml:stylesheet?>` , conforme mostrado nos seguintes dados, tentando carregar esses dados no modelo de objeto de documento XML (DOM) palavras-chave acionar uma exceção.

```xml
<?xml version="1.0" ?>
<?xml:stylesheet type="text/xsl" href="test2.xsl"?>
<root>
    <test>Node 1</test>
    <test>Node 2</test>
</root>
```

Isso ocorre porque `<?xml:stylesheet?>` é considerado um **ProcessingInstruction** inválido para DOM. Qualquer **ProcessingInstruction**, de acordo com os namespaces na especificação XML, só pode ser nomes de sem dois-pontos (NCNames), diferentemente de nomes qualificados (QNames).

Conforme a seção 6 de Namespaces na especificação XML, o efeito de fazer os métodos **Load** e **LoadXml** obedecerem à especificação é que, em um documento:

- Todos os tipos de elemento e nomes de atributo contêm zero ou mais pontos.

- Nenhum nome de entidade, destino de ProcessingInstruction, ou nome de notação contém todos os dois-pontos.

Com `<?xml:stylesheet?>` que contém dois-pontos, você agora viola a regra no segundo marcador.

De acordo com a recomendação [Associating Style Sheets with XML documents Version 1.0 Recommendation](https://www.w3.org/TR/xml-stylesheet/) (Associando folhas de estilos a documentos XML versão 1.0) do W3C (World Wide Web Consortium), a instrução de processamento para associar uma folha de estilos XSLT a um documento XML é `<?xml-stylesheet?>`, com um traço substituindo dois-pontos.

## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
