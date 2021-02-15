---
description: 'Saiba mais sobre: interface ICLRValidator'
title: Interface ICLRValidator
ms.date: 03/30/2017
api_name:
- ICLRValidator
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRValidator
helpviewer_keywords:
- ICLRValidator interface [.NET Framework hosting]
ms.assetid: 2edd0a10-77fb-4173-91eb-f2970cc364d0
topic_type:
- apiref
ms.openlocfilehash: 72ff94915d35967b6a8a87b022789ca697f61711
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99636743"
---
# <a name="iclrvalidator-interface"></a>Interface ICLRValidator

Fornece métodos para validar imagens executáveis portáteis (PE) e relatar erros de validação.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método FormatEventInfo](iclrvalidator-formateventinfo-method.md)|Obtém uma mensagem detalhada sobre o erro de validação especificado.|  
|[Método Validate](iclrvalidator-validate-method.md)|Valida o executável portátil ou o MSIL (Microsoft Intermediate Language) no arquivo especificado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** IValidator. idl, IValidator. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Coclass CLRRuntimeHost](clrruntimehost-coclass.md)
