---
title: Função QualifierSet_Get (referência de API não gerenciada)
description: A função QualifierSet_Get Obtém um qualificador nomeado.
ms.date: 11/06/2017
api_name:
- QualifierSet_Get
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Get
helpviewer_keywords:
- QualifierSet_Get function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: fd096287b85b4a51a8cae85dddcca95cc1a8dbae
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721134"
---
# <a name="qualifierset_get-function"></a>Função QualifierSet_Get

Obtém o qualificador nomeado especificado.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT QualifierSet_Get (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LPCWSTR              wszName,
   [in] LONG                 lFlags,
   [out] VARIANT*            pVal,
   [out] LONG*               plFlavor
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc` no Este parâmetro não é usado.

`ptr` no Um ponteiro para uma instância de [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) .

`wszName` no O nome do qualificador cujo valor é solicitado.

`lFlags` no Reservado. Esse parâmetro deve ser 0.

`pVal` fora Quando bem-sucedido, o tipo e o valor corretos para o qualificador. Se a função falhar, a `VARIANT` apontada para by `pVal` não será modificada. Se esse parâmetro for `null` , o parâmetro será ignorado.

`plFlavor` fora Um ponteiro para um longo que recebe os bits de tipo de qualificador para o qualificador solicitado. Se as informações do tipo não forem desejadas, esse parâmetro poderá ser `null` .

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um parâmetro não é válido. |
|`WBEM_E_NOT_FOUND` | 0x80041002 | O qualificador especificado não existe. |
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemQualifierSet:: Get](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-get) .

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
