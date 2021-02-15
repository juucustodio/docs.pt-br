---
description: 'Saiba mais sobre o método: ICorDebugRegisterSet:: GetRegisters'
title: Método ICorDebugRegisterSet::GetRegisters
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet.GetRegisters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet::GetRegisters
helpviewer_keywords:
- GetRegisters method, ICorDebugRegisterSet interface [.NET Framework debugging]
- ICorDebugRegisterSet::GetRegisters method [.NET Framework debugging]
ms.assetid: fdf91864-48ea-4aa6-b70c-361b7a3184c7
topic_type:
- apiref
ms.openlocfilehash: efb0f19fe9eb823912203b82267803739fc3e2cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690841"
---
# <a name="icordebugregistersetgetregisters-method"></a>Método ICorDebugRegisterSet::GetRegisters

Obtém o valor de cada registro (no computador que está executando o código) que é especificado pela máscara de bits.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRegisters (  
    [in] ULONG64       mask,
    [in] ULONG32       regCount,  
    [out, size_is(regCount), length_is(regCount)]  
        CORDB_REGISTER regBuffer[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `mask`  
 no Uma máscara de bits que especifica quais valores de registro devem ser recuperados. Cada bit corresponde a um registro. Se um bit for definido como um, o valor do registro será recuperado; caso contrário, o valor do registro não será recuperado.  
  
 `regCount`  
 no O número de valores de registro a serem recuperados.  
  
 `regBuffer`  
 fora Uma matriz de `CORDB_REGISTER` objetos, cada um deles recebe um valor de um registro.  
  
## <a name="remarks"></a>Comentários  

 O tamanho da matriz deve ser igual ao número de bits definido como um na máscara de bits. O `regCount` parâmetro especifica o número de elementos no buffer que receberão os valores de registro. Se o `regCount` valor for muito pequeno para o número de registros indicado pela máscara, os registros numerados mais altos serão truncados do conjunto. Se o `regCount` valor for muito grande, os elementos não utilizados não `regBuffer` serão modificados.  
  
 Se a máscara de bits especificar um registro que não está disponível, o `GetRegisters` retornará um valor indeterminado para esse registro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
- [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
