---
description: 'Saiba mais sobre: função CreateALink'
title: Função CreateALink
ms.date: 03/30/2017
api_name:
- CreateALink
api_location:
- alink.dll
api_type:
- DLLExport
f1_keywords:
- CreateALink
helpviewer_keywords:
- CreateALink function
- Alink API, CreateALink function
ms.assetid: fc73bcb9-6af6-44d8-bc39-2f4400325dae
topic_type:
- apiref
ms.openlocfilehash: cf34ae8d38a8339f539c770df8f5dd14e4a3e4b4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638360"
---
# <a name="createalink-function"></a>Função CreateALink

Cria uma instância do vinculador de assembly e define um ponteiro para a interface especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateALink (  
   REFIID riid,  
   IUnknown **ppInterface  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`riid`|O nome físico de uma das interfaces do vinculador de assembly.|  
|`ppInterface`|O local em que a conclusão bem-sucedida contém um ponteiro para a `riid` interface.|  
  
## <a name="requirements"></a>Requisitos  

 **Biblioteca**: alink.dll  
  
## <a name="see-also"></a>Consulte também

- [Al.exe (vinculador de assembly)](../../tools/al-exe-assembly-linker.md)
