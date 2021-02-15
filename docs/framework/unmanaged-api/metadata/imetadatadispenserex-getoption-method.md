---
description: 'Saiba mais sobre o método: IMetaDataDispenserEx:: GetOption'
title: Método IMetaDataDispenserEx::GetOption
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.GetOption
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::GetOption
helpviewer_keywords:
- GetOption method [.NET Framework metadata]
- IMetaDataDispenserEx::GetOption method [.NET Framework metadata]
ms.assetid: d7f794e5-8e25-4d65-850a-7c34fbfce87d
topic_type:
- apiref
ms.openlocfilehash: cf52a251c3c0e0485558a150b727d58eeae81995
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753543"
---
# <a name="imetadatadispenserexgetoption-method"></a>Método IMetaDataDispenserEx::GetOption

Obtém o valor da opção especificada para o escopo de metadados atual. A opção controla como as chamadas para o escopo de metadados atual são tratadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetOption (  
    [in]  REFGUID         optionId,
    [out] const VARIANT   *pValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `optionId`  
 no Um ponteiro para um GUID que especifica a opção a ser recuperada. Consulte a seção comentários para obter uma lista de GUIDs com suporte.  
  
 `pValue`  
 fora O valor da opção retornada. O tipo desse valor será uma variante do tipo da opção especificada.  
  
## <a name="remarks"></a>Comentários  

 A lista a seguir mostra os GUIDs que têm suporte para esse método. Para obter descrições, consulte o método [IMetaDataDispenserEx:: SetOption](imetadatadispenserex-setoption-method.md) . Se `optionId` não estiver nessa lista, esse método retornará HRESULT `E_INVALIDARG` , indicando um parâmetro incorreto.  
  
- MetaDataCheckDuplicatesFor  
  
- MetaDataRefToDefCheck  
  
- MetaDataNotificationForTokenMovement  
  
- MetaDataSetENC  
  
- MetaDataErrorIfEmitOutOfOrder  
  
- MetaDataGenerateTCEAdapters  
  
- MetaDataLinkerOptions  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataDispenserEx](imetadatadispenserex-interface.md)
- [Interface IMetaDataDispenser](imetadatadispenser-interface.md)
