---
description: 'Saiba mais sobre: função DestroyICeeFileGen'
title: Função DestroyICeeFileGen
ms.date: 03/30/2017
api_name:
- DestroyICeeFileGen
api_location:
- mscoree.dll
- mscorpehost.dll
- mscorpe.dll
api_type:
- COM
f1_keywords:
- DestroyICeeFileGen
helpviewer_keywords:
- DestroyICeeFileGen function [.NET Framework hosting]
ms.assetid: dc1e2235-e721-4cb2-a0b8-6b0c030d7bab
topic_type:
- apiref
ms.openlocfilehash: 14ae990999247b90f16b10115dea3408b965a04a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785647"
---
# <a name="destroyiceefilegen-function"></a>Função DestroyICeeFileGen

Destrói um objeto [ICeeFileGen](iceefilegen-class.md) .  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DestroyICeeFileGen (  
    [in] ICeeFileGen  **ceeFileGen  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ceeFileGen`  
 no O `ICeeFileGen` objeto a ser destruído.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna códigos de erro COM padrão.  
  
## <a name="remarks"></a>Comentários  

 `DestroyICeeFileGen` destrói o `ICeeFileGen` objeto criado pela função [CreateICeeFileGen](createiceefilegen-function.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ICeeFileGen. h  
  
 **Biblioteca:** MSCorPE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
