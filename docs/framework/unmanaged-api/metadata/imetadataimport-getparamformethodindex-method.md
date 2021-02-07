---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetParamForMethodIndex'
title: Método IMetaDataImport::GetParamForMethodIndex
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetParamForMethodIndex
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetParamForMethodIndex
helpviewer_keywords:
- IMetaDataImport::GetParamForMethodIndex method [.NET Framework metadata]
- GetParamForMethodIndex method [.NET Framework metadata]
ms.assetid: ec3bfa95-1920-4511-932e-3ff23d76fcb8
topic_type:
- apiref
ms.openlocfilehash: d84b26f1239e548b6cf96d1e6b38791eb6ecddff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728139"
---
# <a name="imetadataimportgetparamformethodindex-method"></a>Método IMetaDataImport::GetParamForMethodIndex

Obtém o token que representa um parâmetro especificado do método representado pelo token MethodDef especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetParamForMethodIndex (  
   [in]  mdMethodDef      md,  
   [in]  ULONG            ulParamSeq,  
   [out] mdParamDef       *ppd  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `md`  
 no Um token que representa o método para o qual retornar o token de parâmetro.  
  
 `ulParamSeq`  
 no A posição ordinal na lista de parâmetros na qual o parâmetro solicitado ocorre. Os parâmetros são numerados a partir de um, com o valor de retorno do método na posição zero.  
  
 `ppd`  
 fora Um ponteiro para um token ParamDef que representa o parâmetro solicitado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
