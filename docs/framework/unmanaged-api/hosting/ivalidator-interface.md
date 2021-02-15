---
description: 'Saiba mais sobre: interface IValidator'
title: Interface IValidator
ms.date: 03/30/2017
api_name:
- IValidator
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IValidator
helpviewer_keywords:
- IValidator interface [.NET Framework hosting]
ms.assetid: b297e3b0-20f9-478f-b707-5e2eecb2b5b2
topic_type:
- apiref
ms.openlocfilehash: bc18b68d0e9a0e978789ab92afaed28751925870
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99680090"
---
# <a name="ivalidator-interface"></a>Interface IValidator

Fornece métodos para validar imagens executáveis portáteis (PE) e relatar erros de validação.  
  
## <a name="methods"></a>Métodos  
  
|Método|DESCRIÇÃO|  
|------------|-----------------|  
|Validar|Valida o PE especificado ou o arquivo da MSIL (Microsoft Intermediate Language).|  
|FormatEventInfo|Obtém a mensagem de erro correspondente ao erro de validação especificado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** IValidator. idl, IValidator. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de hospedagem](hosting-interfaces.md)
- [Coclass CorRuntimeHost](corruntimehost-coclass.md)
