---
description: 'Saiba mais sobre a cláusula: Handles (Visual Basic)'
title: Cláusula Handles
ms.date: 07/20/2015
f1_keywords:
- Handles
- vb.Handles
helpviewer_keywords:
- Handles keyword [Visual Basic]
ms.assetid: 1b051c0e-f499-42f6-acb5-6f4f27824b40
ms.openlocfilehash: 2bddfdecc163feacaaf042a7928ab16af324b0a3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99769020"
---
# <a name="handles-clause-visual-basic"></a>Cláusula Handles (Visual Basic)

Declara que um procedimento manipula um evento especificado.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
proceduredeclaration Handles eventlist  
```  
  
## <a name="parts"></a>Partes  

 `proceduredeclaration`  
 A `Sub` declaração de procedimento para o procedimento que manipulará o evento.  
  
 `eventlist`  
 Lista dos eventos `proceduredeclaration` a serem tratados, separados por vírgulas. Os eventos devem ser gerados pela classe base para a classe atual ou por um objeto declarado usando a `WithEvents` palavra-chave.  
  
## <a name="remarks"></a>Comentários  

 Use a `Handles` palavra-chave no final de uma declaração de procedimento para fazer com que ela manipule eventos gerados por uma variável de objeto declarada usando a `WithEvents` palavra-chave. A `Handles` palavra-chave também pode ser usada em uma classe derivada para manipular eventos de uma classe base.  
  
 A `Handles` palavra-chave e a `AddHandler` instrução permitem que você especifique que procedimentos específicos manipulam eventos específicos, mas há diferenças. Use a `Handles` palavra-chave ao definir um procedimento para especificar que ele trata de um evento específico. A `AddHandler` instrução conecta procedimentos a eventos em tempo de execução. Para obter mais informações, consulte [instrução AddHandler](addhandler-statement.md).  
  
 Para eventos personalizados, o aplicativo invoca o `AddHandler` acessador do evento quando ele adiciona o procedimento como um manipulador de eventos. Para obter mais informações sobre eventos personalizados, consulte [Event Statement](event-statement.md).  
  
## <a name="example"></a>Exemplo  

 [!code-vb[VbVbalrEvents#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#2)]  
  
 O exemplo a seguir demonstra como uma classe derivada pode usar a `Handles` instrução para manipular um evento de uma classe base.  
  
 [!code-vb[VbVbalrEvents#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#3)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir contém dois manipuladores de eventos de botão para um projeto de **aplicativo WPF** .  
  
 [!code-vb[VbVbalrEvents#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/class3.vb#41)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir é equivalente ao exemplo anterior. O `eventlist` na `Handles` cláusula contém os eventos para ambos os botões.  
  
 [!code-vb[VbVbalrEvents#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/class3.vb#42)]  
  
## <a name="see-also"></a>Consulte também

- [WithEvents](../modifiers/withevents.md)
- [Instrução AddHandler](addhandler-statement.md)
- [Instrução RemoveHandler](removehandler-statement.md)
- [Instrução Event](event-statement.md)
- [Instrução RaiseEvent](raiseevent-statement.md)
- [Eventos](../../programming-guide/language-features/events/index.md)
