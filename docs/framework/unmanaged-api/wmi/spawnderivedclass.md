---
title: Função SpawnDerivedClass (referência de API não gerenciada)
description: A função SpawnDerivedClass cria um novo objeto que deriva de um objeto.
ms.date: 11/06/2017
api_name:
- SpawnDerivedClass
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnDerivedClass
helpviewer_keywords:
- SpawnDerivedClass function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 8020dd851b6773e6c76c53892c4b2bc21e4261bb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716506"
---
# <a name="spawnderivedclass-function"></a>Função SpawnDerivedClass

Cria um objeto de classe derivada recentemente por meio de um objeto especificado.
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SpawnDerivedClass (
   [in] int                  vFunc,
   [in] IWbemClassObject*    ptr,
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewClass);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr`  
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`lFlags`  
[in] Reservado. Esse parâmetro deve ser 0.

`ppNewClass`  
fora Recebe o ponteiro para o novo objeto de definição de classe. Se ocorrer um erro, um novo objeto não será retornado e `ppNewClass` permanecerá não modificado. Seu valor não pode ser `null` .

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | Houve uma falha geral. |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | Uma operação inválida, como a geração de uma classe de uma instância, foi solicitada. |
| `WBEM_E_INCOMPLETE_CLASS` | A classe de origem não foi totalmente definida ou registrada com o gerenciamento do Windows, portanto, não é permitida uma nova classe derivada. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Não há memória disponível suficiente para concluir a operação. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass` é `null`. |
| `WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: SpawnDerivedClass](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-clone) .

`ptr` deve ser uma definição de classe que se torna a classe pai do objeto gerado. O objeto retornado se torna uma subclasse do objeto atual.

O novo objeto retornado em `ppNewClass` torna-se automaticamente uma subclasse do objeto atual. Esse comportamento não pode ser substituído. Não há nenhum outro método pelo qual as subclasses (classes derivadas) podem ser criadas.

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
