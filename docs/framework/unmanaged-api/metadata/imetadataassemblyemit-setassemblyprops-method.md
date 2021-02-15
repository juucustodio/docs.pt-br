---
description: 'Saiba mais sobre o método: IMetaDataAssemblyEmit:: SetAssemblyProps'
title: Método IMetaDataAssemblyEmit::SetAssemblyProps
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.SetAssemblyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::SetAssemblyProps
helpviewer_keywords:
- SetAssemblyProps method [.NET Framework metadata]
- IMetaDataAssemblyEmit::SetAssemblyProps method [.NET Framework metadata]
ms.assetid: 91b633d7-9e75-43c3-a8d2-2144984e5f9e
topic_type:
- apiref
ms.openlocfilehash: d5dfb5fa472bb83863c8e4909998deeb2b9fc53b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678179"
---
# <a name="imetadataassemblyemitsetassemblyprops-method"></a>Método IMetaDataAssemblyEmit::SetAssemblyProps

Modifica a estrutura de `Assembly` metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetAssemblyProps (  
    [in] mdAssembly               pma,  
    [in] const void               *pbPublicKey,  
    [in] ULONG                    cbPublicKey,  
    [in] ULONG                    ulHashAlgId,  
    [in] LPCWSTR                  szName,  
    [in] const ASSEMBLYMETADATA   *pMetaData,  
    [in] DWORD                    dwAssemblyFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pma`  
 no O token de metadados que especifica a `Assembly` estrutura de metadados a ser modificada.  
  
 `pbPublicKey`  
 no Um ponteiro para a chave pública do Publicador do assembly.  
  
 `cbPublicKey`  
 no O tamanho em bytes de `pbPublicKey` .  
  
 `ulHashAlgId`  
 no O identificador do algoritmo de hash usado para fazer o hash dos arquivos de assembly.  
  
 `szName`  
 no O nome de texto legível por humanos do assembly.  
  
 `pMetaData`  
 no Um ponteiro para o ASSEMBLYMETADATA que contém informações de versão, plataforma e localidade para o assembly.  
  
 `dwAssemblyFlags`  
 no Uma combinação de bits de valores [AssemblyFlags](assemblyflags-enumeration.md) que especifica vários atributos do assembly.  
  
## <a name="remarks"></a>Comentários  

 Para criar uma `Assembly` estrutura de metadados, use o método [IMetaDataAssemblyEmit::D efineassembly](imetadataassemblyemit-defineassembly-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)
