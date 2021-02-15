---
description: 'Saiba mais sobre: enumeração de AssemblyOptions'
title: Enumeração AssemblyOptions
ms.date: 03/30/2017
api_name:
- AssemblyOptions
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AssemblyOptions
helpviewer_keywords:
- Alink API, AssemblyOptions enumeration
- AssemblyOptions enumeration
ms.assetid: 84f83921-64cb-49e3-ac8b-22a0b77b18a8
topic_type:
- apiref
ms.openlocfilehash: aba9ecb3176f533e2d53e2e45fef3d1dc4e55077
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638412"
---
# <a name="assemblyoptions-enumeration"></a>Enumeração AssemblyOptions

Enumera as opções de assembly.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef enum _AssemblyOptions {  
    optAssemTitle = 0,  
    optAssemDescription,  
    optAssemConfig,  
    optAssemOS,  
    optAssemProcessor,  
    optAssemLocale,  
    optAssemVersion,  
    optAssemCompany,  
    optAssemProduct,  
    optAssemProductVersion,  
    optAssemCopyright,  
    optAssemTrademark,  
    optAssemKeyFile,  
    optAssemKeyName,  
    optAssemAlgID,  
    optAssemFlags,  
    optAssemHalfSign,  
    optAssemFileVersion,  
    optAssemSatelliteVer,  
    optLastAssemOption  
}   AssemblyOptions;  
```  
  
## <a name="fields"></a>Campos  
  
|Campo|Descrição|  
|-----------|-----------------|  
|optAssemTitle|String – representa o título do assembly.|  
|optAssemDescription|String-contém a descrição do assembly.|  
|optAssemConfig|String-contém a configuração do assembly.|  
|optAssemOS|Codificada em cadeia de caracteres como: "dwOSPlatformId. dwOSMajorVersion. dwOSMinorVersion".|  
|optAssemProcessor|ULONG|  
|optAssemLocale|Cadeia de caracteres – contém a localidade do assembly.|  
|optAssemVersion|Cadeia de caracteres codificada como: "Major. Minor. Build. Revision".|  
|optAssemCompany|Cadeia de caracteres – contém a empresa.|  
|optAssemProduct|Cadeia de caracteres-contém o nome do produto.|  
|optAssemProductVersion|Cadeia de caracteres (também conhecida como InformationalVersion).|  
|optAssemCopyright|Cadeia de caracteres-contém as informações de direitos autorais.|  
|optAssemTrademark|Cadeia de caracteres-contém as informações de marca registrada.|  
|optAssemKeyFile|Cadeia de caracteres (nome do arquivo).|  
|optAssemKeyName|Cadeia de caracteres (o nome da chave).|  
|optAssemAlgID|ULONG|  
|optAssemFlags|ULONG|  
|optAssemHalfSign|Bool (também conhecido como DelaySign).|  
|optAssemFileVersion|Cadeia de caracteres codificada como "principal. secundária. Build. Revision" – igual a ProductVersion.|  
|optAssemSatelliteVer|Cadeia de caracteres codificada como "principal. secundária. Build. Revision".|  
|optLastAssemOption|Um contador do número de elementos.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** ALink. h  
  
 **Biblioteca**: alink.dll  
  
## <a name="see-also"></a>Consulte também

- [Al.exe (vinculador de assembly)](../../tools/al-exe-assembly-linker.md)
