---
description: 'Saiba mais sobre: 218-ClientOperationCompleted'
title: 218 - ClientOperationCompleted
ms.date: 03/30/2017
ms.assetid: b069bced-7bb2-4e01-8227-e5dbda17af09
ms.openlocfilehash: 3719b77ce653c5177cf7b92901ecd51982504b83
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794332"
---
# <a name="218---clientoperationcompleted"></a>218 - ClientOperationCompleted

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|218|  
|Palavras-chave|Solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido por clientes logo após a conclusão de uma operação. Para operações unidirecionais, isso ocorre logo após a mensagem ser enviada com êxito. Para operações de solicitação-resposta, isso ocorre depois que a resposta é recebida.  
  
## <a name="message"></a>Mensagem  

 O cliente concluiu a execução da ação ' %1 ' associada ao contrato ' %2 '. A mensagem foi enviada para ' %3 '.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Ação|xs:string|O cabeçalho de ação SOAP da mensagem de saída.|  
|Nome do Contrato|`xs:string`|O nome do contrato. Exemplo: ICalculator.|  
|Destino|`xs:string`|O endereço do ponto de extremidade de serviço para o qual a mensagem foi enviada.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
