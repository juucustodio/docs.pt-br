---
title: Próxima função (referência de API não gerenciada)
description: A função Next recupera a próxima Propriedade em uma enumeração.
ms.date: 11/06/2017
api_name:
- Next
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Next
helpviewer_keywords:
- Next function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: c2a7fae32e82caae40a95bfdad10fa78082988ef
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726776"
---
# <a name="next-function"></a>Função Next

Recupera a próxima Propriedade em uma enumeração que começa com uma chamada para [BeginEnumeration](beginenumeration.md).

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Next (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lFlags,
   [out] BSTR*            pstrName,
   [out] VARIANT*         pVal,
   [out] CIMTYPE*         pvtType,
   [out] LONG*            plFlavor
);
```

## <a name="parameters"></a>Parâmetros

`vFunc`\
no Este parâmetro não é usado.

`ptr`\
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`lFlags`\
[in] Reservado. Esse parâmetro deve ser 0.

`pstrName`\
fora Um novo `BSTR` que contém o nome da propriedade. Você pode definir esse parâmetro como `null` se o nome não for necessário.

`pVal`\
fora Um `VARIANT` preenchido com o valor da propriedade. Você pode definir esse parâmetro como `null` se o valor não for necessário. Se a função retornar um código de erro, o `VARIANT` passado para `pVal` será deixado sem modificações.

`pvtType`\
fora Um ponteiro para uma `CIMTYPE` variável (um `LONG` no qual o tipo da propriedade é colocado). O valor dessa propriedade pode ser a `VT_NULL_VARIANT` ; nesse caso, é necessário determinar o tipo real da propriedade. Esse parâmetro também pode ser `null` .

`plFlavor`\
[out] `null` ou um valor que recebe informações sobre a origem da propriedade. Consulte a seção [Comentários] para obter os valores possíveis.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | Houve uma falha geral. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um parâmetro é inválido. |
| `WBEM_E_UNEXPECTED` | 0x8004101d | Não havia nenhuma chamada para a [`BeginEnumeration`](beginenumeration.md) função. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Não há memória suficiente disponível para iniciar uma nova enumeração. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | A chamada de procedimento remoto entre o processo atual e o gerenciamento do Windows falhou. |
| `WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | Não há mais propriedades na enumeração. |

## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-next) .

Esse método também retorna propriedades do sistema.

Se o tipo subjacente da propriedade for um caminho de objeto, uma data ou hora ou outro tipo especial, o tipo retornado não conterá informações suficientes. O chamador deve examinar a `CIMTYPE` propriedade especificada para determinar se a propriedade é uma referência de objeto, uma data ou hora ou outro tipo especial.

Se `plFlavor` não for `null` , o `LONG` valor receberá informações sobre a origem da propriedade, da seguinte maneira:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | 0x40 | A propriedade é uma propriedade padrão do sistema. |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | 0x20 | Para uma classe: a propriedade é herdada da classe pai. <br> Para uma instância: a propriedade, embora herdada da classe pai, não foi modificada pela instância.  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | 0 | Para uma classe: a propriedade pertence à classe derivada. <br> Para uma instância: a propriedade é modificada pela instância; ou seja, um valor foi fornecido ou um qualificador foi adicionado ou modificado. |

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** WMINet_Utils. idl

**.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
