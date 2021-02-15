---
title: Função NextMethod (referência de API não gerenciada)
description: A função NextMethod recupera o próximo método em uma enumeração.
ms.date: 11/06/2017
api_name:
- NextMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- NextMethod
helpviewer_keywords:
- NextMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: a0466aee47b0a6142870640c78b43f49e221ac2b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726763"
---
# <a name="nextmethod-function"></a>Função NextMethod

Recupera o próximo método em uma enumeração que começa com uma chamada para [BeginMethodEnumeration](beginmethodenumeration.md).  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT NextMethod (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr`  
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`lFlags`  
[in] Reservado. Esse parâmetro deve ser 0.

`pName`  
fora Um ponteiro que aponta para `null` antes da chamada. Quando a função retorna, o endereço de um novo `BSTR` que contém o nome do método.

`ppSignatureIn`  
fora Um ponteiro que recebe um ponteiro para um [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) que contém os `in` parâmetros para o método.

`ppSignatureOut`  
fora Um ponteiro que recebe um ponteiro para um [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) que contém os `out` parâmetros para o método.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | 0x8004101d | Não havia nenhuma chamada para a [`BeginEnumeration`](beginenumeration.md) função. |
| `WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | Não há mais propriedades na enumeração. |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) .

O chamador começa a sequência de enumeração chamando a função [BeginMethodEnumeration](beginmethodenumeration.md) e, em seguida, chama a função [NextMethod] até que a função retorne `WBEM_S_NO_MORE_DATA` . Opcionalmente, o chamador conclui a sequência chamando [EndMethodEnumeration](endmethodenumeration.md). O chamador pode encerrar a enumeração antecipadamente chamando [EndMethodEnumeration](endmethodenumeration.md) a qualquer momento.

## <a name="example"></a>Exemplo

Para obter um exemplo de C++, consulte o método [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) .

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
