---
description: 'Saiba mais sobre: IMetaDataDispenser: método efineScope de:D'
title: Método IMetaDataDispenser::DefineScope
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser.DefineScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser::DefineScope
helpviewer_keywords:
- DefineScope method [.NET Framework metadata]
- IMetaDataDispenser::DefineScope method [.NET Framework metadata]
ms.assetid: af28db02-29af-45ac-aec6-8d6c6123c2ff
topic_type:
- apiref
ms.openlocfilehash: b7a7870ec06af4c08a4ef3609077eb93f74da776
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789236"
---
# <a name="imetadatadispenserdefinescope-method"></a>Método IMetaDataDispenser::DefineScope

Cria uma nova área na memória na qual você pode criar novos metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT DefineScope (  
    [in]  REFCLSID    rclsid,  
    [in]  DWORD       dwCreateFlags,  
    [in]  REFIID      riid,
    [out] IUnknown    **ppIUnk  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `rclsid`  
 no O CLSID da versão de estruturas de metadados a ser criada. Esse valor deve ser CLSID_CorMetaDataRuntime para a versão de .NET Framework 2,0.  
  
 `dwCreateFlags`  
 no Sinalizadores que especificam opções. Esse valor deve ser zero para o .NET Framework 2,0.  
  
 `riid`  
 no A IID da interface de metadados desejada a ser retornada; o chamador usará a interface para criar os novos metadados.  
  
 O valor de `riid` deve especificar uma das interfaces "Emit". Os valores válidos são IID_IMetaDataEmit, IID_IMetaDataAssemblyEmit ou IID_IMetaDataEmit2.  
  
 `ppIUnk`  
 fora O ponteiro para a interface retornada.  
  
## <a name="remarks"></a>Comentários  

 `DefineScope` Cria um conjunto de tabelas de metadados na memória, gera um GUID exclusivo (identificador de versão de módulo ou MVID) para os metadados e cria uma entrada na tabela de módulo para a unidade de compilação que está sendo emitida.  
  
 Você pode anexar atributos ao escopo de metadados como um todo usando o método [IMetaDataEmit:: SetModuleProps](imetadataemit-setmoduleprops-method.md) ou [IMetaDataEmit::D efinecustomattribute](imetadataemit-definecustomattribute-method.md) , conforme apropriado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataDispenser](imetadatadispenser-interface.md)
- [Interface IMetaDataDispenserEx](imetadatadispenserex-interface.md)
- [Interface IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)
- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
