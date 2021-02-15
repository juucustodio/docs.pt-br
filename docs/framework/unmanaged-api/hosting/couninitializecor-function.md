---
description: 'Saiba mais sobre: função CoUninitializeCor'
title: Função CoUninitializeCor
ms.date: 03/30/2017
api_name:
- CoUninitializeCor
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoUninitializeCor
helpviewer_keywords:
- CoUninitializeCor function [.NET Framework hosting]
ms.assetid: 50a95b8b-9766-470e-bb29-2c7ecddfd4a1
topic_type:
- apiref
ms.openlocfilehash: 1aa3482b6891779b4c85c29079ccd26d7170934e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746198"
---
# <a name="couninitializecor-function"></a>Função CoUninitializeCor

`CoUninitializeCor` é obsoleto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
STDAPI_(void) CoUninitializeCor(void);  
```  
  
## <a name="remarks"></a>Comentários  

 O Common Language Runtime não pode ser descarregado de um processo. Para remover completamente o tempo de execução de um processo em execução, você deve desligar esse processo.  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
