---
description: 'Saiba mais sobre: comunicações principais: estrutura de conexão'
title: 'Comunicações principais: Estrutura de conexão'
ms.date: 03/30/2017
ms.assetid: 61ee00e1-896d-47c8-942f-1db28ac89cdc
ms.openlocfilehash: c0603f6f47c6259faeb2de4e9fc6c1be37bbb183
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686551"
---
# <a name="core-communications-connection-framework"></a>Comunicações principais: Estrutura de conexão

Este tópico lista todas as exceções geradas pela estrutura de conexão do Windows Communication Foundation (WCF).  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|CloseTimedOut|O método Close atingiu o tempo limite após o tempo especificado. Aumente o valor de tempo limite que é passado para a chamada para fechar ou aumentar o valor de CloseTimeout na associação. O tempo determinado para essa operação pode ter sido uma parte de um tempo limite maior.|  
|ContentTypeMismatch|O tipo de conteúdo especificado foi enviado a um serviço que estava esperando o especificado. As associações de cliente e serviço podem ser incompatíveis.|  
|DuplexChannelAbortedDuringOpen|O canal duplex para a terminação especificada durante o processo aberto.|  
|FramingValueNotAvailable|O valor não pode ser acessado porque não está totalmente decodificado.|  
|OperationAbortedDuringConnectionEstablishment|A operação foi encerrada ao estabelecer uma conexão com o especificado.|  
|ReceiveTimedOut2|A operação de recebimento atingiu o tempo limite após o tempo especificado. O tempo determinado para essa operação pode ter sido uma parte de um tempo limite maior.|  
|SendCannotBeCalledAfterCloseOutputSession|Você não pode enviar mensagens em um canal após o CloseOutputSession ter ter sido chamado.|
