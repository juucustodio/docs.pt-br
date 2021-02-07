---
description: 'Saiba mais sobre o método: IAssemblyName:: GetDisplayName'
title: Método IAssemblyName::GetDisplayName
ms.date: 03/30/2017
api_name:
- IAssemblyName.GetDisplayName
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyName::GetDisplayName
helpviewer_keywords:
- GetDisplayName method, IAssemblyName interface [.NET Framework fusion]
- IAssemblyName::GetDisplayName method [.NET Framework fusion]
ms.assetid: 9a26547a-9a34-4284-a463-78a7d4b496cf
topic_type:
- apiref
ms.openlocfilehash: 9b52a901385fa9b3ba7cb6bcd1678d0718f8f695
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760752"
---
# <a name="iassemblynamegetdisplayname-method"></a>Método IAssemblyName::GetDisplayName

Obtém o nome legível do assembly referenciado por este objeto [IAssemblyName](iassemblyname-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDisplayName (  
        [out]      LPOLESTR  szDisplayName,  
        [in, out]  LPDWORD   pccDisplayName,  
        [in]       DWORD     dwDisplayFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szDisplayName`  
 fora O buffer de cadeia de caracteres que contém o nome do assembly referenciado.  
  
 `pccDisplayName`  
 [entrada, saída] O tamanho de `szDisplayName` , em caracteres largos, incluindo um caractere de terminador nulo.  
  
 `dwDisplayFlags`  
 no Uma combinação de bits de [ASM_DISPLAY_FLAGS](asm-display-flags-enumeration.md) de valores que influencia os recursos do `szDisplayName` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IAssemblyName](iassemblyname-interface.md)
- [Enumerações Fusion](fusion-enumerations.md)
