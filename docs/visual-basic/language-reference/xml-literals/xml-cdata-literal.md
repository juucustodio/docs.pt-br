---
description: 'Saiba mais sobre: literal XML CDATA (Visual Basic)'
title: Literal CDATA XML
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralCdata
helpviewer_keywords:
- CDATA literal [Visual Basic]
- XML CDATA literal [Visual Basic]
- XML literals [Visual Basic], CDATA
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
ms.openlocfilehash: d0b419954acb5a9e8ae824dbac8234e2116d09b9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99768747"
---
# <a name="xml-cdata-literal-visual-basic"></a>Literal CDATA XML (Visual Basic)

Um literal que representa um <xref:System.Xml.Linq.XCData> objeto.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<![CDATA[content]]>  
```  
  
## <a name="parts"></a>Partes  

 `<![CDATA[`  
 Obrigatório. Indica o início da seção XML CDATA.  
  
 `content`  
 Obrigatório. Conteúdo de texto a ser exibido na seção CDATA XML.  
  
 `]]>`  
 Obrigatório. Denota o final da seção.  
  
## <a name="return-value"></a>Valor retornado  

 Um objeto <xref:System.Xml.Linq.XCData>.  
  
## <a name="remarks"></a>Comentários  

 As seções XML CDATA contêm texto bruto que deve ser incluído, mas não analisado, com o XML que o contém. Uma seção CDATA XML pode conter qualquer texto. Isso inclui caracteres XML reservados. A seção XML CDATA termina com a sequência "]] >". Isso implica nos seguintes pontos:  
  
- Você não pode usar uma expressão inserida em um literal XML CDATA porque os delimitadores de expressão inseridos são conteúdo XML CDATA válido.  
  
- As seções XML CDATA não podem ser aninhadas porque `content` não podem conter o valor "]] >".  
  
 Você pode atribuir um literal XML CDATA a uma variável ou incluí-lo em um literal de elemento XML.  
  
> [!NOTE]
> Um literal XML pode abranger várias linhas, mas não usa caracteres de continuação de linha. Isso permite que você copie o conteúdo de um documento XML e cole-o diretamente em um programa Visual Basic.  
  
 O compilador Visual Basic converte o literal XML CDATA em uma chamada para o <xref:System.Xml.Linq.XCData.%23ctor%2A> Construtor.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir cria uma seção CDATA que contém o texto "pode conter \<XML> marcas literais".  
  
 [!code-vb[VbXMLSamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#23)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XCData>
- [Literal do Elemento XML](xml-element-literal.md)
- [Literais XML](index.md)
- [Criando XML no Visual Basic](../../programming-guide/language-features/xml/creating-xml.md)
