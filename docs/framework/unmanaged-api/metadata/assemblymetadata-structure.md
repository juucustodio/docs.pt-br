---
description: 'Saiba mais sobre: estrutura ASSEMBLYMETADATA'
title: Estrutura ASSEMBLYMETADATA
ms.date: 03/30/2017
api_name:
- ASSEMBLYMETADATA
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ASSEMBLYMETADATA
helpviewer_keywords:
- ASSEMBLYMETADATA structure [.NET Framework metadata]
ms.assetid: 1af98e57-9145-4d35-bb78-77d1da7c91a5
topic_type:
- apiref
ms.openlocfilehash: 6fc9c03bea3b1413cd3a8421746137e37d43bd90
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678920"
---
# <a name="assemblymetadata-structure"></a>Estrutura ASSEMBLYMETADATA

Contém informações sobre o assembly referenciado, incluindo sua versão e seu nível de suporte para localidades, processadores e sistemas operacionais.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct {  
    USHORT  usMajorVersion;  
    USHORT  usMinorVersion;  
    USHORT  usBuildNumber;  
    USHORT  usRevisionNumber;  
    LPWSTR  szLocale;  
    ULONG   cbLocale;  
    DWORD*  rdwProcessor[];  
    ULONG   ulProcessor  
    OSINFO* rOS[];  
    ULONG   ulOS;  
} ASSEMBLYMETADATA;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`usMajorVersion`|O número de versão principal do assembly referenciado. Esse valor não pode ser zero. Se todos os bits de `usMajorVersion` estiverem definidos, a versão principal não será especificada.|  
|`usMinorVersion`|O número de versão secundária do assembly referenciado. Esse valor não pode ser zero. Se todos os bits de `usMinorVersion` estiverem definidos, a versão secundária não será especificada.|  
|`usBuildNumber`|O número de Build do assembly referenciado. Esse valor não pode ser zero. Se todos os bits de `usBuildNumber` estiverem definidos, o número de Build não será especificado.|  
|`usRevisionNumber`|O número de revisão do assembly referenciado. Esse valor não pode ser zero. Se todos os bits de `usRevisionNumber` estiverem definidos, o número de revisão não será especificado.|  
|`szLocale`|Uma lista de nomes de localidade que estão em conformidade com a especificação RFC1766, separados por ponto e vírgula, especificando as localidades com suporte no assembly referenciado. Um valor nulo indica independência de localidade. **Observação:**  No .NET Framework versão 1,0, você não pode especificar mais de uma localidade.|  
|`cbLocale`|O tamanho em caracteres largos de `szLocale` .|  
|`rdwProcessor`|Uma matriz de identificadores, conforme definido em Winnt. h, para os tipos de processador que são suportados pelo assembly referenciado. Um valor nulo indica independência do processador.|  
|`ulProcessor`|O comprimento da matriz `rdwProcessor`.|  
|`rOS`|Uma matriz de instâncias de [OSInfo](osinfo-structure.md) que especificam os sistemas operacionais com suporte no assembly referenciado. Um valor nulo indica a independência do sistema operacional.|  
|`ulOS`|O comprimento da matriz `rOS`.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de metadados](metadata-structures.md)
- [Interface IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)
- [Estrutura OSINFO](osinfo-structure.md)
