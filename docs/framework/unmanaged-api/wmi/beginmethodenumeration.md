---
title: Função BeginMethodEnumeration (referência de API não gerenciada)
description: A função BeginMethodEnumeration inicia uma enumeração dos métodos do objeto
ms.date: 11/06/2017
api_name:
- BeginMethodEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginMethodEnumeration
helpviewer_keywords:
- BeginMethodEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: a72d61a572a0582ed8c03e56a8a9933c5f2775f0
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95719756"
---
# <a name="beginmethodenumeration-function"></a>Função BeginMethodEnumeration

Inicia uma enumeração dos métodos disponíveis para o objeto.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT BeginMethodEnumeration (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lEnumFlags
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr`  
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`lEnumFlags`  
no Zero (0) para todos os métodos ou um sinalizador que especifica o escopo da enumeração. Os sinalizadores a seguir são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | Limitar a enumeração a métodos que são definidos na própria classe. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | Limite a enumeração a propriedades que são herdadas de classes base. |

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `lEnnumFlags` é diferente de zero e não é um dos sinalizadores especificados. |
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: BeginMethodEnumeration](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-beginmethodenumeration) .

Essa chamada de método só terá suporte se o objeto atual for uma definição de classe. A manipulação de método não está disponível em ponteiros [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) que apontam para instâncias. A ordem na qual os métodos são enumerados é garantida como invariável para uma determinada instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject).

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
