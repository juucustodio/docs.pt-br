---
description: 'Saiba mais sobre: método ICorRuntimeHost:: GetConfiguration'
title: Método ICorRuntimeHost::GetConfiguration
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.GetConfiguration
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::GetConfiguration
helpviewer_keywords:
- ICorRuntimeHost::GetConfiguration method [.NET Framework hosting]
- GetConfiguration method [.NET Framework hosting]
ms.assetid: c431617a-b055-44a0-8730-48b7a86d9610
topic_type:
- apiref
ms.openlocfilehash: d3e3f065c3957fb29daa11ed7c46858a53865c91
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784828"
---
# <a name="icorruntimehostgetconfiguration-method"></a>Método ICorRuntimeHost::GetConfiguration

Obtém um objeto que permite ao host especificar a configuração de retorno de chamada do Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetConfiguration(  
    [out] ICorConfiguration** pConfiguration  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pConfiguration`  
 fora Um ponteiro para o endereço de um objeto [ICorConfiguration](icorconfiguration-interface.md) que pode ser usado para configurar o CLR.  
  
## <a name="remarks"></a>Comentários  

 O CLR deve ser configurado antes de sua inicialização; caso contrário, o `GetConfiguration` método retornará um HRESULT indicando um erro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **Versões do .NET Framework:** 1,0, 1,1  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorRuntimeHost](icorruntimehost-interface.md)
