---
description: 'Saiba mais sobre: usando WS-AtomicTransaction'
title: Utilizando Transações WS-Atomic
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF]
ms.assetid: 04a4c200-0af0-4c5d-a3d9-87cb7339e054
ms.openlocfilehash: c79a5912289d0dca9f671e614e69e54b82bba854
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756026"
---
# <a name="using-ws-atomictransaction"></a>Utilizando Transações WS-Atomic

O WS-AtomicTransaction (WS-AT) é um protocolo de transação interoperável. Ele permite que você flua transações distribuídas usando mensagens de serviço Web e coordene interoperável entre infraestruturas de transação heterogêneas. O WS-AT usa o protocolo de confirmação de duas fases para direcionar um resultado atômico entre aplicativos distribuídos, gerenciadores de transações e gerenciadores de recursos.  
  
 O Windows Communication Foundation de implementação do WS-AT (WCF) fornece um serviço de protocolo incorporado ao Gerenciador de transações do Microsoft Coordenador de Transações Distribuídas (MSDTC). Usando o WS-AT, os aplicativos WCF podem fluir transações para outros aplicativos, incluindo serviços Web interoperáveis criados com tecnologia de terceiros.  
  
 Ao fluir uma transação entre um aplicativo cliente e um aplicativo de servidor, o protocolo de transação usado é determinado pela associação que o servidor expõe no ponto de extremidade selecionado pelo cliente. Algumas associações fornecidas pelo sistema WCF assumem como padrão a especificação do `OleTransactions` protocolo como o formato de propagação de transação, enquanto outros assumem a especificação de WS-AT. Você também pode modificar programaticamente a escolha do protocolo de transação dentro de uma determinada associação.  
  
 A escolha do protocolo influencia:  
  
- O formato dos cabeçalhos de mensagem usados para fluir a transação do cliente para o servidor.  
  
- O protocolo de rede usado para executar o protocolo de confirmação de duas fases entre o Gerenciador de transações do cliente e a transação do servidor, a fim de resolver o resultado da transação.  
  
 Se o servidor e o cliente forem gravados usando o WCF, você não precisará usar o WS-AT. Em vez disso, você pode usar as configurações padrão de `NetTcpBinding` com o `TransactionFlow` atributo habilitado, que usará o `OleTransactions` protocolo. Para obter mais informações, confira [\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md). Caso contrário, se você estiver fluindo transações para serviços Web criados em tecnologias de terceiros, deverá usar WS-AT.  
  
## <a name="see-also"></a>Consulte também

- [Configurando suporte de transações de WS-Atomic](configuring-ws-atomic-transaction-support.md)
