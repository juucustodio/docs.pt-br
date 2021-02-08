---
description: 'Saiba mais sobre o método: ICorDebugRemote:: CreateProcessEx'
title: Método ICorDebugRemote::CreateProcessEx
ms.date: 03/30/2017
api_name:
- ICorDebugRemote.CreateProcessEx
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugRemoteTarget::CreateProcessEx
helpviewer_keywords:
- CreateProcessEx method, ICorDebugRemote interface [.NET Framework debugging]
- ICorDebugRemote::CreateProcessEx method [.NET Framework debugging]
ms.assetid: 41af93c7-e448-4251-8d4d-413d38c635f2
topic_type:
- apiref
ms.openlocfilehash: cd27400f5c9f348621fb66b3b7730cf15d397151
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794722"
---
# <a name="icordebugremotecreateprocessex-method"></a>Método ICorDebugRemote::CreateProcessEx

Inicia um processo em um computador remoto sob o depurador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateProcessEx (  
    [in]  ICorDebugRemoteTarget*      pRemoteTarget,  
    [in]  LPCWSTR                     lpApplicationName,  
    [in]  LPWSTR                      lpCommandLine,  
    [in]  LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
    [in]  LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
    [in]  BOOL                        bInheritHandles,  
    [in]  DWORD                       dwCreationFlags,  
    [in]  PVOID                       lpEnvironment,  
    [in]  LPCWSTR                     lpCurrentDirectory,  
    [in]  LPSTARTUPINFOW              lpStartupInfo,  
    [in]  LPPROCESS_INFORMATION       lpProcessInformation,  
    [in]  CorDebugCreateProcessFlags  debuggingFlags,  
    [out] ICorDebugProcess**          ppProcess  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pRemoteTarget`  
 no Ponteiro para uma [interface ICorDebugRemoteTarget](icordebugremotetarget-interface.md). Usado para determinar o computador remoto no qual o processo será iniciado.  
  
 `lpApplicationName`  
 no Ponteiro para uma cadeia de caracteres terminada em nulo que especifica o módulo a ser executado pelo processo iniciado. O módulo é executado no contexto de segurança do processo de chamada.  
  
 `lpCommandLine`  
 no Ponteiro para uma cadeia de caracteres terminada em nulo que especifica a linha de comando a ser executada pelo processo iniciado.  
  
 `lpProcessAttributes`  
 no Não usado para depuração remota.  
  
 `lpThreadAttributes`  
 no Não usado para depuração remota.  
  
 `bInheritHandles`  
 no Não usado para depuração remota.  
  
 `dwCreationFlags`  
 no Não usado para depuração remota.  
  
 `lpEnvironment`  
 no Ponteiro para um bloco de ambiente para o novo processo.  
  
 `lpCurrentDirectory`  
 no Ponteiro para uma cadeia de caracteres terminada em nulo que especifica o caminho completo para o diretório atual para o processo. Se esse parâmetro for nulo, o novo processo terá a mesma unidade e diretório atuais que o processo de chamada.  
  
 `lpStartupInfo`  
 no Não usado para depuração remota.  
  
 `lpProcessInformation`  
 no Não usado para depuração remota.  
  
 `debuggingFlags`  
 no Não usado para depuração remota.  
  
 `ppProcess`  
 fora Um ponteiro para o endereço de um objeto "interface ICorDebugProcess" que representa o processo.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK  
 O processo foi iniciado com êxito no computador remoto e retornou uma "interface ICorDebugProcess" para depuração.  
  
 E_FAIL (ou outros códigos de retorno de E_)  
 Não é possível iniciar o processo no computador remoto e retornar uma "interface ICorDebugProcess" para depuração.  
  
## <a name="remarks"></a>Comentários  

 Não há suporte para a depuração de modo misto no Silverlight.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 4,5, 4, 3,5 SP1  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRemote](icordebugremote-interface.md)
- [Interface ICorDebug](icordebug-interface.md)

- [Depurando interfaces](debugging-interfaces.md)
