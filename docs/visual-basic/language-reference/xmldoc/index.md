---
description: 'Saiba mais sobre: marcas XML recomendadas para comentários de documentação (Visual Basic)'
title: Marcas XML recomendadas para comentários de documentação
ms.date: 07/20/2015
f1_keywords:
- vb.XmlDocComment
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
ms.openlocfilehash: 5d3451d98b66817de143cfbddbcb6121de57ca8b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787442"
---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a>marcações XML recomendadas para comentários da documentação (Visual Basic)

O compilador Visual Basic pode processar comentários de documentação em seu código para um arquivo XML. Você pode usar ferramentas adicionais para processar o arquivo XML na documentação do.  
  
 Comentários XML são permitidos em construções de código, como tipos e membros de tipo. Para tipos parciais, apenas uma parte do tipo pode ter comentários XML, embora não haja nenhuma restrição ao comentar seus membros.  
  
> [!NOTE]
> Comentários de documentação não podem ser aplicados a namespaces. O motivo é que um namespace pode abranger vários assemblies, e nem todos os assemblies precisam ser carregados ao mesmo tempo.  
  
 O compilador processa qualquer marca que seja XML válida. As marcas a seguir fornecem funcionalidade comumente usada na documentação do usuário.  
  
||||  
|---|---|---|  
|[\<c>](c.md)|[\<code>](code.md)|[\<example>](example.md)|  
|[\<exception>](exception.md)<sup>1</sup>|[\<include>](include.md)<sup>1</sup>|[\<list>](list.md)|  
|[\<para>](para.md)|[\<param>](param.md)<sup>1</sup>|[\<paramref>](paramref.md)|  
|[\<permission>](permission.md)<sup>1</sup>|[\<remarks>](remarks.md)|[\<returns>](returns.md)|  
|[\<see>](see.md)<sup>1</sup>|[\<seealso>](seealso.md)<sup>1</sup>|[\<summary>](summary.md)|  
|[\<typeparam>](typeparam.md)<sup>1</sup>|[\<value>](value.md)||  
  
 (<sup>1</sup> o compilador verifica a sintaxe.)  
  
> [!NOTE]
> Se você quiser que os colchetes angulares apareçam no texto de um comentário de documentação, use `&lt;` e `&gt;` . Por exemplo, a cadeia de caracteres `"&lt;text in angle brackets&gt;"` será exibida como `<text in angle brackets>` .  
  
## <a name="see-also"></a>Consulte também

- [Documentando o código com XML](../../programming-guide/program-structure/documenting-your-code-with-xml.md)
- [-doc](../../reference/command-line-compiler/doc.md)
- [Como criar documentação XML](../../programming-guide/program-structure/how-to-create-xml-documentation.md)
