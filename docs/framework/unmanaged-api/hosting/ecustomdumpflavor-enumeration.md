---
description: 'Saiba mais sobre: Enumeração ECustomDumpFlavor'
title: Enumeração ECustomDumpFlavor
ms.date: 03/30/2017
api_name:
- ECustomDumpFlavor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ECustomDumpFlavor
helpviewer_keywords:
- ECustomDumpFlavor enumeration [.NET Framework hosting]
ms.assetid: b39b3320-fac7-41f1-9a03-ab6fb0cd89c7
topic_type:
- apiref
ms.openlocfilehash: 3ef118368fc827472bdaacb0b03d8c2011275056
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785517"
---
# <a name="ecustomdumpflavor-enumeration"></a>Enumeração ECustomDumpFlavor

Contém valores que indicam quais itens incluir em um subconjunto personalizado de um despejo de heap ao relatar erros.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    DUMP_FLAVOR_Mini            = 1,  
    DUMP_FLAVOR_NonHeapCLRState = 2  
} ECustomDumpFlavor;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`DUMP_FLAVOR_Mini`|Especifica que o despejo de heap personalizado deve iniciar como um minidespejo e incluir dados adicionais especificados por quaisquer instâncias de [CustomDumpItem](customdumpitem-structure.md) passadas para o mesmo método.|  
|`DUMP_FLAVOR_NonHeapCLRState`|Especifica que o despejo de heap personalizado deve coletar todos os dados de estado de tempo de execução que não foram alocados dinamicamente.|  
  
## <a name="remarks"></a>Comentários  

 Um parâmetro do tipo `ECustomDumpFlavor` é passado para o método [ICLRErrorReportingManager:: BeginCustomDump](iclrerrorreportingmanager-begincustomdump-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração ECustomDumpItemKind](ecustomdumpitemkind-enumeration.md)
- [Interface ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
