---
description: 'Saiba mais sobre o método: ICorDebugILCode2:: GetLocalVarSigToken'
title: ICorDebugILCode2::Método GetLocalVarSigToken
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILCode2.GetLocalVarSigToken
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 17665b77-1342-4115-94fd-9f45b0ecfb0f
topic_type:
- apiref
ms.openlocfilehash: cdf2725274a132528123534ddd36ae95e265af44
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791420"
---
# <a name="icordebugilcode2getlocalvarsigtoken-method"></a>ICorDebugILCode2::Método GetLocalVarSigToken

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Obtém o token de metadados para a assinatura de variável local para a função que é representada por esta instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetLocalVarSigToken(  
   [out] mdSignature *pmdSig  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pmdSig`  
 [out] Um ponteiro para o token `mdSignature` para a assinatura de variável local desta função ou `mdSignatureNil` se não houver uma assinatura (isto é, se a função não tiver variáveis locais).  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugILCode2](icordebugilcode2-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
