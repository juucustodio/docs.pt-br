---
description: 'Saiba mais sobre: função CorMarkThreadInThreadPool'
title: Função CorMarkThreadInThreadPool
ms.date: 03/30/2017
api_name:
- CorMarkThreadInThreadPool
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CorMarkThreadInThreadPool
helpviewer_keywords:
- CorMarkThreadInThreadPool function [.NET Framework hosting]
ms.assetid: 3f958d41-e82e-4ec3-ae6f-16c7b3b31e3e
topic_type:
- apiref
ms.openlocfilehash: 68d945870075f2f8c06fe76b7a71e2f806078694
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716925"
---
# <a name="cormarkthreadinthreadpool-function"></a>Função CorMarkThreadInThreadPool

Marca o thread do pool de threads em execução no momento para a execução do código gerenciado. A partir do .NET Framework versão 2,0, essa função não tem nenhum efeito. Ela não é necessária e pode ser removida do seu código. Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
void CorMarkThreadInThreadPool ();  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
