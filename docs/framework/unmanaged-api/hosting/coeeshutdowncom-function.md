---
description: 'Saiba mais sobre: função CoEEShutDownCOM'
title: Função CoEEShutDownCOM
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
ms.openlocfilehash: 4f1ac8107c9a121ebf52ef21a5f2c9006880914f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799857"
---
# <a name="coeeshutdowncom-function"></a>Função CoEEShutDownCOM

Força o Common Language Runtime (CLR) a liberar todos os ponteiros de interface que ele mantém dentro de RCW (Runtime Callable Wrappers). Isso tem o efeito de liberar todos os caches de RCW. Essa função global foi preterida no .NET Framework 4. Em vez disso, use o ponto de entrada para um tempo de execução específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a>Comentários  

 A `CoEEShutDownCOM` função primeiro libera todos os RCWs em todos os contextos e em todos os caches e, em seguida, remove qualquer notificação de subdivisão existente na instalação. Nenhum descarregamento de DLL ocorre.  
  
> [!CAUTION]
> Essa função afeta todos os tempos de execução que são carregados no processo.  
  
 Começando com o .NET Framework 4, chame o ponto de entrada para essa função no tempo de execução específico que você deseja afetar. Para obter o ponto de entrada, chame o método [ICLRRuntimeInfo:: GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) e especifique "CoEEShutDownCOM".  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
