---
title: Função ResetSecurity (referência de API não gerenciada)
description: A função ResetSecurity atribui um token de representação ao thread atual.
ms.date: 11/06/2017
api_name:
- ResetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ResetSecurity
helpviewer_keywords:
- ResetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 259bef74356f16221f1453dd4086e2fbb26faa83
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721108"
---
# <a name="resetsecurity-function"></a>Função ResetSecurity

Atribui o token de representação fornecido para o thread atual.
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ResetSecurity (
   [in] HANDLE token
);
```  

## <a name="parameters"></a>Parâmetros

`token`  
no O token de representação a ser associado ao thread atual. Seu valor pode ser `null`.

## <a name="return-value"></a>Valor retornado

Se a função for realizada com sucesso, o valor de retorno será `S_OK` (0).

Se a função falhar, o valor de retorno será um código de erro diferente de zero. Para obter informações de erro estendidas, chame a função [GetErrorInfo](geterrorinfo.md) .
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
