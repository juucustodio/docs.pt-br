---
description: 'Saiba mais sobre: estrutura de FUSION_INSTALL_REFERENCE'
title: Estrutura FUSION_INSTALL_REFERENCE
ms.date: 03/30/2017
api_name:
- FUSION_INSTALL_REFERENCE
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- FUSION_INSTALL_REFERENCE
helpviewer_keywords:
- FUSION_INSTALL_REFERENCE structure [.NET Framework fusion]
ms.assetid: ae181ec8-36bf-4ed1-9a02-ca27d417c80b
topic_type:
- apiref
ms.openlocfilehash: 4ac3d2f7d36dd017315a8a3ce6d6185e75f9ddc6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761103"
---
# <a name="fusion_install_reference-structure"></a>Estrutura FUSION_INSTALL_REFERENCE

Representa uma referência que um aplicativo faz para um assembly que o aplicativo instalou no cache de assembly global.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _FUSION_INSTALL_REFERENCE_ {  
    DWORD    cbSize,  
    DWORD    dwFlags,  
    GUID     guidScheme,  
    LPCWSTR  szIdentifier,  
    LPCWSTR  szNonCanonicalData  
} FUSION_INSTALL_REFERENCE, *LPFUSION_INSTALL_REFERENCE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`cbSize`|O tamanho da estrutura em bytes.|  
|`dwFlags`|Reservado para extensibilidade futura. Esse valor deve ser 0 (zero).|  
|`guidScheme`|A entidade que adiciona a referência. Esse campo pode ter um dos seguintes valores:<br /><br /> -FUSION_REFCOUNT_MSI_GUID: o assembly é referenciado por um aplicativo que foi instalado usando o Microsoft Windows Installer. O `szIdentifier` campo é definido como `MSI` e o `szNonCanonicalData` campo é definido como `Windows Installer` . Esse esquema é usado para assemblies lado a lado do Windows.<br />-FUSION_REFCOUNT_UNINSTALL_SUBKEY_GUID: o assembly é referenciado por um aplicativo que aparece na interface **Adicionar/remover programas** . O `szIdentifier` campo fornece o token que registra o aplicativo com a interface **Adicionar/remover programas** .<br />-FUSION_REFCOUNT_FILEPATH_GUID: o assembly é referenciado por um aplicativo que é representado por um arquivo no sistema de arquivos. O `szIdentifier` campo fornece o caminho para esse arquivo.<br />-FUSION_REFCOUNT_OPAQUE_STRING_GUID: o assembly é referenciado por um aplicativo que é representado somente por uma cadeia de caracteres opaca. O `szIdentifier` campo fornece essa cadeia de caracteres opaca. O cache de assembly global não verifica a existência de referências opacas quando você remove esse valor.<br />-FUSION_REFCOUNT_OSINSTALL_GUID: esse valor é reservado.|  
|`szIdentifier`|Uma cadeia de caracteres exclusiva que identifica o aplicativo que instalou o assembly no cache de assembly global. Seu valor depende do valor do `guidScheme` campo.|  
|`szNonCanonicalData`|Uma cadeia de caracteres que é compreendida somente pela entidade que adiciona a referência. O cache de assembly global armazena essa cadeia de caracteres, mas não a usa.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de fusão](fusion-structures.md)
- [Cache de assemblies global](../../app-domains/gac.md)
