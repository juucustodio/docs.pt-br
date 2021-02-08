---
description: 'Saiba mais sobre: fragmento de árvore de resultados em transformações'
title: Fragmento da árvore de resultado nas transformações
ms.date: 03/30/2017
ms.assetid: df363480-ba02-4233-9ddf-8434e421c4f1
ms.openlocfilehash: 6f3d0b561fcca57b81d154cfc21dcee05e866230
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783034"
---
# <a name="result-tree-fragment-in-transformations"></a>Fragmento da árvore de resultado nas transformações

> [!NOTE]
> A classe <xref:System.Xml.Xsl.XslTransform> está obsoleta no .NET Framework 2.0. Você pode executar a linguagem XSL Transformations (XSLT) usando a classe <xref:System.Xml.Xsl.XslCompiledTransform>. Confira [Usar a classe XslCompiledTransform](using-the-xslcompiledtransform-class.md) e [Migrar da classe XslTransform](migrating-from-the-xsltransform-class.md) para saber mais.

 Os fragmentos da árvore de resultado, também conhecido como partes da árvore de resultado, não há nada mais que um tipo especial de conjunto do nó. Você pode executar qualquer função em que eles podem ser executados em um conjunto de nó. Ou, você também pode converter um fragmento da árvore de resultado a um conjunto de nó usando a função de `node-set()` e depois usá-lo qualquer lugar que um conjunto de nó pode ser usado.

 Um fragmento da árvore do resultado é criado como resultado de usar um elemento de `<xsl:variable>` ou de `<xsl:param>` de uma maneira específica em uma folha de estilos. A sintaxe para elementos de `variable` e de `parameter` é a seguinte:

```xml
<xsl:param name=Qname select= XPath Expression >
    template body
</xsl:param>

<xsl:variable name=Qname select=XPath Expression >
    template body
</xsl:variable>
```

Para o elemento de `parameter` , o valor é atribuído ao nome qualificado (`Qname`) em várias maneiras. Você pode atribuir um valor padrão para o parâmetro retornando o conteúdo de uma expressão de idioma do caminho de XML (XPath) no atributo de `select` , ou atribuindo o conteúdo do corpo do modelo.

Para o elemento de `variable` , o valor é atribuído também em várias maneiras. Você pode atribuí-lo retornando o conteúdo de expressão XPath no atributo de `select` , ou atribuindo o conteúdo do corpo do modelo.

Para elementos de `parameter` e de `variable` , se um valor é determinado pela expressão XPath, então um dos quatro tipos básicos XPath será retornado: Booleano, cadeia de caracteres, número, ou conjunto de nó. Quando o valor é fornecido usando um corpo não vazio de modelo, então um tipo de dados não XPath será retornado, e que será um fragmento da árvore de resultado.

Quando uma variável é associado a um fragmento da árvore de resultado em vez de um dos quatro tipos de dados básicos XPath, este é a única vez que uma consulta XPath retorna um tipo que não é um dos quatro tipos de objeto XPath. Os fragmentos da árvore de resultado e seu comportamento são discutidos na [especificação World Wide Web Consortium (W3C)](https://www.w3.org/TR/xslt-10/), da [seção 11.1 Fragmentos da Árvore do Resultado](https://www.w3.org/TR/xslt-10/#section-Result-Tree-Fragments) até [seção 11.6 Passando Parâmetros para os Modelos](https://www.w3.org/TR/xslt-10/#section-Passing-Parameters-to-Templates). Além disso, a [seção 1 Introdução](https://www.w3.org/TR/xslt-10/#section-Introduction) discute como os modelos podem conter elementos do namespace XSLT que retornam ou como podem criar fragmentos da árvore de resultado.

Um fragmento da árvore de resultado, o conceito, se comporta como um nó definido com nada mais de um único nó raiz. No entanto, o resto de nós retornados é nós filho. Para ver programaticamente nós filho, copie o fragmento da árvore de resultado à árvore de resultado usando o elemento de `<xsl:copy-of>` . Quando cópia- de for executado, todos os nós filhos são copiados também à árvore de resultado em ordem. Até `copy` ou `copy-of` é usado, um fragmento da árvore do resultado não é parte da árvore de resultado ou da saída de transformação.

Para iterar sobre os nós retornados de um fragmento da árvore de resultado, <xref:System.Xml.XPath.XPathNavigator> é usado. O exemplo de código a seguir mostra como criar um fragmento da árvore de resultado em uma folha de estilos chamar a função com um parâmetro `fragment`, que contém XML.

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:user="http://www.adventure-works.com"
                version="1.0">
    <xsl:var name="fragment">
        <node1>
            <node2/>
        </node1>
    <xsl:var>

  <msxsl:script language="C#" implements-prefix="user">
    function NodeFragment(XPathNavigator nav)
    {
      if (nav.HasSelection == false)
        XPathNavigator.MoveToNext();
      return;
    }
  </msxsl:script>

    <xsl:template match="/">
            <xsl:value-of select="user:NodeFragment(msxml:node-set($fragment))"/>
    </xsl:template>
</xsl:stylesheet>
```

Aqui está um exemplo que mostra uma variável, que está em formato rich text (RTF), portanto, um tipo de fragmento da árvore de resultado, que não é convertido em um conjunto de nó. Em vez disso, é passado para uma função de script, e <xref:System.Xml.XPath.XPathNavigator> é usado para navegar sobre os nós.

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"
        xmlns:user="urn:books"
        exclude-result-prefixes="msxsl">

<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>

<xsl:variable name="node-fragment">
    <book>Book1</book>
    <book>Book2</book>
    <book>Book3</book>
    <book>Book4</book>
</xsl:variable>

<msxsl:script implements-prefix="user" language="c#">

<![CDATA[
    string func(XPathNavigator nav)
    {
        bool b = nav.MoveToFirstChild();
        if (b)
            return nav.Value;
        else
            return "Does not exist";
    }

]]>

</msxsl:script>

<xsl:template match="/">
    <first_book>
        <xsl:value-of select="user:func($node-fragment)"/>
    </first_book>
</xsl:template>

</xsl:stylesheet>
```

O resultado de qualquer transformar XML com essa folha de estilos é mostrado na seguinte saída.

## <a name="output"></a>Saída

```xml
<first_book xmlns:user="urn:books">Book1</first_book>
```

Como dito acima, a função de `node-set` permite que você converter um fragmento da árvore de resultado em um conjunto de nó. O nó resultante sempre contém um único nó que é o nó raiz da árvore. Se você converter um fragmento da árvore de resultado a um conjunto de nó, então você pode usá-lo em qualquer lugar que um conjunto normal do nó é usado, como em para- cada instrução ou o valor de um atributo de `select` . As seguintes linhas de código mostram o fragmento que está sendo convertido em um nó definido e usaram-se como um nó definida:

`<xsl:for-each select="msxsl:node-set($node-fragment)">`

`<xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>`

Quando um fragmento é convertido em um conjunto de nó, você não usa <xref:System.Xml.XPath.XPathNavigator> para navegar sobre ele. Para um conjunto de nó, você usa <xref:System.Xml.XPath.XPathNodeIterator> em vez disso.

No exemplo a seguir, `$var` é uma variável que é uma árvore de nós na folha de estilos. Para- cada declaração, combinada com a função de `node-set` , permite que o usuário itere sobre esta árvore como um conjunto de nó.

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:user="http://www.adventure-works.com"
                version="1.0">
    <xsl:variable name="states">
        <node1>AL</node1>
        <node1>CA</node1>
        <node1>CO</node1>
        <node1>WA</node1>
    </xsl:variable>

    <xsl:template match="/">
            <xsl:for-each select="msxsl:node-set($states)"/>
    </xsl:template>
</xsl:stylesheet>
```

Aqui está um exemplo de uma variável que está em RTF, e portanto de fragmento da árvore do resultado de tipo, que é convertido em um nó definida antes de ser passado para uma função script como XPathNodeIterator.

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:msxsl="urn:schemas-microsoft-com:xslt"
        xmlns:user="urn:books"
        exclude-result-prefixes="msxsl">

<xsl:output method="xml" indent="yes" omit-xml-declaration="yes"/>

<xsl:variable name="node-fragment">
    <book>Book1</book>
    <book>Book2</book>
    <book>Book3</book>
    <book>Book4</book>
</xsl:variable>

<msxsl:script implements-prefix="user" language="c#">

<![CDATA[
    string func(XPathNodeIterator it)
    {
        it.MoveNext();
        return it.Current.Value;
        //it.Current returns XPathNavigator positioned on the current node
    }

]]>

</msxsl:script>
<xsl:template match="/">
    <books>
        <xsl:value-of select="user:func(msxsl:node-set($node-fragment))"/>
    </books>
</xsl:template>

</xsl:stylesheet>
```

O seguinte é o resultado de transformar XML com essa folha de estilos:

```xml
<books xmlns:user="urn:books">Book1Book2Book3Book4</books>
```

## <a name="see-also"></a>Consulte também

- <xref:System.Xml.XPath.XPathNodeIterator>
- [Transformações XSLT com a classe XslTransform](xslt-transformations-with-the-xsltransform-class.md)
- [A classe XslTransform implementa do processador XSLT](xsltransform-class-implements-the-xslt-processor.md)
