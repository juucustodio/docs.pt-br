---
description: 'Saiba mais sobre: implementação de comportamentos discricionários na classe XslTransform'
title: Implementação de comportamentos arbitrários na classe XslTransform
ms.date: 03/30/2017
ms.assetid: d2758ea1-03f6-47bd-88d2-0fb7ccdb2fab
ms.openlocfilehash: 56936183f635a002d2226bd8e91a6539308259e5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99713748"
---
# <a name="implementation-of-discretionary-behaviors-in-the-xsltransform-class"></a>Implementação de comportamentos arbitrários na classe XslTransform

> [!NOTE]
> A classe <xref:System.Xml.Xsl.XslTransform> está obsoleta no .NET Framework 2.0. Você pode executar a linguagem XSL Transformations (XSLT) usando a classe <xref:System.Xml.Xsl.XslCompiledTransform>. Confira [Usar a classe XslCompiledTransform](using-the-xslcompiledtransform-class.md) e [Migrar da classe XslTransform](migrating-from-the-xsltransform-class.md) para saber mais.

Os comportamentos discricionários são descritos como os comportamentos listados em [World Wide Web Consortium (W3C) XSL Transformations (XSLT) Version 1.0 Recommendation](https://www.w3.org/TR/1999/REC-xslt-19991116) [Recomendação de XSLT (XSL Transformations) do W3C (World Wide Web Consortium) Versão 1.0], nos quais o provedor de implementação escolhe uma das várias opções possíveis como uma maneira de lidar com uma situação. Por exemplo, em instruções de processamento criadoras da seção 7,3, a recomendação W3C informa que é um erro se criar uma instância do conteúdo de `xsl:processing-instruction` cria nós diferentes de nós de texto. Para alguns problemas, W3C informa o que a decisão deve ser feita se o processador decidir recuperar de erro. Para o problema da seção 7,3, o W3C com a implementação pode recuperar esse erro ignorando os nós e seu conteúdo.

Portanto, porque cada um dos comportamentos arbitrários permitidos pelo W3C, a tabela abaixo lista os comportamentos arbitrários implementados para a implementação do .NET Framework da classe de <xref:System.Xml.Xsl.XslTransform>, e que na seção recomendação W3C XSLT 1,0 que esse problema é discutido.

|Problema|Comportamento|Seção|
|-------------|--------------|-------------|
|Um nó de texto corresponde `xsl:strip-space` e `xsl:preserve-space`.|Recuperar|3.4|
|Um nó de origem corresponde mais de uma regra de modelo.|Recuperar|5.5|
|Um namespace Uniform Resource Identifier (URI) é declarada para ser um alias para vários namespace URIs, tudo que tem o mesmo precedência de importação.|Recuperar|7.1.1|
|O nome do atributo em `xsl:attribute` e em `xsl:element` gerado de um modelo de valor de atributo não é um nome qualificado válido (QName).|Exceção lançada|7.1.2 e 7.1.3|
|Adicionando um atributo a um elemento após os nós filho já foram adicionados ao nó do elemento.|Recuperar|7.1.3|
|Adicionando um atributo a algo diferente de um nó de elemento.|Recuperar|7.1.3|
|A instanciação do conteúdo de um elemento de `xsl:attribute` não é um nó de texto.|Recuperar|7.1.3|
|Dois conjuntos de atributo tem a mesma precedência de importação e nome expandido. Têm o mesmo atributo, e não há nenhum outro atributo definida que contém o atributo comum com o mesmo nome com importância mais alta.|Recuperar|7.1.4|
|o atributo de nome de`xsl:processing-instruction` não produz um nome de sem dois-pontos (NCName) e um destino de instrução de processamento.|Recuperar|7.3|
|Criar uma instância do conteúdo de `xsl:processing-instruction` cria nós diferentes de nós de texto.|Recuperar|7.3|
|Os resultados de criar uma instância do conteúdo de `xsl:processing-instruction` contêm a cadeia de caracteres “`?>`”.|Recuperar|7.3|
|Os resultados de instanciar o conteúdo de `xsl:comment` contêm a cadeia de caracteres "--" ou terminam com "-".|Recuperar|7.4|
|Os resultados de criar uma instância do conteúdo de `xsl:comment` criar nós diferentes de nós de texto.|Recuperar|7.4|
|O modelo dentro de um elemento de variável associação retorna um nó de atributo ou um nó de namespace.|Recuperar|11.2|
|Há um erro que recupera o recurso URI passado na função do documento.|Exceção lançada|12.1|
|A referência URI na função do documento contém um identificador de fragmento, e há um erro que processa o identificador do fragmento.|Exceção lançada|12.1|
|Há vários atributos com o mesmo nome que não são nomeados `cdata-section-elements` em `xls:output`, e esses atributos têm a mesma precedência de importação.|Recuperar|16|
|O processador não oferece suporte ao valor de codificação de caracteres fornecido no atributo de `encoding` do elemento de `xsl:output` .|Recuperar|16.1|
|`disable-output-escaping` é usado para um nó de texto, e o nó de texto é usado para criar algo diferente de um nó de texto na árvore de resultado.|o atributo de`disable-output-escaping` é ignorado|16.4|
|Convertendo uma árvore de resultado fragmente a um número ou cadeia se o fragmento da árvore de resultado contém um nó de texto com o escape de saída ativado.|Ignored|16.4|
|O escape de saída é desativado para os caracteres que não podem ser representados na codificação que o processador XSLT está usando para saída.|Ignored|16.4|
|Adicionando um nó de namespace para um elemento após os filhos lhe foram adicionados ou após os atributos lhe foram adicionados|Recuperar|Erratas e25|
|`xsl:number` é NaN, interminável, ou menor que 0,5.|Recuperar|Erratas e24|
|O segundo argumento nó- definida como a função do documento está vazia e a referência URI é relativo|Recuperar|Erratas e14|

As seções da errata podem ser encontradas em [XSL Transformations (XSLT) Version 1.0 Specification Errata](https://www.w3.org/1999/11/REC-xslt-19991116-errata/) [Erratas de especificação de XSLT (XSL Transformations) Versão 1.0] do W3C.

## <a name="custom-defined-implementation-behaviors"></a>Comportamentos definidos de implementação personalizada

Há comportamentos exclusivos para a implementação da classe de <xref:System.Xml.Xsl.XslTransform> . Esta seção discutem a implementação específica do provedor de `xsl:sort` e recursos opcionais que são suportados pela classe de <xref:System.Xml.Xsl.XslTransform> .

## <a name="xslsort"></a>xsl:sort

Ao usar uma transformação para classificar, a recomendação W3C XSLT 1,0 faça algumas observações. Eles são:

- Dois processadores XSLT podem ser processadores de conformação, mas ainda podem classificar diferente.

- Nem todos os processadores XSLT suportam os mesmos idiomas.

- Em relação aos processadores, linguagens diferentes podem variar em sua classificação em um idioma específico não especificado em `xsl:sort.`

A tabela a seguir mostra o comportamento de classificação implementado para cada tipo de dados na implementação de uma transformação do .NET Framework usando <xref:System.Xml.Xsl.XslTransform>:

|Tipo de dados|Comportamento de classificação|
|---------------|----------------------|
|Texto|Os dados são classificados usando o método Common Language Runtime (CLR) String.Compare, e a localidade cultural. Quando o tipo de dados é igual a “texto”, classificação na classe de <xref:System.Xml.Xsl.XslTransform> se comporta de forma idêntica os comportamentos de comparação de cadeia de caracteres de CLR.|
|Número|Os valores numéricos são tratados como números XPath (linguagem XPath) e classificados de acordo com os detalhes descritos em [XML Path Language (XPath) Version 1.0 Recommendation, Section 3.5](https://www.w3.org/TR/1999/REC-xpath-19991116/#numbers) [Recomendação de XPath (linguagem XPath) Versão 1.0, Seção 3.5] do W3C.|

## <a name="optional-features-supported"></a>Recursos opcionais suportados

A tabela a seguir mostra os recursos que são opcionais para um processador XSLT implementa e é implementada na classe de <xref:System.Xml.Xsl.XslTransform> .

|Recurso|Local de referência|Observações|
|-------------|------------------------|-----------|
|atributo de`disable-output-escaping` em `<xsl:text...>` e em marcas de `<xsl:value-of...>` .|Recomendação W3C XSLT, 1,0<br /><br /> Seção 16,4|O atributo de `disable-output-escaping` é ignorado quando os elementos de `xsl:text` ou de `xsl:value-of` são usados em `xsl:comment`, em `xsl:processing-instruction`, ou no elemento de `xsl:attribute` .<br /><br /> Os fragmentos da árvore de resultado que contêm texto e saída de texto que foram de escape não são suportados.<br /><br /> O atributo de escape é ignorado quando uma transformação a <xref:System.Xml.XmlReader> ou <xref:System.Xml.XmlWriter> objetos.|

## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Xsl.XslTransform>
- [A classe XslTransform implementa do processador XSLT](xsltransform-class-implements-the-xslt-processor.md)
- [Transformações XSLT com a classe XslTransform](xslt-transformations-with-the-xsltransform-class.md)
- [XPathNavigator nas transformações](xpathnavigator-in-transformations.md)
- [XPathNodeIterator nas transformações](xpathnodeiterator-in-transformations.md)
- [XPathDocument inseriu a XslTransform](xpathdocument-input-to-xsltransform.md)
- [XmlDataDocument inseriu a XslTransform](xmldatadocument-input-to-xsltransform.md)
- [XmlDocument inseriu a XslTransform](xmldocument-input-to-xsltransform.md)
