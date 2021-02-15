---
description: 'Saiba mais sobre o método: IMetaDataImport:: EnumMemberRefs'
title: Método IMetaDataImport::EnumMemberRefs
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMemberRefs
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMemberRefs
helpviewer_keywords:
- EnumMemberRefs method [.NET Framework metadata]
- IMetaDataImport::EnumMemberRefs method [.NET Framework metadata]
ms.assetid: e97c97a6-6e4f-41f5-9af1-9b3cf3bdbd6b
topic_type:
- apiref
ms.openlocfilehash: 0c9b10342f73ae5b604ac25b6ff8ccec58deb5ab
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99670938"
---
# <a name="imetadataimportenummemberrefs-method"></a>Método IMetaDataImport::EnumMemberRefs

Enumera os tokens de MemberRef que representam os membros do tipo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumMemberRefs (  
   [in, out] HCORENUM    *phEnum,
   [in]   mdToken        tkParent,
   [out]  mdMemberRef    rMemberRefs[],
   [in]   ULONG          cMax,
   [out]  ULONG          *pcTokens  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phEnum`  
 [entrada, saída] Um ponteiro para o enumerador.  
  
 `tkParent`  
 no Um token de TypeDef, TypeRef, MethodDef ou ModuleRef para o tipo cujos membros devem ser enumerados.  
  
 `rMemberRefs`  
 fora A matriz usada para armazenar tokens de MemberRef.  
  
 `cMax`  
 no O tamanho máximo da `rMemberRefs` matriz.  
  
 `pcTokens`  
 fora O número real de tokens de MemberRef retornado em `rMemberRefs` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumMemberRefs` retornado com êxito.|  
|`S_FALSE`|Não há tokens de MemberRef para enumerar. Nesse caso, `pcTokens` é zero.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
