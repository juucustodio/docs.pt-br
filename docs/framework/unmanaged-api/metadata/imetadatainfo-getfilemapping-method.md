---
description: 'Saiba mais sobre o método: IMetaDataInfo:: GetFileMapping'
title: Método IMetaDataInfo::GetFileMapping
ms.date: 03/30/2017
api_name:
- IMetaDataInfo.GetFileMapping
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataInfo::GetFileMapping
helpviewer_keywords:
- IMetaDataInfo::GetFileMapping method [.NET Framework metadata]
- GetFileMapping method [.NET Framework metadata]
ms.assetid: 2868dfec-c992-4606-88bb-a8e0b6b18271
topic_type:
- apiref
ms.openlocfilehash: 82a1a23c50a4d8340804f66966933fc6a11e0f8c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99688475"
---
# <a name="imetadatainfogetfilemapping-method"></a>Método IMetaDataInfo::GetFileMapping

Obtém a região de memória do arquivo mapeado e o tipo de mapeamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFileMapping (  
    [out] const void           **ppvData,
    [out] ULONGLONG            *pcbData,
    [out] DWORD                *pdwMappingType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppvData`  
 fora Um ponteiro para o início do arquivo mapeado.  
  
 `pcbData`  
 fora O tamanho da região mapeada. Se `pdwMappingType` for `fmFlat` , esse é o tamanho do arquivo.  
  
 `pdwMappingType`  
 fora Um valor [CorFileMapping](corfilemapping-enumeration.md) que indica o tipo de mapeamento. A implementação atual do Common Language Runtime (CLR) sempre retorna `fmFlat` . Outros valores são reservados para uso futuro. No entanto, você sempre deve verificar o valor retornado, pois outros valores podem ser habilitados em versões futuras ou versões de serviço.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|Todas as saídas são preenchidas.|  
|`E_INVALIDARG`|NULL foi passado como um valor de argumento.|  
|`COR_E_NOTSUPPORTED`|A implementação do CLR não pode fornecer informações sobre a região da memória. Isso pode ocorrer pelos seguintes motivos:<br /><br /> -O escopo de metadados foi aberto com `ofWrite` o `ofCopyMemory` sinalizador ou.<br />-O escopo de metadados foi aberto sem o `ofReadOnly` sinalizador.<br />-O método [IMetaDataDispenser:: OpenScopeOnMemory](imetadatadispenser-openscopeonmemory-method.md) foi usado para abrir apenas a parte de metadados do arquivo.<br />-O arquivo não é um arquivo executável portátil (PE). **Observação:**  Essas condições dependem da implementação do CLR e provavelmente serão diminuídas em versões futuras do CLR.|  
  
## <a name="remarks"></a>Comentários  

 A memória que `ppvData` aponta para é válida somente contanto que o escopo de metadados subjacente esteja aberto.  
  
 Para que esse método funcione, ao mapear os metadados de um arquivo em disco para a memória chamando o método [IMetaDataDispenser:: OpenScope](imetadatadispenser-openscope-method.md) , você deve especificar o `ofReadOnly` sinalizador e não deve especificar o `ofWrite` `ofCopyMemory` sinalizador ou.  
  
 A escolha do tipo de mapeamento de arquivo para cada escopo é específica para uma determinada implementação do CLR. Ele não pode ser definido pelo usuário. A implementação atual do CLR sempre retorna `fmFlat` no `pdwMappingType` , mas isso pode ser alterado em versões futuras do CLR ou em futuras versões de serviço de determinada versão. Você sempre deve verificar o valor retornado em `pdwMappingType` , pois tipos diferentes terão layouts e deslocamentos diferentes.  
  
 Não há suporte para a passagem de NULL para qualquer um dos três parâmetros. O método retorna `E_INVALIDARG` e nenhuma das saídas é preenchida. Ignorar o tipo de mapeamento ou o tamanho da região pode resultar em um encerramento anormal do programa.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataInfo](imetadatainfo-interface.md)
- [Enumeração CorFileMapping](corfilemapping-enumeration.md)
