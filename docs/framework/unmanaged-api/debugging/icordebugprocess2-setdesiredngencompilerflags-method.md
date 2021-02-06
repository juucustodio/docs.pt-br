---
description: 'Saiba mais sobre o método: ICorDebugProcess2:: SetDesiredNGENCompilerFlags'
title: Método ICorDebugProcess2::SetDesiredNGENCompilerFlags
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetDesiredNGENCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags
helpviewer_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags method [.NET Framework debugging]
- SetDesiredNGENCompilerFlags method [.NET Framework debugging]
ms.assetid: 98320175-7c5e-4dbb-8683-86fa82e2641f
topic_type:
- apiref
ms.openlocfilehash: 3a4749ad26e88d1a602876f28a52754323093fce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650060"
---
# <a name="icordebugprocess2setdesiredngencompilerflags-method"></a>Método ICorDebugProcess2::SetDesiredNGENCompilerFlags

Define os sinalizadores que devem ser inseridos em uma imagem pré-compilada para que o tempo de execução carregue essa imagem no processo atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetDesiredNGENCompilerFlags (  
    [in] DWORD    pdwFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwFlags`  
 no Um valor da enumeração [CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md) que especifica os sinalizadores de compilador usados para selecionar a imagem previamente compilada correta.  
  
## <a name="remarks"></a>Comentários  

 O `SetDesiredNGENCompilerFlags` método especifica os sinalizadores que devem ser inseridos em uma imagem pré-compilada para que o tempo de execução carregue essa imagem nesse processo. Os sinalizadores definidos por esse método são usados apenas para selecionar a imagem pré-compilada correta. Se essa imagem não existir, o tempo de execução carregará a imagem do Microsoft Intermediate Language (MSIL) e o compilador JIT (just-in-time). Nesse caso, o depurador ainda deve usar o método [ICorDebugModule2:: SetJITCompilerFlags](icordebugmodule2-setjitcompilerflags-method.md) para definir os sinalizadores conforme desejado para a compilação JIT.  
  
 Se uma imagem for carregada, mas alguma compilação JIT precisar ocorrer para essa imagem (que será o caso se a imagem contiver genéricos), os sinalizadores do compilador especificados pelo `SetDesiredNGENCompilerFlags` método serão aplicados à compilação adicional do JIT.  
  
 O `SetDesiredNGENCompilerFlags` método deve ser chamado durante o retorno de chamada [ICorDebugManagedCallback:: CreateProcess](icordebugmanagedcallback-createprocess-method.md) . Haverá falha nas tentativas de chamar o `SetDesiredNGENCompilerFlags` método posteriormente. Além disso, as tentativas de definir sinalizadores que não estão definidos na `CorDebugJITCompilerFlags` enumeração ou não são legais para o processo especificado falharão.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebug](icordebug-interface.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
