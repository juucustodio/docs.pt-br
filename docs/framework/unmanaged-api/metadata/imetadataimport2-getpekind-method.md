---
description: 'Saiba mais sobre o método: IMetaDataImport2:: GetPEKind'
title: Método IMetaDataImport2::GetPEKind
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetPEKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetPEKind
helpviewer_keywords:
- GetPEKind method [.NET Framework metadata]
- IMetaDataImport2::GetPEKind method [.NET Framework metadata]
ms.assetid: d91c3d89-8022-4a4c-a2a2-a8af2c387507
topic_type:
- apiref
ms.openlocfilehash: 3cd003f4b1a56f59b9e8c89bf1c4f8f2f8c7fea1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99688566"
---
# <a name="imetadataimport2getpekind-method"></a>Método IMetaDataImport2::GetPEKind

Obtém um valor que identifica a natureza do código no arquivo executável portátil (PE), normalmente um arquivo DLL ou EXE, que é definido no escopo de metadados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetPEKind (  
   [out] DWORD *pdwPEKind,  
   [out] DWORD *pdwMachine  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwPEKind`  
 fora Um ponteiro para um valor da enumeração [CorPEKind](corpekind-enumeration.md) que descreve o arquivo PE.  
  
 `pdwMachine`  
 fora Um ponteiro para um valor que identifica a arquitetura do computador. Consulte a próxima seção para obter os valores possíveis.  
  
## <a name="remarks"></a>Comentários  

 O valor referenciado pelo `pdwMachine` parâmetro pode ser um dos seguintes.  
  
|Valor|Arquitetura do computador|  
|-----------|--------------------------|  
|IMAGE_FILE_MACHINE_I386<br /><br /> 0x014C|x86|  
|IMAGE_FILE_MACHINE_IA64<br /><br /> 0x0200|IPF Intel|  
|IMAGE_FILE_MACHINE_AMD64<br /><br /> 0x8664|x64|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport2](imetadataimport2-interface.md)
- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Enumeração CorPEKind](corpekind-enumeration.md)
