---
description: 'Saiba mais sobre: suporte para a função msxsl: node-set ()'
title: Suporte à função msxsl:node-set()
ms.date: 03/30/2017
ms.assetid: d0cbf517-d9f6-4097-9851-4fa62903decd
ms.openlocfilehash: cd9f02dbfdd400b182c95453de5f49e43ee0b2aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782917"
---
# <a name="support-for-the-msxslnode-set-function"></a>Suporte à função msxsl:node-set()

A função `msxsl:node-set` permite que você converta um fragmento da árvore de resultados em um conjunto de nós. O conjunto de nós resultante sempre contém um único nó e é o nó raiz da árvore.  
  
> [!NOTE]
> A classe <xref:System.Xml.Xsl.XslTransform> está obsoleta no .NET Framework 2.0. Você pode executar a linguagem XSL Transformations (XSLT) usando a classe <xref:System.Xml.Xsl.XslCompiledTransform>. Confira [Usar a classe XslCompiledTransform](using-the-xslcompiledtransform-class.md) e [Migrar da classe XslTransform](migrating-from-the-xsltransform-class.md) para saber mais.  
  
 A função `msxsl:node-set` permite que você converta um fragmento da árvore de resultados em um conjunto de nós. O conjunto de nós resultante sempre contém um único nó e é o nó raiz da árvore.  
  
## <a name="example"></a>Exemplo  

 No exemplo a seguir, `$books` é uma variável que é uma árvore de nós na folha de estilos. A instrução for-each combinada com a função `node-set` permite que o usuário itere sobre essa árvore de nós como um conjunto de nós.  
  
## <a name="nodesetxsl"></a>nodeset.xsl  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.contoso.com"  
                version="1.0">  
    <xsl:variable name="books">  
        <book author="Michael Howard">Writing Secure Code</book>  
        <book author="Michael Kay">XSLT Reference</book>  
    </xsl:variable>  
  
    <xsl:template match="/">  
        <authors>  
            <xsl:for-each select="msxsl:node-set($books)/book">
                <author><xsl:value-of select="@author"/></author>  
            </xsl:for-each>  
        </authors>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
## <a name="output"></a>Saída  

 A saída da transformação é  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<authors><author>Michael Howard</author><author>Michael Kay</author></authors>  
```  
  
## <a name="see-also"></a>Consulte também

- [A classe XslTransform implementa do processador XSLT](xsltransform-class-implements-the-xslt-processor.md)
