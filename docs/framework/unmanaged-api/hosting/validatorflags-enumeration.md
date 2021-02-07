---
description: 'Saiba mais sobre: Enumeração ValidatorFlags'
title: Enumeração ValidatorFlags
ms.date: 03/30/2017
api_name:
- ValidatorFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ValidatorFlags
helpviewer_keywords:
- ValidatorFlags enumeration [.NET Framework hosting]
ms.assetid: a3f5c266-3fcc-4ad1-aaf5-4cdbe26304ad
topic_type:
- apiref
ms.openlocfilehash: 473b0eef2851126256e1ea6b6d2b82be32e03e1c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99679115"
---
# <a name="validatorflags-enumeration"></a>Enumeração ValidatorFlags

Contém valores que indicam o tipo de validação que deve ser executado em uma chamada para o método [ICLRValidator:: Validate](iclrvalidator-validate-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum ValidatorFlags {  
    VALIDATOR_EXTRA_VERBOSE =       0x00000001,  
    VALIDATOR_SHOW_SOURCE_LINES =   0x00000002,  
    VALIDATOR_CHECK_ILONLY =        0x00000004,  
    VALIDATOR_CHECK_PEFORMAT_ONLY = 0x00000008,  
    VALIDATOR_NOCHECK_PEFORMAT =    0x00000010,  
};  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`VALIDATOR_CHECK_ILONLY`|Especifica que somente a MSIL (Microsoft Intermediate Language) no arquivo executável deve ser validada.|  
|`VALIDATOR_CHECK_PEFORMAT_ONLY`|Especifica que somente o formato do arquivo executável deve ser validado.|  
|`VALIDATOR_EXTRA_VERBOSE`|Especifica que todos os tipos de validação devem ser executados e relatados em.|  
|`VALIDATOR_NOCHECK_PEFORMAT`|Especifica que o formato do arquivo executável não deve ser validado.|  
|`VALIDATOR_SHOW_SOURCE_LINES`|Especifica que as mensagens de erro de validação devem incluir as linhas do código-fonte que geram erros de validação. Esse valor de campo não é válido na versão .NET Framework 2,0.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** IValidator. idl, IValidator. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
