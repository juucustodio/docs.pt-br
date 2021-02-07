---
description: 'Saiba mais sobre: função CoUninitializeEE'
title: Função CoUninitializeEE
ms.date: 03/30/2017
api_name:
- CoUninitializeEE
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoUninitializeEE
helpviewer_keywords:
- CoUninitializeEE function [.NET Framework hosting]
ms.assetid: 5f5a311a-839a-465f-89d9-ff1c74da9736
topic_type:
- apiref
ms.openlocfilehash: e356135ea027bd52520eff9084ad2f7f09e1fe0b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746159"
---
# <a name="couninitializeee-function"></a>Função CoUninitializeEE

`CoUninitializeEE` é obsoleto e não fornece nenhuma funcionalidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
void CoUninitializeEE (  
    BOOL fFlags  
);  
```  
  
## <a name="remarks"></a>Comentários  

 O mecanismo de execução de Common Language Runtime não pode ser descarregado de um processo. Para desligar a chamada do mecanismo de execução [CorExitProcess](corexitprocess-function.md).  
  
## <a name="see-also"></a>Consulte também

- [Função CoInitializeEE](coinitializeee-function.md)
- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
