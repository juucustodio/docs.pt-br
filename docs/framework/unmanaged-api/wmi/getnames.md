---
title: Função GetNames (referência de API não gerenciada)
description: A função GetNames recupera os nomes das propriedades de um objeto.
ms.date: 11/06/2017
api_name:
- GetNames
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetNames
helpviewer_keywords:
- GetNames function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: fd889158e61b86f42d88bcf86eda7d816277e6ac
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95687652"
---
# <a name="getnames-function"></a>Função GetNames

Recupera um subconjunto ou todos os nomes das propriedades de um objeto.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNames (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszQualifierName,
   [in] LONG                lFlags,
   [in] VARIANT*            pQualifierValue,
   [out] SAFEARRAY (BSTR)** pstrNames
);
```  

## <a name="parameters"></a>Parâmetros

`vFunc`  
no Este parâmetro não é usado.

`ptr`  
no Um ponteiro para uma instância de [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`wszQualifierName`  
no Um ponteiro para um válido `LPCWSTR` que especifica um nome de qualificador que funciona como parte de um filtro. Para obter mais informações, consulte a seção [comentários](#remarks) . Esse parâmetro pode ser `null`.

`lFlags`  
no Uma combinação de campos de bits. Para obter mais informações, consulte a seção [comentários](#remarks) .

`pQualifierValue` no Um ponteiro para uma `VARIANT` estrutura válida inicializada para um valor de filtro. Esse parâmetro pode ser `null`.

`pstrNames`  
fora Uma `SAFEARRAY` estrutura que contém nomes de propriedade. Na entrada, esse parâmetro sempre deve ser um ponteiro para `null` . Consulte a seção [comentários](#remarks) para obter mais informações.

## <a name="return-value"></a>Valor retornado

Os valores a seguir retornados por essa função são definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | Houve uma falha geral. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um ou mais parâmetros não são válidos ou uma combinação incorreta de sinalizadores e parâmetros foi especificada. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Não há memória disponível suficiente para concluir a operação. |
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o método [IWbemClassObject:: GetNames](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getnames) .

O nome retornado é controlado por uma combinação de sinalizadores e parâmetros. Por exemplo, a função pode retornar os nomes de todas as propriedades ou apenas os nomes das propriedades de chave.  O filtro primário é especificado no `lFlags` parâmetro e os outros parâmetros variam dependendo dele.

Os valores de sinalizador no `lFlags` são campos de bits

Os sinalizadores que podem ser passados como o `lEnumFlags` argumento são campos de bits definidos no arquivo de cabeçalho *WbemCli. h* ou você pode defini-los como constantes em seu código.  Você pode combinar um sinalizador de cada grupo com qualquer sinalizador de qualquer outro grupo. No entanto, os sinalizadores do mesmo grupo são mutuamente exclusivos.

| Sinalizadores do grupo 1 |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
| `WBEM_FLAG_ALWAYS` | 0 | Retornar todos os nomes de propriedade. `strQualifierName` e `pQualifierVal` não são usados. |
| `WBEM_FLAG_ONLY_IF_TRUE` | 1 | Retornar apenas as propriedades que têm um qualificador do nome especificado pelo `strQualifierName` parâmetro. Se esse sinalizador for usado, você deverá especificar `strQualifierName` . |
|`WBEM_FLAG_ONLY_IF_FALSE` | 2 |  Retornar apenas propriedades que não têm um qualificador do nome especificado pelo `strQualifierName` parâmetro. Se esse sinalizador for usado, você deverá especificar `strQualifierName` . |
|`WBEM_FLAG_ONLY_IF_IDENTICAL` | 3 | Retornam apenas propriedades que têm um qualificador do nome especificado pelo `wszQualifierName` parâmetro e também têm um valor idêntico ao especificado pela `pQualifierVal` estrutura. Se esse sinalizador for usado, você deverá especificar um `wszQualifierName` e um `pQualifierValue` . |

| Sinalizadores do grupo 2 |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | Retornar somente os nomes das propriedades que definem as chaves. |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | Retornar apenas nomes de propriedade que são referências de objeto. |

| Sinalizadores do grupo 3 |Valor  |DESCRIÇÃO  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | Retornar apenas os nomes de propriedade que pertencem à classe mais derivada. Exclua as propriedades das classes pai. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | Retornar apenas os nomes de propriedade que pertencem às classes pai. |
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | Retornar apenas os nomes das propriedades do sistema. |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | Retornar apenas os nomes das propriedades que não são do sistema. |

A função sempre aloca um novo `SAFEARRAY` se ele retornar `WBEM_S_NO_ERROR` e `pstrNames` sempre será definido para apontar para ele. A matriz retornada pode ter 0 elementos se nenhuma propriedade corresponder aos filtros especificados. Se a função retornar um valor diferente de `WBM_S_NO_ERROR` , uma nova `SAFEARRAY` estrutura não será retornada.

## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils. idl  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Confira também

- [WMI e Contadores de Desempenho (Referência de API Não Gerenciada)](index.md)
