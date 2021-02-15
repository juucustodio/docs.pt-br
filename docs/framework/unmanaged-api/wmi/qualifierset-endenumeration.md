---
title: Função QualifierSet_EndEnumeration (referência de API não gerenciada)
description: A função QualifierSet_EndEnumeration encerra uma enumeração.
ms.date: 11/06/2017
api_name:
- QualifierSet_EndEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_EndEnumeration
helpviewer_keywords:
- QualifierSet_EndEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 2739003fc9c1f93d379e4a59338cbef7a1a0f135
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726737"
---
# <a name="qualifierset_endenumeration-function"></a>Função QualifierSet_EndEnumeration

Encerra a enumeração iniciada com uma chamada para a função [QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md) .  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT QualifierSet_EndEnumeration (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr` no Um ponteiro para uma instância de [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) .

## <a name="return-value"></a>Valor retornado

O valor a seguir retornado por essa função é definido no arquivo de cabeçalho *WbemCli. h* ou você pode defini-lo como uma constante no seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemQualifierSet:: endenumeration](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-endenumeration) .

Essa chamada é recomendada, mas não obrigatória. Ele libera imediatamente os recursos associados à enumeração.

## <a name="requirements"></a>Requisitos  

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
**Cabeçalho:** WMINet_Utils. idl  
  
**.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
