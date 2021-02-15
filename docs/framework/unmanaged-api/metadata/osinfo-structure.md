---
description: 'Saiba mais sobre: estrutura OSINFO'
title: Estrutura OSINFO
ms.date: 03/30/2017
api_name:
- OSINFO
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- OSINFO
helpviewer_keywords:
- OSINFO structure [.NET Framework metadata]
ms.assetid: fac7b480-7adb-4450-a5e9-690fed81ffae
topic_type:
- apiref
ms.openlocfilehash: 5027ef5cf4137aa1e781134b325407e1251fdd31
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799090"
---
# <a name="osinfo-structure"></a>Estrutura OSINFO

Contém detalhes sobre o sistema operacional de um assembly ou módulo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct {  
    DWORD   dwOSPlatformId;  
    DWORD   dwOSMajorVersion;
    DWORD   dwOSMinorVersion;
} OSINFO;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`dwOSPlatformId`|Um dos valores de identificador definidos pela função da plataforma Microsoft Windows `GetVersionEx` . Os seguintes valores têm suporte:<br /><br /> -VER_PLATFORM_WIN32s, ou 0x0000, para especificar o Microsoft Windows 3,1.<br />-VER_PLATFORM_WIN32_WINDOWS, ou 0x0001, para especificar o Windows 95, o Windows 98 ou os sistemas operacionais decrescentes deles.<br />-VER_PLATFORM_WIN32_NT, ou 0x0002, para especificar o Windows NT ou os sistemas operacionais que descendem dele.|  
|`dwOSMajorVersion`|A versão principal do sistema operacional ou um valor nulo para indicar qualquer versão.|  
|`dwOSMinorVersion`|A versão secundária do sistema operacional ou um valor nulo para indicar qualquer versão.|  
  
## <a name="remarks"></a>Comentários  

 `OSINFO` baseia-se na `OSVERSIONINFOEX` estrutura usada em chamadas para a função da plataforma Microsoft Windows `GetVersionEx` . Essa estrutura é usada pela estrutura ASSEMBLYMETADATA para indicar o suporte do sistema operacional.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de metadados](metadata-structures.md)
- [Interface IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)
