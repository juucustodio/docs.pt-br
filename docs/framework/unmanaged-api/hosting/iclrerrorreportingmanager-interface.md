---
description: 'Saiba mais sobre: interface ICLRErrorReportingManager'
title: Interface ICLRErrorReportingManager
ms.date: 03/30/2017
api_name:
- ICLRErrorReportingManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRErrorReportingManager
helpviewer_keywords:
- ICLRErrorReportingManager interface [.NET Framework hosting]
ms.assetid: ea8af0d5-4133-4472-8a1f-50570d7e85fa
topic_type:
- apiref
ms.openlocfilehash: 094fe52858983fd0e1e5826e823932cb150b6087
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689268"
---
# <a name="iclrerrorreportingmanager-interface"></a>Interface ICLRErrorReportingManager

Fornece métodos que permitem ao host configurar despejos de pilha personalizados para o relatório de erros.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método BeginCustomDump](iclrerrorreportingmanager-begincustomdump-method.md)|Especifica a configuração de despejos de pilha personalizados para o relatório de erros.|  
|[Método EndCustomDump](iclrerrorreportingmanager-endcustomdump-method.md)|Limpa a configuração de despejo de pilha personalizado que foi definida por uma chamada anterior para `BeginCustomDump` .|  
|[Método GetBucketParametersForCurrentException](iclrerrorreportingmanager-getbucketparametersforcurrentexception-method.md)|Obtém o Bucket do Watson para a exceção atual no thread de chamada.|  
  
## <a name="remarks"></a>Comentários  

 O `BeginCustomDump` método define a configuração de despejo de pilha personalizado. O `EndCustomDump` método limpa a configuração de despejo de pilha personalizada e libera qualquer estado associado. Ele deve ser chamado após a conclusão do despejo personalizado.  
  
> [!IMPORTANT]
> Falha ao chamar `EndCustomDump` faz com que a memória seja vazada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração ECustomDumpItemKind](ecustomdumpitemkind-enumeration.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
