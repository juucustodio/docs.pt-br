---
description: 'Saiba mais sobre: como registrar um protocolo personalizado usando WebRequest'
title: 'Como: Registrar um protocolo personalizado usando WebRequest'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 98ddbdb9-66b1-4080-92ad-51f5c447fcf8
ms.openlocfilehash: 7415017f20c0c6ed80570992e249fb8121907de2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785751"
---
# <a name="how-to-register-a-custom-protocol-using-webrequest"></a>Como: Registrar um protocolo personalizado usando WebRequest

Este exemplo mostra como registrar uma classe específica de protocolo que é definida em outro local. Neste exemplo, `CustomWebRequestCreator` é o objeto implementado pelo usuário que implementa o método **create** que retorna o objeto `CustomWebRequest`. O exemplo de código pressupõe que você tenha escrito o código `CustomWebRequest` que implementa o protocolo personalizado.  
  
## <a name="example"></a>Exemplo  
  
```csharp  
WebRequest.RegisterPrefix("custom", new CustomWebRequestCreator());  
WebRequest req = WebRequest.Create("custom://customHost.contoso.com/");  
```  
  
```vb  
WebRequest.RegisterPrefix("custom", New CustomWebRequestCreator())  
Dim req As WebRequest = WebRequest.Create("custom://customHost.contoso.com/")  
```  
  
## <a name="compiling-the-code"></a>Compilando o código  

 Este exemplo requer:  
  
 Referências ao namespace <xref:System.Net>.  
  
## <a name="see-also"></a>Consulte também

- [Programando protocolos conectáveis](programming-pluggable-protocols.md)
