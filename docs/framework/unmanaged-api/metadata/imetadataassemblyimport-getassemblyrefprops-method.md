---
description: 'Saiba mais sobre o método: IMetaDataAssemblyImport:: GetAssemblyRefProps'
title: Método IMetaDataAssemblyImport::GetAssemblyRefProps
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetAssemblyRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps
helpviewer_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps method [.NET Framework metadata]
- GetAssemblyRefProps method [.NET Framework metadata]
ms.assetid: 5c6b7fb4-cbca-4479-b650-ab9a99732ea0
topic_type:
- apiref
ms.openlocfilehash: f7011806920ba37ca84b1a48f12da3a5557fa464
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784126"
---
# <a name="imetadataassemblyimportgetassemblyrefprops-method"></a>Método IMetaDataAssemblyImport::GetAssemblyRefProps

Obtém o conjunto de propriedades para a referência de assembly com a assinatura de metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetAssemblyRefProps (  
    [in]  mdAssemblyRef        mdar,
    [out] const void          **ppbPublicKeyOrToken,
    [out] ULONG                *pcbPublicKeyOrToken,
    [out] LPWSTR               szName,
    [in]  ULONG                cchName,
    [out] ULONG                *pchName,
    [out] ASSEMBLYMETADATA     *pMetaData,
    [out] const void           **ppbHashValue,
    [out] ULONG                *pcbHashValue,
    [out] DWORD                *pdwAssemblyRefFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `mdar`  
 no O `mdAssemblyRef` token de metadados que representa a referência de assembly para a qual obter as propriedades.  
  
 `ppbPublicKeyOrToken`  
 fora Um ponteiro para a chave pública ou o token de metadados.  
  
 `pcbPublicKeyOrToken`  
 fora O número de bytes na chave pública ou no token retornado.  
  
 `szName`  
 fora O nome simples do assembly.  
  
 `cchName`  
 no O tamanho, em caracteres largos, de `szName` .  
  
 `pchName`  
 fora Um ponteiro para o número de caracteres largos realmente retornados em `szName` .  
  
 `pMetaData`  
 fora Um ponteiro para uma estrutura ASSEMBLYMETADATA que contém os metadados do assembly.  
  
 `ppbHashValue`  
 fora Um ponteiro para o valor de hash. Esse é o hash, usando o algoritmo SHA-1, da `PublicKey` Propriedade do assembly que está sendo referenciado, a menos que o sinalizador arfFullOriginator da enumeração [AssemblyRefFlags](assemblyrefflags-enumeration.md) seja definido.  
  
 `pcbHashValue`  
 fora O número de caracteres largos no valor de hash retornado.  
  
 `pdwAssemblyRefFlags`  
 fora Um ponteiro para sinalizadores que descrevem os metadados aplicados a um assembly. O valor de flags é uma combinação de um ou mais valores de [CorAssemblyFlags](corassemblyflags-enumeration.md) .  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retornará S_OK se tiver sucesso; caso contrário, ele retorna um dos códigos de erro definidos no arquivo de cabeçalho Winerror. h.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataAssemblyImport](imetadataassemblyimport-interface.md)
