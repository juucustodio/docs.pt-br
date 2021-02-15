---
description: 'Saiba mais sobre: como acessar propriedades de HTTP-Specific'
title: 'Como: Acessar propriedades específicas de HTTP'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f8848c7e-f5c5-4d42-b86d-9951ff8f4146
ms.openlocfilehash: a54ef247b479cf6cdec8dc28732304cf03b0b202
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729296"
---
# <a name="how-to-access-http-specific-properties"></a>Como: Acessar propriedades específicas de HTTP

Esta amostra explica como desligar o comportamento **Keep-alive** do HTTP e obter o número de versão do protocolo do servidor Web.  
  
## <a name="example"></a>Exemplo  
  
```vb  
Dim HttpWReq As HttpWebRequest= _  
    CType(WebRequest.Create("http://www.contoso.com"), HttpWebRequest)  
' Turn off connection keep-alives.  
HttpWReq.KeepAlive = False  
  
Dim HttpWResp As HttpWebResponse = _  
    CType(HttpWReq.GetResponse(), HttpWebResponse)  
  
' Get the HTTP protocol version number returned by the server.  
Dim ver As String = HttpWResp.ProtocolVersion.ToString()  
HttpWResp.Close()  
```  
  
```csharp  
HttpWebRequest HttpWReq =
    (HttpWebRequest)WebRequest.Create("http://www.contoso.com");  
// Turn off connection keep-alives.  
HttpWReq.KeepAlive = false;  
  
HttpWebResponse HttpWResp = (HttpWebResponse)HttpWReq.GetResponse();  
  
// Get the HTTP protocol version number returned by the server.  
String ver = HttpWResp.ProtocolVersion.ToString();  
HttpWResp.Close();  
```  
  
## <a name="compiling-the-code"></a>Compilando o código  

 Este exemplo requer:  
  
- Referências ao namespace **System.Net**.  
  
## <a name="see-also"></a>Consulte também

- [Acessando a Internet por meio de um proxy](accessing-the-internet-through-a-proxy.md)
- [Usando protocolos de aplicativo](using-application-protocols.md)
- [HTTP](http.md)
