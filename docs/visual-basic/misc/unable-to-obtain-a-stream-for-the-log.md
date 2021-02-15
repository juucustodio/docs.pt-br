---
description: 'Saiba mais sobre: não é possível obter um fluxo para o log'
title: Não é possível obter um fluxo para o log
ms.date: 07/20/2015
f1_keywords:
- vbrApplicationLog_ExhaustedPossibleStreamNames
ms.assetid: 33994f52-8efb-4790-a459-033e5c1db632
ms.openlocfilehash: 6eda12eb4dc2b3cf303e543a66e1f2f7d739eb6b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100455269"
---
# <a name="unable-to-obtain-a-stream-for-the-log"></a>Não é possível obter um fluxo para o log

Não é possível obter um fluxo para o log. Os nomes de arquivo potenciais com base em \<name> já estão em uso.  
  
 A <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> classe não pôde criar um novo arquivo de log porque todos os nomes de arquivo de log potenciais com base no \<name> já estão em uso.  
  
 Ter muitos arquivos de log pode indicar um problema de arquitetura com o aplicativo. Consulte a documentação da <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> classe para obter mais informações.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Defina a <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A> propriedade como <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Daily> ou <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Weekly> para incluir um carimbo de data/hora no nome do arquivo de log.  
  
2. Arquive os logs existentes e remova-os do computador para permitir que o <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> objeto crie novos logs.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>
- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A>
- [Meu. Application. log](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
- [Meu. Application. info. DirectoryPath](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
