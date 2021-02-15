---
description: 'Saiba mais sobre: CeeSectionRelocExtra Union'
title: CeeSectionRelocExtra União
ms.date: 03/30/2017
api_name:
- CeeSectionRelocExtra Union
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CeeSectionRelocExtra
helpviewer_keywords:
- CeeSectionRelocExtra union [.NET Framework metadata]
ms.assetid: d9568cf6-7f98-4cd6-ab36-0a2bd509afcc
topic_type:
- apiref
ms.openlocfilehash: 40001c1a0772e24633f4232da8e7817f3747f8ea
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678842"
---
# <a name="ceesectionrelocextra-union"></a>CeeSectionRelocExtra União

Representa um deslocamento de endereço que é usado pela interface [ICeeGen](iceegen-interface.md) para realocar uma seção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef union  {  
    USHORT highAdj;  
} CeeSectionRelocExtra;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`highAdj`|O ajuste de endereço superior para a seção.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Uniões de metadados](metadata-unions.md)
