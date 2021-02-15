---
title: Função BeginEnumeration (referência de API não gerenciada)
description: A função BeginEnumeration redefine um enumerador para o início da enumeração
ms.date: 11/06/2017
api_name:
- BeginEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginEnumeration
helpviewer_keywords:
- BeginEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 6057526ddbe2efed65f8569e829c35524829e43e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708212"
---
# <a name="beginenumeration-function"></a>Função BeginEnumeration

Redefine um enumerador de volta para o início da enumeração.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT BeginEnumeration (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lEnumFlags
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`\
no Este parâmetro não é usado.

`ptr`\
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`lEnumFlags`\
no Uma combinação de bits de bit que indica os sinalizadores ou valores descritos na seção [comentários](#remarks) que controla as propriedades incluídas na enumeração.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | A combinação de sinalizadores no `lEnumFlags` é inválida ou um argumento inválido foi especificado. |
|`WBEM_E_UNEXPECTED` | 0x8004101d | Uma segunda chamada para `BeginEnumeration` foi feita sem uma chamada intermediária para [`EndEnumeration`](endenumeration.md) . |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Não há memória suficiente disponível para iniciar uma nova enumeração. |
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: BeginEnumeration](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

Os sinalizadores que podem ser passados como o `lEnumFlags` argumento são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código.  Você pode combinar um sinalizador de cada grupo com qualquer sinalizador de qualquer outro grupo. No entanto, os sinalizadores do mesmo grupo são mutuamente exclusivos.

**Grupo 1**

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | Inclua propriedades que constituem apenas a chave. |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | Inclua propriedades que são referências de objeto apenas. |

**Grupo 2**

Constante  |Valor  |Descrição  |
|---------|---------|---------|
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | Limitar a enumeração somente às propriedades do sistema. |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | Incluir propriedades locais e propagadas, mas excluir propriedades do sistema da enumeração. |

Para classes:

Constante  |Valor  |Descrição  |
|---------|---------|---------|
|`WBEM_FLAG_CLASS_OVERRIDES_ONLY` | 0x100 | Limite a enumeração às propriedades substituídas na definição de classe. |
|`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` | 0x100 | Limitar a enumeração às propriedades substituídas na definição de classe atual e às novas propriedades definidas na classe. |
| `WBEM_MASK_CLASS_CONDITION` | 0x300 | Uma máscara (em vez de um sinalizador) a ser aplicada a um `lEnumFlags` valor para verificar se `WBEM_FLAG_CLASS_OVERRIDES_ONLY` ou `WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` está definido. |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | Limite a enumeração a propriedades que são definidas ou modificadas na própria classe. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | Limite a enumeração a propriedades que são herdadas de classes base. |

Para instâncias:

Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | Limite a enumeração a propriedades que são definidas ou modificadas na própria classe. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | Limite a enumeração a propriedades que são herdadas de classes base. |

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
