---
description: 'Saiba mais sobre: Propriedade do indexador de extensão (Visual Basic)'
title: Propriedade do Indexador de Extensão
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionIndexer
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML extension indexer [Visual Basic]
- extension indexer [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: a16a4b13-54be-432c-82b3-a87091464ada
ms.openlocfilehash: ec165836f739db9a74ea266ebba32be5bb42cca6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99700319"
---
# <a name="extension-indexer-property-visual-basic"></a>Propriedade do indexador de extensão (Visual Basic)

Fornece acesso aos elementos individuais em uma coleção.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
object(index)  
```  
  
## <a name="parts"></a>Partes  
  
|Termo|Definição|  
|---|---|  
|`object`|Obrigatório. Uma coleção passível de consulta. Ou seja, uma coleção que implementa <xref:System.Collections.Generic.IEnumerable%601> ou <xref:System.Linq.IQueryable%601> .|  
|(|Obrigatório. Denota o início da Propriedade do indexador.|  
|`index`|Obrigatório. Uma expressão de inteiro que especifica a posição de base zero de um elemento da coleção.|  
|)|Obrigatório. Denota o final da Propriedade do indexador.|  
  
## <a name="return-value"></a>Valor retornado  

 O objeto do local especificado na coleção ou `Nothing` se o índice está fora do intervalo.  
  
## <a name="remarks"></a>Comentários  

 Você pode usar a propriedade do indexador de extensão para acessar elementos individuais em uma coleção. Essa propriedade do indexador normalmente é usada na saída das propriedades do eixo XML. As propriedades do eixo XML filho e do XML descendente retornam coleções de <xref:System.Xml.Linq.XElement> objetos ou um valor de atributo.  
  
 O compilador Visual Basic converte Propriedades do indexador de extensão em chamadas para o `ElementAtOrDefault` método. Ao contrário de um indexador de matriz, o `ElementAtOrDefault` método retorna `Nothing` se o índice está fora do intervalo. Esse comportamento é útil quando você não pode determinar facilmente o número de elementos em uma coleção.  
  
 Essa propriedade do indexador é como uma propriedade de extensão para coleções que implementam <xref:System.Collections.Generic.IEnumerable%601> ou <xref:System.Linq.IQueryable%601> : ela será usada somente se a coleção não tiver um indexador ou uma propriedade padrão.  
  
 Para acessar o valor do primeiro elemento em uma coleção de <xref:System.Xml.Linq.XElement> objetos ou <xref:System.Xml.Linq.XAttribute> , você pode usar a propriedade XML `Value` . Para obter mais informações, consulte [propriedade de valor XML](xml-value-property.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como usar o indexador de extensão para acessar o segundo nó filho em uma coleção de <xref:System.Xml.Linq.XElement> objetos. A coleção é acessada usando a propriedade do eixo filho, que obtém todos os elementos filho nomeados `phone` no `contact` objeto.  
  
 [!code-vb[VbXMLSamples#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#24)]  
  
 Esse código exibe o seguinte texto:  
  
 `Second phone number: 425-555-0145`  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XElement>
- [Propriedades do eixo XML](index.md)
- [Literais XML](../xml-literals/index.md)
- [Criando XML no Visual Basic](../../programming-guide/language-features/xml/creating-xml.md)
- [Propriedade do Valor XML](xml-value-property.md)
