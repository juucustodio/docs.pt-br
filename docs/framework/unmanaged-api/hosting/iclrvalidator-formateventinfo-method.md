---
description: 'Saiba mais sobre o método: ICLRValidator:: FormatEventInfo'
title: Método ICLRValidator::FormatEventInfo
ms.date: 03/30/2017
api_name:
- ICLRValidator.FormatEventInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRValidator::FormatEventInfo
helpviewer_keywords:
- FormatEventInfo method, ICLRValidator interface [.NET Framework hosting]
- ICLRValidator::FormatEventInfo method [.NET Framework hosting]
ms.assetid: 808e1f1d-52f4-47c4-83cc-dcf47d075219
topic_type:
- apiref
ms.openlocfilehash: 3d8d1eff8c638517e201905d0313ee824490acf4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99636761"
---
# <a name="iclrvalidatorformateventinfo-method"></a>Método ICLRValidator::FormatEventInfo

Obtém uma mensagem detalhada sobre o erro de validação especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT FormatEventInfo (  
    [in] HRESULT            hVECode,  
    [in] VEContext          Context,  
    [in, out] LPWSTR        msg,  
    [in] unsigned long      ulMaxLength,  
    [in] SAFEARRAY(VARIANT) psa  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `hVECode`  
 no O valor HRESULT que foi passado para o manipulador de erro de validação.  
  
 `Context`  
 no Uma `VEContext` instância que contém informações de contexto sobre os erros de validação.  
  
 `msg`  
 [entrada, saída] A mensagem de erro amigável.  
  
 `ulMaxLength`  
 no O comprimento máximo da mensagem de erro.  
  
 `psa`  
 no Uma matriz segura de parâmetros adicionais a serem usados na mensagem.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`FormatEventInfo` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** IValidator. idl, IValidator. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)
- [Interface ICLRValidator](iclrvalidator-interface.md)
