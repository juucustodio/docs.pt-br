---
title: Função DeleteMethod (referência de API não gerenciada)
description: A função DeleteMethod exclui o método especificado de uma definição de classe CIM.
ms.date: 11/06/2017
api_name:
- DeleteMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- DeleteMethod
helpviewer_keywords:
- DeleteMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 8ca58ed3510360b20577890055e4284869d1bf94
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708095"
---
# <a name="deletemethod-function"></a>Função DeleteMethod

Exclui o método especificado de uma definição de classe CIM.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Delete (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr`  
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`wszName`  
no O nome do método a ser removido da tabela de classes. `wszName` deve ser um ponteiro para um válido `LPCWSTR` .

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_E_NOT_FOUND` | 0x80041002 | O método especificado não existe. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Não há memória suficiente para concluir a operação. |
| `WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |

## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject::D eletemethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-deletemethod) .

Não há suporte para exclusão de método para ponteiros [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) que apontam para instâncias de CIM.

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
