---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetNativeCallConvFromSig'
title: Método IMetaDataImport::GetNativeCallConvFromSig
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetNativeCallConvFromSig
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetNativeCallConvFromSig
helpviewer_keywords:
- GetNativeCallConvFromSig method [.NET Framework metadata]
- IMetaDataImport::GetNativeCallConvFromSig method [.NET Framework metadata]
ms.assetid: 50e04026-4d4a-47d9-96c1-f4677d6d938b
topic_type:
- apiref
ms.openlocfilehash: 2fb5c347098f860f9ad32eab20c8b5bd6278f838
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99677566"
---
# <a name="imetadataimportgetnativecallconvfromsig-method"></a>Método IMetaDataImport::GetNativeCallConvFromSig

Obtém a Convenção de chamada nativa para o método representado pelo ponteiro de assinatura especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNativeCallConvFromSig (  
   [in]  void const  *pvSig,  
   [in]  ULONG       cbSig,  
   [out] ULONG       *pCallConv  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pvSig`  
 no Um ponteiro para a assinatura de metadados do método para o qual retornar a Convenção de chamada.  
  
 `cbSig`  
 no O tamanho em bytes de `pvSig` .  
  
 `pCallConv`  
 fora Um ponteiro para a Convenção de chamada nativa.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.InteropServices.CallingConvention>
- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
