---
description: 'Saiba mais sobre: instrução AddHandler'
title: Instrução AddHandler
ms.date: 07/20/2015
f1_keywords:
- vb.AddHandlerMethod
- addhandler
- vb.addhandler
helpviewer_keywords:
- AddHandler statement [Visual Basic]
ms.assetid: cfe69799-2a0f-42c0-a99e-09fed954da01
ms.openlocfilehash: c0c34abd7ff225765ab36278825a555e2b84b0d1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99674097"
---
# <a name="addhandler-statement"></a>Instrução AddHandler

Associa um evento a um manipulador de eventos em tempo de execução.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
AddHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>Partes  

|||
|---|---|
|event|O nome do evento a ser manipulado.|  
|`eventhandler`|O nome de um procedimento que manipula o evento.|
|||
  
## <a name="remarks"></a>Comentários  

 As `AddHandler` `RemoveHandler` instruções e permitem iniciar e parar a manipulação de eventos a qualquer momento durante a execução do programa.  
  
 A assinatura do `eventhandler` procedimento deve corresponder à assinatura do evento `event` .  
  
 A `Handles` palavra-chave e a `AddHandler` instrução permitem que você especifique que procedimentos específicos manipulam eventos específicos, mas há diferenças. A `AddHandler` instrução conecta procedimentos a eventos em tempo de execução. Use a `Handles` palavra-chave ao definir um procedimento para especificar que ele trata de um evento específico. Para obter mais informações, consulte [Handles](handles-clause.md).  
  
> [!NOTE]
> Para eventos personalizados, a `AddHandler` instrução invoca o `AddHandler` acessador do evento. Para obter mais informações sobre eventos personalizados, consulte [Event Statement](event-statement.md).  
  
## <a name="example"></a>Exemplo  

 [!code-vb[VbVbalrEvents#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#17)]  
  
## <a name="see-also"></a>Consulte também

- [Instrução RemoveHandler](removehandler-statement.md)
- [Alças](handles-clause.md)
- [Instrução Event](event-statement.md)
- [Eventos](../../programming-guide/language-features/events/index.md)
