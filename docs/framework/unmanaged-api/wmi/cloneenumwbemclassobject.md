---
title: Função CloneEnumWbemClassObject (referência de API não gerenciada)
description: A função CloneEnumWbemClassObject faz uma cópia lógica de um enumerador.
ms.date: 11/06/2017
api_name:
- CloneEnumWbemClassObject
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CloneEnumWbemClassObject
helpviewer_keywords:
- CloneEnumWbemClassObject function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: fa8a7f436c018e3e083be452d300eb21e17f93f3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708121"
---
# <a name="cloneenumwbemclassobject-function"></a>Função CloneEnumWbemClassObject

Faz uma cópia lógica de um enumerador, mantendo sua posição atual em uma enumeração.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CloneEnumWbemClassObject (
   [out] IEnumWbemClassObject**  ppEnum,
   [in] DWORD                    authLevel,
   [in] DWORD                    impLevel,
   [in] IEnumWbemClassObject*    pCurrentEnumWbemClassObject,
   [in] BSTR                     strUser,
   [in] BSTR                     strPassword,
   [in BSTR]                     strAuthority
);
```

## <a name="parameters"></a>Parâmetros

`ppEnum`\
fora Recebe um ponteiro para um novo [IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject).

`authLevel`\
no O nível de autorização.

`impLevel`\
no O nível de representação.

`pCurrentEnumWbemClassObject`\
fora Um ponteiro para a instância de [IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject) a ser clonada.

`strUser`\
no O nome de usuário. Consulte a função [ConnectServerWmi](connectserverwmi.md) para obter mais informações.

`strPassword`\
no A senha. Consulte a função [ConnectServerWmi](connectserverwmi.md) para obter mais informações.

`strAuthority`\
no O nome de domínio do usuário. Consulte a função [ConnectServerWmi](connectserverwmi.md) para obter mais informações.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | Houve uma falha geral. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um parâmetro é inválido. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Não há memória suficiente disponível conclua a operação. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | O link RPC (chamada de procedimento remoto) entre o processo atual e o WMI falhou. |
| `WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |

## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IEnumWbemClassObject:: clone](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone) .

Esse método faz apenas uma cópia "melhor esforço". Devido à natureza dinâmica de muitos objetos CIM, é possível que o novo enumerador não enumere o mesmo conjunto de objetos que o enumerador de origem.

Se a chamada de função falhar, você poderá obter informações adicionais sobre o erro chamando a função [GetErrorInfo](geterrorinfo.md) .

## <a name="example"></a>Exemplo

Para obter um exemplo, consulte o método [IEnumWbemClassObject:: clone](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone) .

## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

 **Cabeçalho:** WMINet_Utils. idl

 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
