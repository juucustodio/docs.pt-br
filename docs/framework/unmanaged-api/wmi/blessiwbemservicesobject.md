---
title: Função BlessIWbemServicesObject (referência de API não gerenciada)
description: A função BlessIWbemServicesObject indica se as credenciais do usuário permitem o acesso a um objeto IWbemServices
ms.date: 11/06/2017
api_name:
- BlessIWbemServicesObject
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServicesObject
helpviewer_keywords:
- BlessIWbemServicesObject function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 1aab2076f57f938715a3e65481a3540dc52279c6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95719743"
---
# <a name="blessiwbemservicesobject-function"></a>Função BlessIWbemServicesObject

Indica se as credenciais do usuário permitem o acesso a um objeto [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) especificado.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT BlessIWbemServicesObject (
   [in] IUnknown* pIUnknown,
   [in] BSTR strUser,
   [in] BSTR strPassword,
   [in] BSTR strAuthority,
   [in] DWORD impLevel,
   [in] DWORD authnLevel
);
```

## <a name="parameters"></a>Parâmetros

`pIWbemServices`\
no Um ponteiro para um objeto de serviço WMI.

`strUser`\
no O nome de usuário.

`strPassword`\
no A senha associada a `strUser` .

`strAuthority`\
no O nome de domínio do usuário. Consulte a função [ConnectServerWmi](connectserverwmi.md) para obter mais informações.

`impLevel`\
no O nível de representação.

`authnLevel`\
no O nível de autorização.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *Winerror. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
| `E_INVALIDARG` | 0x80070057 | Um ou mais argumentos são inválidos. |
| `E_POINTER` | 0x80004003 | `pIWbemServices` é `null`. |
| `E_FAIL` | 0x80000008 | Ocorreu um erro não especificado. |
| `E_OUTOFMEMORY` | 0x80000002 | Memória insuficiente disponível para executar a operação. |
| `S_OK` | 0 | A chamada de função foi bem-sucedida. |

## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

 **Cabeçalho:** WMINet_Utils. idl

 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
