---
description: 'Saiba mais sobre o método: ICeeGen:: GetSectionCreate'
title: Método ICeeGen::GetSectionCreate
ms.date: 03/30/2017
api_name:
- ICeeGen.GetSectionCreate
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetSectionCreate
helpviewer_keywords:
- ICeeGen::GetSectionCreate method [.NET Framework metadata]
- GetSectionCreate method [.NET Framework metadata]
ms.assetid: 154b2460-59ce-4874-a9f2-1b3353486ac5
topic_type:
- apiref
ms.openlocfilehash: 2839d11c927dbf573f213d3ebaa9e6e6d8d5015d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99706858"
---
# <a name="iceegengetsectioncreate-method"></a>Método ICeeGen::GetSectionCreate

Gera e obtém uma seção de código usando os valores de nome e sinalizador especificados.  
  
 Este método é obsoleto e não deve ser usado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSectionCreate (  
    [in]  const char     *name,  
    [in]  DWORD          flags,  
    [out] HCEESECTION    *section  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `name`  
 no Um ponteiro para uma cadeia de caracteres que especifica o nome da seção a ser criada.  
  
 `flags`  
 no Sinalizadores que especificam opções.  
  
 `section`  
 fora Um ponteiro para a seção de código recém-criada.  
  
## <a name="remarks"></a>Comentários  

 Chame `GetSectionCreate` somente se você tiver requisitos de seção especiais que não são tratados por outros métodos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICeeGen](iceegen-interface.md)
