---
description: 'Saiba mais sobre o método: ICorDebugILFrame4:: GetCodeEx'
title: ICorDebugILFrame4::Método GetCodeEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetLocalVariableEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: aeda0e42-29ee-4ca8-9f21-ac4641677a62
topic_type:
- apiref
ms.openlocfilehash: 1d17dfa531354b8a4b0dd3c0d3d2eb47206900cc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791225"
---
# <a name="icordebugilframe4getcodeex-method"></a>ICorDebugILFrame4::Método GetCodeEx

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Obtém um ponteiro para o código que este registro de ativação está executando.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetCodeEx(  
   [in] ILCodeKind flags,
   [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `flags`  
 no Um membro de enumeração [ILCodeKind](ilcodekind-enumeration.md) que especifica se a Il (linguagem intermediária) definida pela solicitação ReJIT do criador de perfil está incluída no quadro.  
  
 `ppCode`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugCode" que representa o código que esse quadro de pilha está executando.  
  
## <a name="remarks"></a>Comentários  

 Esse método é semelhante ao método [ICorDebugFrame:: GetCode](icordebugframe-getcode-method.md) , exceto pelo fato de que ele acessa opcionalmente o código definido pela solicitação ReJIT do criador de perfil. Chamar esse método com um `flags` valor de `ILCODE_ORIGINAL_IL` é equivalente a chamar [GetCode](icordebugframe-getcode-method.md); se o método for instrumentado, seu Il não estará acessível. `ILCODE_REJIT_IL` permite que o depurador acesse a IL definida pela solicitação ReJIT do criador de perfil. Se o IL não for instrumentado, `ppCode` será **NULL** e o método retornará `S_OK` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugILFrame4](icordebugilframe4-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [ReJIT: um guia de How-To](/archive/blogs/davbr/rejit-a-how-to-guide)
