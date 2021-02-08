---
description: 'Saiba mais sobre: criar novos nós no DOM'
title: Criar novos nós no DOM
ms.date: 03/30/2017
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
ms.openlocfilehash: fdc2eb20a71450285e47a5f8b6766ba77151a7f8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783411"
---
# <a name="create-new-nodes-in-the-dom"></a>Criar novos nós no DOM

O <xref:System.Xml.XmlDocument> tem um método de criação para todos os tipos de nó. Forneça o método com um nome se necessário, e conteúdo ou outros parâmetros para os nós que têm conteúdo (por exemplo, um nó de texto), e o nó é criado. Os seguintes métodos são os que precisam de um nome e alguns outros parâmetros preenchidos para criar um nó apropriado.  
  
- <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
- <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
- <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
- <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
- <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 Outros tipos de nós têm mais requisitos do que apenas fornecer dados para parâmetros.  
  
 Para saber mais sobre atributos, confira [Criando novos atributos para elementos no DOM](creating-new-attributes-for-elements-in-the-dom.md). Para saber mais sobre elementos e validação de nomes de atributos, confira [O elemento XML e a verificação de nome de atributo ao criar novos nós](xml-element-and-attribute-name-verification-when-creating-new-nodes.md). Para criar referências de entidade, confira [Criando novas referências de entidades](creating-new-entity-references.md). Para saber mais sobre como os namespaces afetam a expansão de referências de entidade, confira [Efeito do namespace na expansão de referência de entidade para novos nós contendo elementos e atributos](namespace-affect-on-entity-ref-expansion-for-new-nodes.md).  
  
 Assim que os novos nós são criados, há vários métodos disponíveis para inseri-los na árvore. A tabela lista os métodos com uma descrição de onde o novo nó aparece no DOM (Document Object Model) XML.  
  
|Método|Posicionamento do nó|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|Inserido antes do nó de referência. Por exemplo, para inserir o novo nó na posição 5:<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> Para obter mais informações, consulte o método <xref:System.Xml.XmlNode.InsertBefore%2A>.|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|Inserido após o nó de referência. Por exemplo:<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> Para obter mais informações, consulte o método <xref:System.Xml.XmlNode.InsertAfter%2A>.|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|Adiciona o nó no final da lista de nós filho para o nó determinado. Se o nó que está sendo adicionado for um <xref:System.Xml.XmlDocumentFragment>, todo o conteúdo do fragmento do documento é movido para a lista filho deste nó. Para obter mais informações, consulte o método <xref:System.Xml.XmlNode.AppendChild%2A>.|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|Adiciona o nó no início da lista de nós filho do nó determinado. Se o nó que está sendo adicionado for um <xref:System.Xml.XmlDocumentFragment>, todo o conteúdo do fragmento do documento é movido para a lista filho deste nó. Para obter mais informações, consulte o método <xref:System.Xml.XmlNode.PrependChild%2A>.|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|Adiciona um nó <xref:System.Xml.XmlAttribute> ao final da coleção de atributos associada a um elemento. Para obter mais informações, consulte o método <xref:System.Xml.XmlAttributeCollection.Append%2A>.|  
  
## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
