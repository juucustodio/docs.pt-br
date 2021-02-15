---
description: 'Saiba mais sobre: meu objeto. Response'
title: Objeto My.Response
ms.date: 07/20/2015
f1_keywords:
- My.MyWebExtension.Response
- My.Response
helpviewer_keywords:
- My.Response object
ms.assetid: 626359bc-3165-40b4-bfaf-2c610e26eb5b
ms.openlocfilehash: 551528356040539994251cb66a905d0249f482da
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99640609"
---
# <a name="myresponse-object"></a>Objeto My.Response

Obtém o <xref:System.Web.HttpResponse> objeto associado ao <xref:System.Web.UI.Page> . Esse objeto permite que você envie dados de resposta HTTP para um cliente e contém informações sobre essa resposta.  
  
## <a name="remarks"></a>Comentários  

 O `My.Response` objeto contém o <xref:System.Web.HttpResponse> objeto atual associado à página.  
  
 O `My.Response` objeto só está disponível para aplicativos ASP.net.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir obtém a coleção de cabeçalho do `My.Request` objeto e usa o `My.Response` objeto para escrevê-lo na página ASP.net.  
  
 [!code-aspx-vb[VbVbalrMyWeb#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyWeb/VB/Default.aspx#1)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Web.HttpResponse>
- [Objeto My.Request](my-request-object.md)
