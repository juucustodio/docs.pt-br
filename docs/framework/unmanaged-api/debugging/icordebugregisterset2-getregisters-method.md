---
description: 'Saiba mais sobre o método: ICorDebugRegisterSet2:: GetRegisters'
title: Método ICorDebugRegisterSet2::GetRegisters
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.GetRegisters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::GetRegisters
helpviewer_keywords:
- GetRegisters method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
- ICorDebugRegisterSet2::GetRegisters method [.NET Framework debugging]
ms.assetid: dbc498a8-ba3f-42f2-bdd9-b623c77a1019
topic_type:
- apiref
ms.openlocfilehash: 58af939b0e88185e2be23b69ca70d28e93ff873f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794764"
---
# <a name="icordebugregisterset2getregisters-method"></a>Método ICorDebugRegisterSet2:: GetRegisters

Obtém o valor de cada registro (para a plataforma em que o código está em execução no momento) que é especificado pela máscara de bits fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRegisters (  
    [in] ULONG32 maskCount,  
    [in, size_is(maskCount)] BYTE mask[],  
    [in] ULONG32 regCount,  
    [out, size_is(regCount)] CORDB_REGISTER regBuffer[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros

 `maskCount`  
 no O tamanho, em bytes, da `mask` matriz.  
  
 `mask`  
 no Uma matriz de bytes, cada bit corresponde a um registro. Se o bit for 1, o valor do registro correspondente será recuperado.  
  
 `regCount`  
 no O número de valores de registro a serem recuperados.  
  
 `regBuffer`  
 fora Uma matriz de `CORDB_REGISTER` objetos, cada um deles recebe o valor de um registro.  
  
## <a name="remarks"></a>Comentários

 O `GetRegisters` método retorna uma matriz de valores dos registros que são especificados pela máscara. A matriz não contém valores de registros cujo bit de máscara não esteja definido. Portanto, o tamanho da `regBuffer` matriz deve ser igual ao número de 1 na máscara. Se o valor de `regCount` for muito pequeno para o número de registros indicado pela máscara, os valores dos registros numerados mais altos serão truncados do conjunto. Se `regCount` for muito grande, os elementos não utilizados não `regBuffer` serão modificados.  
  
 Se um registro indisponível for indicado pela máscara, um valor indeterminado será retornado para esse registro.  
  
 O `ICorDebugRegisterSet2::GetRegisters` método é necessário para plataformas que têm mais de 64 registros. Por exemplo, IA64 tem 128 registros de uso geral e 128 registros de ponto flutuante, portanto, você precisa de mais de 64 bits na máscara de bits.  
  
 Se você não tiver mais de 64 registros, como é o caso em plataformas como x86, o `GetRegisters` método apenas converterá os bytes na `mask` matriz de bytes em um `ULONG64` e, em seguida, chamará o método [ICorDebugRegisterSet:: GetRegisters](icordebugregisterset-getregisters-method.md) , que usa a `ULONG64` máscara.  
  
## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
