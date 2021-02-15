---
description: 'Saiba mais sobre: método SetAssemblyProps'
title: Método SetAssemblyProps
ms.date: 03/30/2017
api_name:
- IALink.SetAssemblyProps
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetAssemblyProps
helpviewer_keywords:
- SetAssemblyProps method
ms.assetid: a3d7cf29-1414-49e6-8aae-9b3283c4f5f0
topic_type:
- apiref
ms.openlocfilehash: 212d8aad22ac1cb231db46f20ff65de2339a21aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662345"
---
# <a name="setassemblyprops-method"></a>Método SetAssemblyProps

Atribui propriedades no nível do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetAssemblyProps(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    AssemblyOptions Option,  
    VARIANT         Value  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID do assembly.  
  
 `FileToken`  
 Arquivo que define a propriedade. Pode ser NULL se não `AssemblyID` indicar um netmodule não associado.  
  
 `Option`  
 Indica a opção a ser modificada.  
  
 `Value`  
 Novo valor da opção.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
