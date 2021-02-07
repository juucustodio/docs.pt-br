---
description: 'Saiba mais sobre: transporte MSMQ'
title: Transporte do MSMQ
ms.date: 03/30/2017
ms.assetid: 3f29a2fe-24df-4614-b64c-b0c084fb7003
ms.openlocfilehash: af371a6481e7137321f1c32d0183f68e529d13d3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686343"
---
# <a name="msmq-transport"></a>Transporte do MSMQ

Este tópico lista todas as exceções geradas pelo transporte MSMQ.  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|MsmqActiveDirectoryRequiresNativeTransfer|Falha na validação de associação para a mensagem. O cliente não pode enviar mensagens. Um conflito nas propriedades de associação causou essa falha. O UseActiveDirectory é definido como true e QueueTransferProtocol é definido como Native. Para resolver o conflito, corrija uma das propriedades.|  
|MsmqAuthNoneRequiresProtectionNone|A validação de associação para o serviço falhou. O ponto de extremidade de serviço ou o cliente não pode ser iniciado. Um conflito nas propriedades de associação causou essa falha. MsmqAuthenticationMode é definido como None e MsmqProtectionLevel não está definido como None. Para resolver o conflito, corrija uma das propriedades.|  
|MsmqCustomRequiresPerAddDLQ|Falha na validação de associação para a mensagem. O cliente não pode enviar a mensagem. O DeadLetterQueue está definido como Custom, mas o CustomDeadLetterQueue não foi especificado. Especifique o URI da fila de mensagens mortas para cada aplicativo na propriedade CustomDeadLetterQueue.|  
|MsmqDeserializationError|Foi encontrado um erro ao desserializar a mensagem XML. A mensagem não pode ser recebida e descartada.|  
|MsmqDLQNotWriteable|Falha na validação de associação para o cliente. O cliente não pode enviar uma mensagem. A fila de mensagens mortas especificada não existe ou não pode ser gravada. Verifique se a fila existe com a autorização apropriada para gravar nela.|  
|MsmqGetPrivateComputerInformationError|A verificação de versão falhou com o erro especificado. A versão do MSMQ não pode ser detectada, todas as operações que estão no canal na fila falharão. Verifique se o MSMQ está instalado e disponível.|  
|MsmqNoAssurancesForVolatile|A validação de associação para o serviço falhou. O ponto de extremidade de serviço ou o cliente não pode ser iniciado. A propriedade ExactlyOnce é definida como true e a propriedade durável é definida como false. Isso não tem suporte. Para resolver o conflito, corrija uma dessas propriedades.|  
|MsmqNonTransactionalQueueNeeded|Uma incompatibilidade entre a associação e a configuração da fila MSMQ foi detectada. Não é possível iniciar o ponto de extremidade de serviço. A propriedade ExactlyOnce é definida como false e a fila para a qual as mensagens serão lidas é uma fila transacional. Corrija o erro definindo a propriedade ExactlyOnce como true ou crie uma associação não transacional.|  
|MsmqOpenError|Ocorreu um erro ao abrir a fila especificada. A mensagem não pode ser enviada ou recebida da fila. Verifique se o MSMQ está instalado e em execução. Verifique também se a fila está disponível para ser aberta com o modo de acesso e a autorização necessários.|  
|MsmqPathLookupError|Ocorreu um erro ao converter o nome do caminho de fila especificado para o nome do formato. Todas as operações no canal enfileirado falharam. Verifique se o endereço da fila é válido. O MSMQ deve ser instalado com a integração do Active Directory habilitada e o acesso a ele está disponível.|  
|MsmqPerAppDLQRequiresCustom|Falha na validação de associação no cliente. O cliente não pode enviar mensagens. A propriedade CustomDeadLetterQueue está definida, mas a propriedade DeadLetterQueue não está definida como Custom. Defina a propriedade DeadLetterQueue como Custom.|  
|MsmqPerAppDLQRequiresExactlyOnce|Falha na validação de associação para o cliente. O cliente não pode enviar mensagens. Um conflito nas propriedades de associação está causando a falha. Para usar a fila de mensagens mortas personalizada, ExactlyOnce deve ser definido como true para resolver em conflito.|  
|MsmqPerAppDLQRequiresMsmq4|Uma incompatibilidade entre a associação e a configuração do MSMQ foi detectada. O cliente não pode enviar mensagens. Para usar a fila de mensagens mortas personalizada, você deve ter o MSMQ versão 4,0 ou superior. Se você não tiver a versão 4,0 ou superior do MSMQ, defina a propriedade DeadLetterQueue como System ou None.|  
|MsmqReceiveError|Ocorreu um erro ao receber uma mensagem da fila. Verifique se o MSMQ está instalado e em execução. Verifique se a fila está disponível para receber de.|  
|MsmqSameTransactionExpected|Ocorreu um erro de transação para esta sessão. O canal de sessão está com falha. As mensagens na sessão não podem ser enviadas ou recebidas. Uma sessão enfileirada não pode ser associada a mais de uma transação. Certifique-se de que todas as mensagens na sessão sejam enviadas ou recebidas usando uma única transação.|  
|MsmqSendError|Ocorreu um erro ao enviar para a fila especificada. Verifique se o MSMQ está instalado e em execução. Se você estiver enviando para uma fila local, verifique se a fila existe com o modo de acesso e a autorização necessários.|  
|MsmqTimeSpanTooLarge|A vida útil da mensagem é muito grande. Não é possível enviar a mensagem. A TTL (vida útil da mensagem) não pode exceder o valor máximo de Int32.|  
|MsmqTokenProviderNeededForCertificates|Não é possível encontrar um X509SecurityTokenProvider. Não é possível enviar a mensagem. O modo de autenticação de certificado requer um provedor de token X. 509. Verifique se um provedor de token de segurança está disponível para o certificado instalado.|  
|MsmqTransactedDLQExpected|Ocorreu uma incompatibilidade entre a associação e a configuração do MSMQ. Não é possível enviar mensagens. A fila de mensagens mortas personalizada especificada na associação deve ser uma fila de transações. Verifique se o endereço da fila de mensagens mortas personalizada está correto e se a fila é uma fila transacional.|  
|MsmqTransactionalQueueNeeded|Ocorreu uma incompatibilidade entre a associação e a configuração da fila MSMQ. Não é possível iniciar o ponto de extremidade de serviço. A propriedade ExactlyOnce é definida como true e a fila para a qual as mensagens serão lidas não é uma fila transacional. Para corrigir o erro, defina a propriedade ExactlyOnce como false ou crie uma fila transacional para essa associação.|  
|MsmqTransactionCurrentRequired|Nenhuma transação está disponível para enviar mensagens na sessão. Para enviar uma mensagem em uma sessão enfileirada, é necessária uma transação. Certifique-se de que um escopo de transação seja especificado para enviar a mensagem na sessão.|  
|MsmqTransactionRequired|Uma transação é necessária, mas não está disponível. As mensagens não podem ser enviadas ou recebidas. Verifique se o escopo da transação está especificado para enviar ou receber mensagens.|  
|MsmqUnsupportedSerializationFormat|Ocorreu um erro de desserialização. A mensagem não pode ser recebida e descartada. Não há suporte para o formato de serialização especificado.|  
|MsmqWrongPrivateQueueSyntax|A URL é inválida. A URL da fila não pode conter o caractere ' $ '. Use a sintaxe em net. MSMQ://machine/private/queueName para endereçar uma fila privada.|
