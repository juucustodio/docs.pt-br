---
description: 'Saiba mais sobre o método: IMetaDataTables:: GetString'
title: Método IMetaDataTables::GetString
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetString
helpviewer_keywords:
- IMetaDataTables::GetString method [.NET Framework metadata]
- GetString method, IMetaDataTables interface [.NET Framework metadata]
ms.assetid: 895c35cf-b95d-4e3b-93b5-cfc1cf9044fc
topic_type:
- apiref
ms.openlocfilehash: 2104e30657a152d1b9a2ace743da9b126fb15d60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99687786"
---
# <a name="imetadatatablesgetstring-method"></a>Método IMetaDataTables::GetString

Obtém a cadeia de caracteres no índice especificado da coluna de tabela no escopo de referência atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetString (
    [in]  ULONG       ixString,  
    [out] const char  **ppString  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ixString`  
 no O índice no qual começar a procurar o próximo valor.  
  
 `ppString`  
 fora Um ponteiro para um ponteiro para o valor de cadeia de caracteres retornado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataTables](imetadatatables-interface.md)
- [Interface IMetaDataTables2](imetadatatables2-interface.md)
