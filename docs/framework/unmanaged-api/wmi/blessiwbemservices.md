---
title: Função BlessIWbemServices (referência de API não gerenciada)
description: A função BlessIWbemServices indica se as credenciais do usuário permitem o acesso a uma classe IWbemServices.
ms.date: 11/06/2017
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 43ef617ee754c9dcd661b31abba6b17434563c22
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708147"
---
# <a name="blessiwbemservices-function"></a>Função BlessIWbemServices

Indica se as credenciais do usuário permitem o acesso à classe [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) especificada.
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser,
   [in] BSTR strPassword,
   [in] BSTR strAuthority,
   [in] DWORD impLevel,
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a>Parâmetros

`pIWbemServices`\
no Um ponteiro para o objeto [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) para o qual são necessárias permissões.

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

|Constante  |Valor  |Descrição  |
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
