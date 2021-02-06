---
description: 'Saiba mais sobre: Função GetALinkMessageDll'
title: Função GetALinkMessageDll
ms.date: 03/30/2017
api_name:
- GetALinkMessageDll
api_location:
- alink.dll
api_type:
- DLLExport
f1_keywords:
- GetALinkMessageDll
helpviewer_keywords:
- Alink API, GetALinkMessageDll function
- GetALinkMessageDll function
ms.assetid: 67985a22-88a2-4c54-8d99-4bcde9d6213e
topic_type:
- apiref
ms.openlocfilehash: 67a294d1f21f50cee938ddeb14d1f30b4ccf911b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637866"
---
# <a name="getalinkmessagedll-function"></a>Função GetALinkMessageDll

Localiza e carrega a DLL de mensagem. Retornará 0 se a DLL de mensagem não puder ser localizada ou carregada. A DLL de mensagem deve estar em um subdiretório cujo nome é uma ID de idioma ou no diretório atual.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HINSTANCE WINAPI GetALinkMessageDll();  
```  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** ALink. h  
  
 **Biblioteca**: alink.dll  
  
## <a name="see-also"></a>Consulte também

- [Al.exe (vinculador de assembly)](../../tools/al-exe-assembly-linker.md)
