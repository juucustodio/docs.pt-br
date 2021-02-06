---
description: 'Saiba mais sobre o método: ICLRTask:: Reset'
title: Método ICLRTask::Reset
ms.date: 03/30/2017
api_name:
- ICLRTask.Reset
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::Reset
helpviewer_keywords:
- ICLRTask::Reset method [.NET Framework hosting]
- Reset method, ICLRTask interface [.NET Framework hosting]
ms.assetid: 1bfb5d3a-0ffd-4bb4-9bf6-aec00cb675b7
topic_type:
- apiref
ms.openlocfilehash: d30738b98003e0543c1a2a31c7471b15811efe5f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99636982"
---
# <a name="iclrtaskreset-method"></a>Método ICLRTask::Reset

Informa o Common Language Runtime (CLR) que o host concluiu uma tarefa e permite que o CLR reutilize a instância [ICLRTask](iclrtask-interface.md) atual para representar outra tarefa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Reset (  
    [in] BOOL fFull  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fFull`  
 [in] `true` , se o tempo de execução deve redefinir todos os valores estáticos relacionados ao thread, além das informações de segurança e localidade relacionadas à `ICLRTask` instância atual; caso contrário, `false` .  
  
 Se o valor for `true` , o tempo de execução redefinirá os dados que foram armazenados usando o <xref:System.Threading.Thread.AllocateDataSlot%2A> ou o <xref:System.Threading.Thread.AllocateNamedDataSlot%2A> .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`Reset` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada. com êxito|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O CLR pode reciclar instâncias criadas anteriormente `ICLRTask` para evitar a sobrecarga de criar novas instâncias repetidamente toda vez que precisar de uma nova tarefa. O host habilita esse recurso chamando `ICLRTask::Reset` em vez de [ICLRTask:: ExitTask](iclrtask-exittask-method.md) quando concluiu uma tarefa. A lista a seguir resume o ciclo de vida normal de uma `ICLRTask` instância do:  
  
1. O tempo de execução cria uma nova `ICLRTask` instância.  
  
2. O tempo de execução chama [IHostTaskManager:: GetCurrentTask](ihosttaskmanager-getcurrenttask-method.md) para obter uma referência à tarefa de host atual.  
  
3. O tempo de execução chama [IHostTask:: SetCLRTask](ihosttask-setclrtask-method.md) para associar a nova instância à tarefa do host.  
  
4. A tarefa é executada e concluída.  
  
5. O host destrói a tarefa chamando `ICLRTask::ExitTask` .  
  
 `Reset` altera esse cenário de duas maneiras. Na etapa 5 acima, o host chama `Reset` para redefinir a tarefa para um estado limpo e, em seguida, dissocia a `ICLRTask` instância de sua instância [IHostTask](ihosttask-interface.md) associada. Se desejar, o host também pode armazenar em cache a `IHostTask` instância para reutilização. Na etapa 1 acima, o tempo de execução efetua pull `ICLRTask` de uma reciclagem do cache em vez de criar uma nova instância.  
  
 Essa abordagem funciona bem quando o host também tem um pool de tarefas de trabalho reutilizáveis. Quando o host destrói uma de suas `IHostTask` instâncias, ele destrói o correspondente `ICLRTask` chamando `ExitTask` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRTask](iclrtask-interface.md)
- [Interface ICLRTaskManager](iclrtaskmanager-interface.md)
- [Interface IHostTask](ihosttask-interface.md)
- [Interface IHostTaskManager](ihosttaskmanager-interface.md)
