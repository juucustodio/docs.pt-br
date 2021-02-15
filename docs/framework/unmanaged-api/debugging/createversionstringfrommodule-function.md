---
description: 'Saiba mais sobre: função CreateVersionStringFromModule'
title: Função CreateVersionStringFromModule
ms.date: 03/30/2017
api_name:
- CreateVersionStringFromModule
api_location:
- dbgshim.dll
api_type:
- COM
f1_keywords:
- CreateVersionStringFromModule
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- CreateVersionStringFromModule function
ms.assetid: 3d2fe9bd-75ef-4364-84a6-da1e1994ac1a
topic_type:
- apiref
ms.openlocfilehash: 45ae3ec31cf77e4c96e42a58b23e1f52dcf7c54b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661539"
---
# <a name="createversionstringfrommodule-function"></a>Função CreateVersionStringFromModule

Cria uma cadeia de caracteres de versão de um caminho Common Language Runtime (CLR) em um processo de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateVersionStringFromModule (  
    [in]  DWORD      pidDebuggee,  
    [in]  LPCWSTR    szModuleName,  
    [out, size_is(cchBuffer),  
          length_is(*pdwLength)] LPWSTR Buffer,  
    [in]  DWORD      cchBuffer,  
    [out] DWORD*     pdwLength  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pidDebuggee`  
 no Identificador do processo no qual o CLR de destino é carregado.  
  
 `szModuleName`  
 no Caminho completo ou relativo para o CLR de destino que é carregado no processo.  
  
 `pBuffer`  
 fora Buffer de retorno para armazenar a cadeia de caracteres de versão para o CLR de destino.  
  
 `cchBuffer`  
 no Tamanho de `pBuffer` .  
  
 `pdwLength`  
 fora Comprimento da cadeia de caracteres de versão retornada por `pBuffer` .  
  
## <a name="return-value"></a>Valor retornado  

 S_OK  
 A cadeia de caracteres de versão para o CLR de destino foi retornada com êxito em `pBuffer` .  
  
 E_INVALIDARG  
 `szModuleName` é NULL ou `pBuffer` or `cchBuffer` é nulo. `pBuffer` e `cchBuffer` devem ser nulos ou não nulos.  
  
 HRESULT_FROM_WIN32 (ERROR_INSUFFICIENT_BUFFER)  
 `pdwLength` é maior que `cchBuffer`. Esse pode ser um resultado esperado se você tiver passado nulo para `pBuffer` and e `cchBuffer` , e tiver consultado o tamanho de buffer necessário usando `pdwLength` .  
  
 HRESULT_FROM_WIN32 (ERROR_MOD_NOT_FOUND)  
 `szModuleName` Não contém um caminho para um CLR válido no processo de destino.  
  
 E_FAIL (ou outros códigos de retorno de E_)  
 `pidDebuggee` Não se refere a um processo válido ou a outra falha.  
  
## <a name="remarks"></a>Comentários  

 Essa função aceita um processo CLR identificado pelo `pidDebuggee` e um caminho de cadeia de caracteres especificado por `szModuleName` . A cadeia de caracteres de versão é retornada no buffer que `pBuffer` aponta para. Essa cadeia de caracteres é opaca para o usuário da função; ou seja, não há nenhum significado intrínseco na própria cadeia de caracteres de versão. Ele é usado unicamente no contexto dessa função e da [função CreateDebuggingInterfaceFromVersion](createdebugginginterfacefromversion-function-for-silverlight.md).  
  
 Essa função deve ser chamada duas vezes. Quando você o chama pela primeira vez, passe NULL para `pBuffer` e `cchBuffer` . Quando você fizer isso, o tamanho do buffer necessário para `pBuffer` será retornado em `pdwLength` . Em seguida, você pode chamar a função uma segunda vez e passar o buffer para dentro `pBuffer` e seu tamanho em `cchBuffer` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** dbgshim. h  
  
 **Biblioteca:** dbgshim.dll  
  
 **Versões do .NET Framework:** 3,5 SP1
