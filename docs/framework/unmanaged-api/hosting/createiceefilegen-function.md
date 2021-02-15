---
description: 'Saiba mais sobre: função CreateICeeFileGen'
title: Função CreateICeeFileGen
ms.date: 03/30/2017
api_name:
- CreateICeeFileGen
api_location:
- mscoree.dll
- mscorpehost.dll
- mscorpe.dll
api_type:
- COM
f1_keywords:
- CreateICeeFileGen
helpviewer_keywords:
- CreateICeeFileGen function [.NET Framework hosting]
ms.assetid: e36e1fd8-8456-4359-bdc3-3ec1765f041f
topic_type:
- apiref
ms.openlocfilehash: 10aefaad4dd1173e4ef55f727371bab508e2d40c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716920"
---
# <a name="createiceefilegen-function"></a>Função CreateICeeFileGen

Cria um objeto [ICeeFileGen](iceefilegen-class.md) .  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateICeeFileGen (  
    [out] ICeeFileGen  **ceeFileGen  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ceeFileGen`  
 fora Um ponteiro para o endereço de um novo `ICeeFileGen` objeto.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna códigos de erro COM padrão.  
  
## <a name="remarks"></a>Comentários  

 O `ICeeFileGen` objeto é usado para criar Common Language Runtime (CLR) arquivos executáveis portáteis (PE).  
  
 Chame a função [DestroyICeeFileGen](destroyiceefilegen-function.md) para destruir o `ICeeFileGen` objeto quando terminar.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ICeeFileGen. h  
  
 **Biblioteca:** MSCorPE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
