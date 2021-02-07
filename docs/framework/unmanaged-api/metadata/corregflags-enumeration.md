---
description: 'Saiba mais sobre: Enumeração CorRegFlags'
title: Enumeração CorRegFlags
ms.date: 03/30/2017
api_name:
- CorRegFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorRegFlags
helpviewer_keywords:
- CorRegFlags enumeration [.NET Framework metadata]
ms.assetid: 8d3080ee-39fe-4c57-8950-51323632d045
topic_type:
- apiref
ms.openlocfilehash: 534b7b4b170d1f586e967807c4cc8a9c82648e8b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753647"
---
# <a name="corregflags-enumeration"></a>Enumeração CorRegFlags

Fornece valores de sinalizador usados para registro ao instalar um módulo ou uma imagem composta.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum
{  
    regNoCopy  = 0x00000001,  
    regConfig  = 0x00000002,  
    regHasRefs = 0x00000004  
} CorRegFlags;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`regNoCopy`|Especifica que os arquivos não devem ser copiados para o destino.|  
|`regConfig`|Especifica que o módulo ou composto é uma configuração.|  
|`regHasRefs`|Especifica que o módulo ou composto tem referências de classe.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
