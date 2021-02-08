---
description: 'Saiba mais sobre: utilitário de configuração do WS-AtomicTransaction (wsatConfig.exe)'
title: Utilitário de configuração de transações WS-Atomic (wsatConfig.exe)
ms.date: 03/30/2017
ms.assetid: 1c56cf98-3963-46d5-a4e1-482deae58c58
ms.openlocfilehash: 8b315e5aa5df23a4d9bb032db41b7067accfa010
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792954"
---
# <a name="ws-atomictransaction-configuration-utility-wsatconfigexe"></a>Utilitário de configuração de transações WS-Atomic (wsatConfig.exe)

O utilitário de configuração WS-AtomicTransaction é usado para definir as configurações básicas de suporte de WS-AtomicTransaction.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
wsatConfig [Options]  
```  
  
## <a name="remarks"></a>Comentários

 Essa ferramenta de linha de comando pode ser usada para definir configurações básicas do WS-AT somente em um computador local. Se você precisar definir as configurações em máquinas locais e remotas, deverá usar o snap-in do MMC, conforme descrito em [Configurando o suporte à transação WS-Atomic](./feature-details/configuring-ws-atomic-transaction-support.md).  
  
 A ferramenta de linha de comando pode ser encontrada no local de instalação do SDK do Windows:
  
 Foundation\wsatConfig.exe de comunicação%SystemRoot%\Microsoft.Net\Framework\v3.0\Windows
  
 A tabela a seguir mostra as opções que podem ser usadas com o wsatConfig.exe (utilitário de configuração do WS-AtomicTransaction).  
  
> [!NOTE]
> Ao definir um certificado SSL para uma porta selecionada, você substitui o certificado SSL original associado a essa porta, se houver.  
  
|Opções|Descrição|  
|-------------|-----------------|  
|as\<account,>|Especifica uma lista separada por vírgulas de contas que podem participar de WS-AtomicTransaction. A validade dessas contas não está marcada.|  
|-accountsCerts: \<thumb>&#124; "Issuer\SubjectName", >|Especifica uma lista separada por vírgulas de certificados que podem participar de WS-AtomicTransaction. Os certificados são indicados por impressão digital ou pelo par Issuer\SubjectName. Use {EMPTY} para o nome da entidade se ele estiver vazio.|  
|-endpointCert: <Machine&#124;\<thumb>&#124; "Issuer\SubjectName" >|Usa o certificado do computador ou outro certificado de ponto de extremidade local especificado por um par de impressão digital ou Issuer\SubjectName. Usa {EMPTY} para o nome da entidade se ele estiver vazio.|  
|-maxTimeout:\<sec>|Especifica o tempo limite máximo em segundos. Os valores válidos são de 0 a 3600.|  
|rede\<enable&#124;disable>|Habilita ou desabilita o suporte de rede WS-AtomicTransaction.|  
|Porto\<portNum>|Define a porta HTTPS para WS-AtomicTransaction.<br /><br /> Se você já tiver habilitado o firewall antes de executar essa ferramenta, a porta será automaticamente registrada na lista de exceções. Se o firewall estiver desabilitado antes da execução dessa ferramenta, nada adicional será configurado com relação ao firewall.<br /><br /> Se você habilitar o firewall depois de configurar o WS-AT, você precisará executar essa ferramenta novamente e fornecer o número da porta usando esse parâmetro. Se você desabilitar o firewall após a configuração, o WS-AT continuará funcionando sem entrada adicional.|  
|cedido\<sec>|Especifica o tempo limite padrão em segundos. Os valores válidos são de 1 a 3600.|  
|-traceActivity:\<enable&#124;disable>|Habilita ou desabilita o rastreamento de eventos de atividade.|  
|-traceLevel: \<Off&#124;Error&#124;Critical&#124;Warning&#124;Information&#124; Verbose&#124;All> }|Especifica o nível de rastreamento.|  
|-tracePII:\<enable&#124;disable>|Habilita ou desabilita o rastreamento de informações de identificação pessoal.|  
|-traceProp:\<enable&#124;disable>|Habilita ou desabilita o rastreamento de eventos de propagação.|  
|-restart|Reinicia o MSDTC para ativar as alterações imediatamente. Se isso não for especificado, as alterações entrarão em vigor quando o MSDTC for reiniciado.|  
|-Mostrar|Exibe as configurações de protocolo de WS-AtomicTransaction atuais.|  
|servidor virtual\<virtualServer>|Especifica o nome do cluster de recursos do DTC.|  
  
## <a name="see-also"></a>Consulte também

- [Utilizando Transações WS-Atomic](./feature-details/using-ws-atomictransaction.md)
- [Configurando suporte de transações de WS-Atomic](./feature-details/configuring-ws-atomic-transaction-support.md)
