---
description: 'Saiba mais sobre: função CoInitialize'
title: Função CoInitializeEE
ms.date: 03/30/2017
api_name:
- CoInitializeEE
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoInitializeEE
helpviewer_keywords:
- CoInitializeEE function [.NET Framework hosting]
ms.assetid: 7e42a928-5068-4ba6-b8c3-806551a01fa8
topic_type:
- apiref
ms.openlocfilehash: 9664324c569ed4de73262491cf8eda8296b3c3a1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799818"
---
# <a name="coinitializeee-function"></a>Função CoInitializeEE

Garante que o mecanismo de execução de Common Language Runtime seja carregado em um processo. Essa função foi preterida no .NET Framework 4. Em vez disso, use o método [ICLRRuntimeHost:: Start](iclrruntimehost-start-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CoInitializeEE (  
   [in] DWORD fFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fFlags`  
 no Uma das constantes de enumeração [COINITIEE](../metadata/coinitiee-enumeration.md) .  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna códigos de erro COM padrão, conforme definido em Winerror. h, e os valores na tabela a seguir.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|S_OK|O mecanismo de execução foi carregado com êxito.|  
|S_FALSE|O mecanismo de execução já está carregado.|  
|E_FAIL|Não foi possível carregar o mecanismo de execução.|  
  
## <a name="remarks"></a>Comentários  

 Esse método carregará o mecanismo de execução se ele não tiver sido carregado anteriormente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
