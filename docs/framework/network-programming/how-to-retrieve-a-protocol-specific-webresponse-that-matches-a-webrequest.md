---
title: 'Como: Recuperar uma WebResponse específica de protocolo que corresponde a uma WebRequest'
description: Saiba como recuperar um WebResponse específico de protocolo que corresponde a um WebRequest no .NET Framework.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d8c90785-f16b-42a5-8439-ed2f731b2ba8
ms.openlocfilehash: fd163c115dcd19c05f93f4c202b043440834ba9d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266734"
---
# <a name="how-to-retrieve-a-protocol-specific-webresponse-that-matches-a-webrequest"></a>Como: Recuperar uma WebResponse específica de protocolo que corresponde a uma WebRequest

Esse exemplo mostra como recuperar uma WebResponse específica de protocolo que corresponde a uma WebRequest.  
  
## <a name="example"></a>Exemplo  
  
```csharp  
WebRequest req = WebRequest.Create("http://www.contoso.com/");  
WebResponse resp = req.GetResponse();  
```  
  
```vb  
Dim req As WebRequest = WebRequest.Create("http://www.contoso.com")  
Dim resp As WebResponse = req.GetResponse()  
```  
  
## <a name="compiling-the-code"></a>Compilando o código  

 Este exemplo requer:  
  
- Referências ao namespace **System.Net**.  
  
## <a name="see-also"></a>Veja também

- [Solicitando dados](requesting-data.md)
