---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetMemberProps'
title: Método IMetaDataImport::GetMemberProps
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberProps
helpviewer_keywords:
- IMetaDataImport::GetMemberProps method [.NET Framework metadata]
- GetMemberProps method [.NET Framework metadata]
ms.assetid: 42790918-4142-4938-b8f4-a56979a55846
topic_type:
- apiref
ms.openlocfilehash: 073c8fae06c3df69f0b3152b109417b818637d1c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783892"
---
# <a name="imetadataimportgetmemberprops-method"></a>Método IMetaDataImport::GetMemberProps

Obtém informações armazenadas nos metadados para uma definição de membro especificada, incluindo o nome, a assinatura binária e o endereço virtual relativo, do <xref:System.Type> membro referenciado pelo token de metadados especificado. Este é um método auxiliar simples: se *MB* for um MethodDef, **GetMethodProps** será chamado; Se *MB* for um FieldDef, então **GetFieldProps** será chamado. Consulte esses outros métodos para obter detalhes.
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMemberProps (  
   [in]  mdToken           mb,
   [out] mdTypeDef         *pClass,  
   [out] LPWSTR            szMember,
   [in]  ULONG             cchMember,
   [out] ULONG             *pchMember,
   [out] DWORD             *pdwAttr,  
   [out] PCCOR_SIGNATURE   *ppvSigBlob,
   [out] ULONG             *pcbSigBlob,
   [out] ULONG             *pulCodeRVA,
   [out] DWORD             *pdwImplFlags,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppValue,  
   [out] ULONG             *pcchValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `mb`  
 no O token que faz referência ao membro para obter os metadados associados.  
  
 `pClass`  
 fora Um ponteiro para o token de metadados que representa a classe do membro.  
  
 `szMember`  
 fora O nome do membro.  
  
 `cchMember`  
 no O tamanho em caracteres largos do `szMember` buffer.  
  
 `pchMember`  
 fora O tamanho em caracteres largos do nome retornado.  
  
 `pdwAttr`  
 fora Quaisquer valores de sinalizador aplicados ao membro.  
  
 `ppvSigBlob`  
 fora Um ponteiro para a assinatura de metadados binários do membro.  
  
 `pcbSigBlob`  
 fora O tamanho em bytes de `ppvSigBlob` .  
  
 `pulCodeRVA`  
 fora Um ponteiro para o endereço virtual relativo do membro.  
  
 `pdwImplFlags`  
 fora Quaisquer sinalizadores de implementação de método associados ao membro.  
  
 `pdwCPlusTypeFlag`  
 fora Um sinalizador que marca um <xref:System.ValueType> . É um dos `ELEMENT_TYPE_*` valores.
  
 `ppValue`  
 fora Um valor de cadeia de caracteres constante retornado por este membro.  
  
 `pcchValue`  
 fora O tamanho em caracteres de `ppValue` , ou zero, se não `ppValue` mantiver uma cadeia de caracteres.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
