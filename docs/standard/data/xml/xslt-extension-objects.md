---
description: 'Saiba mais sobre: objetos de extensão XSLT'
title: Objetos de extensão XSLT
ms.date: 03/30/2017
ms.assetid: a4ebdbad-087c-4cfe-acc0-17c48142f81a
ms.openlocfilehash: 5fc4ee8b3828219bc298a3ffc4c81bc342e2f591
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782527"
---
# <a name="xslt-extension-objects"></a>Objetos de extensão XSLT

Os objetos de extensão são usados para estender a funcionalidade de folhas de estilos. Os objetos de extensão são mantidos pela classe de <xref:System.Xml.Xsl.XsltArgumentList> .  
  
 Os seguintes são vantagens de usar um objeto de extensão em vez do script inserido:  
  
- Fornece a melhor encapsulamento e reutilização de classes.  
  
- Permite que as folhas de estilos são menores e mais sustentável.  
  
 Os objetos de extensão XSLT são adicionados ao objeto de <xref:System.Xml.Xsl.XsltArgumentList> usando o método <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> . Um nome qualificado e URI de namespace são associados com o objeto de extensão no momento.  
  
> [!NOTE]
> O conjunto de permissões FullTrust é necessário chamar o método de <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> . Para saber mais, confira [Segurança de acesso ao código](../../../framework/misc/code-access-security.md) e [Conjuntos de permissão nomeada](/previous-versions/dotnet/netframework-4.0/4652tyx7(v=vs.100)).  
  
 Os tipos de dados retornados de objetos de extensão é um dos quatro tipos de dados básicos XPath `number`, `string`, `Boolean`, e `node set`.  
  
 Nenhum método que é definido com a palavra-chave `params` , que permite que um número especificado de parâmetros não é passado, não é suportado atualmente pela classe de <xref:System.Xml.Xsl.XslCompiledTransform> . As folhas de estilos XSLT que utilizam qualquer método definido com a palavra-chave `params` não funcionarão corretamente. Para obter detalhes, confira [params](../../../csharp/language-reference/keywords/params.md).  
  
### <a name="to-use-an-xslt-extension-object"></a>Para usar um objeto de extensão XSLT  
  
1. Crie um objeto de <xref:System.Xml.Xsl.XsltArgumentList> e adicione o objeto de extensão usando o método <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> .  
  
2. Chame o objeto de extensão folha de estilos.  
  
3. Passe o objeto de <xref:System.Xml.Xsl.XsltArgumentList> para o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> .  
  
## <a name="see-also"></a>Consulte também

- [Transformações XSLT](xslt-transformations.md)
- [Considerações de segurança XSLT](xslt-security-considerations.md)
