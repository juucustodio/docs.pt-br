---
description: 'Saiba mais sobre: solução de problemas: ouvintes de log (Visual Basic)'
title: 'Solução de problemas: ouvintes de log'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
ms.openlocfilehash: dc40f88a19e9cb205c6adb290c1ed48d40eabf5b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99775039"
---
# <a name="troubleshooting-log-listeners-visual-basic"></a>Solucionando problemas: ouvintes de log (Visual Basic)

É possível usar os objetos `My.Application.Log` e `My.Log` para registrar em log as informações sobre eventos que ocorrem em seu aplicativo.  
  
 Para determinar quais ouvintes de log recebem essas mensagens, consulte [Instruções passo a passo: determinando onde My.Application.Log grava informações](walkthrough-determining-where-my-application-log-writes-information.md).  
  
 O objeto `Log` pode usar filtragem de log para limitar a quantidade de informações que ele registra no log. Se os filtros tiverem sido configurados incorretamente, os logs poderão conter informações incorretas. Para obter informações sobre filtragem, consulte [Instruções passo a passo: filtrando a saída de My.Application.Log](walkthrough-filtering-my-application-log-output.md).  
  
 No entanto, se um log tiver sido configurado incorretamente, talvez seja necessário obter mais informações sobre sua configuração atual. É possível obter essas informações por meio da propriedade `TraceSource` avançada do log.  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a>Para determinar os ouvintes de log do objeto Log no código  
  
1. Importe o namespace <xref:System.Diagnostics> no início do arquivo de código. Para obter mais informações, consulte [Instrução Imports (tipo e namespace .NET)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
     [!code-vb[VbVbalrMyApplicationLog#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#13)]  
  
2. Crie uma função que retorna uma cadeia de caracteres que consiste de informações para cada um dos ouvintes de log.  
  
     [!code-vb[VbVbalrMyApplicationLog#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#14)]  
  
3. Passe a coleção dos ouvintes de rastreamento do log para a função `GetListeners` e exiba o valor retornado.  
  
     [!code-vb[VbVbalrMyApplicationLog#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#19)]  
  
     Para obter mais informações, consulte <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [Trabalhar com logs do aplicativo](working-with-application-logs.md)
- [Passo a passo: determinar o local no qual My.Application.Log grava informações](walkthrough-determining-where-my-application-log-writes-information.md)
