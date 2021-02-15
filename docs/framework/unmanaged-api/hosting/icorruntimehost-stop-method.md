---
description: 'Saiba mais sobre o método: ICorRuntimeHost:: Stop'
title: Método ICorRuntimeHost::Stop
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.Stop
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::Stop
helpviewer_keywords:
- Stop method, ICorRuntimeHost interface [.NET Framework hosting]
- ICorRuntimeHost::Stop method [.NET Framework hosting]
ms.assetid: 46a0d450-b516-4bef-8b71-8d3bf265cbed
topic_type:
- apiref
ms.openlocfilehash: b44c77b7d0fe3a078efa11756f5fac7ba400ca5e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789587"
---
# <a name="icorruntimehoststop-method"></a>Método ICorRuntimeHost::Stop

Interrompe a execução do código no tempo de execução para o processo atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Stop ();  
```  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A operação foi bem-sucedida.|  
|S_FALSE|Falha ao concluir a operação.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o Common Language Runtime (CLR) não poderá mais ser usado no processo. As chamadas subsequentes para qualquer API de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
  
## <a name="remarks"></a>Comentários  

 Normalmente, é desnecessário chamar o `Stop` método, pois o código para de ser executado quando o processo é encerrado.  
  
> [!NOTE]
> Após uma chamada para `Stop` , o CLR não pode ser reinicializado no mesmo processo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **Versões do .NET Framework:** 1,0, 1,1  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorRuntimeHost](icorruntimehost-interface.md)
