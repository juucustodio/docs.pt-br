---
title: Função GetDemultiplexedStub (referência de API não gerenciada)
description: A função GetDemultiplexedStub cria um coletor de encaminhador de objetos para ajudar um cliente a receber chamadas assíncronas do gerenciamento do Windows.
ms.date: 11/06/2017
api_name:
- GetDemultiplexedStub
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetDemultiplexedStub
helpviewer_keywords:
- GetDemultiplexedStub function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: f8f9b56268168bb16c476a9366facd17e8ac44e5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730624"
---
# <a name="getdemultiplexedstub-function"></a>Função GetDemultiplexedStub

Cria um coletor do encaminhador de objeto para ajudar um cliente a receber chamadas assíncronas do Gerenciamento do Windows.
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDemultiplexedStub (
   [in] IUnknown*    pObject,
   [in] boolean      isLocal,
   [out] IUnknown**  ppObject
);
```  

## <a name="parameters"></a>Parâmetros

`pObject`  
no Um ponteiro para a implementação em processo do cliente do [IWbemObjectSink](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectsink).

`isLocal`  
no Um sinalizador que indica se o evento é local ( `true` ); caso contrário, `false` .

`ppObject`  
fora Um coletor de encaminhador de objetos para auxiliar um cliente no recebimento de chamadas assíncronas do gerenciamento do Windows.

## <a name="return-value"></a>Valor retornado

Se a função for realizada com sucesso, o valor de retorno será `S_OK` (0).

Se a função falhar, o valor de retorno será um código de erro diferente de zero. Para obter informações de erro estendidas, chame a função [GetErrorInfo](geterrorinfo.md) .

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
