---
title: Função GetMethodOrigin (referência de API não gerenciada)
description: A função GetMethodOrigin determina a classe na qual um método é declarado.
ms.date: 11/06/2017
api_name:
- GetMethodOrigin
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetMethodOrigin
helpviewer_keywords:
- GetMethodOrigin function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 434392ffb4d9124e319bcd9c42fdd340d3fec5b4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722772"
---
# <a name="getmethodorigin-function"></a>Função GetMethodOrigin

Determina a classe na qual um método é declarado.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMethodOrigin (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszMethodName,
   [out] BSTR*              pstrClassName
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr`  
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`wszMethodName`  
no O nome do método para o objeto cuja classe proprietária está sendo solicitada.

`pstrClassName`  
fora Recebe o nome da classe que possui o método.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | O método especificado não foi encontrado. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um ou mais parâmetros não são válidos. |
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: GetMethodOrigin](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getmethod) .

Como uma classe pode herdar métodos de uma ou mais classes base, os desenvolvedores geralmente desejam determinar a classe na qual um determinado método é definido.

O `pstrClassName` parâmetro não deve apontar para um válido `BSTR` antes que a função seja chamada porque esse é um `out` parâmetro; esse ponteiro não é desalocado depois que a função retorna.

## <a name="requirements"></a>Requisitos  

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
