---
description: 'Saiba mais sobre o método: ICorDebugEval:: NewObjectNoConstructor'
title: Método ICorDebugEval::NewObjectNoConstructor
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewObjectNoConstructor
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewObjectNoConstructor
helpviewer_keywords:
- NewObjectNoConstructor method [.NET Framework debugging]
- ICorDebugEval::NewObjectNoConstructor method [.NET Framework debugging]
ms.assetid: 80d509ca-b5e3-4c46-9c14-800db73d9bf7
topic_type:
- apiref
ms.openlocfilehash: 4bc8f95da1a554091052dc7e7f49aef4f494578d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99693805"
---
# <a name="icordebugevalnewobjectnoconstructor-method"></a>Método ICorDebugEval::NewObjectNoConstructor

Aloca uma nova instância de objeto do tipo especificado, sem tentar chamar um método de construtor.  
  
 Esse método é obsoleto no .NET Framework versão 2,0. Use [ICorDebugEval2:: NewParameterizedObjectNoConstructor](icordebugeval2-newparameterizedobjectnoconstructor-method.md) em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT NewObjectNoConstructor (  
    [in] ICorDebugClass     *pClass  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pClass`  
 no Ponteiro para um objeto ICorDebugClass que representa o tipo de objeto a ser instanciado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Consulte também

- [Método NewParameterizedObjectNoConstructor](icordebugeval2-newparameterizedobjectnoconstructor-method.md)
