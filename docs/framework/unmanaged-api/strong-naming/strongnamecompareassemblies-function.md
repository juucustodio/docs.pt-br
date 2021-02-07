---
description: 'Saiba mais sobre: função StrongNameCompareAssemblies'
title: Função StrongNameCompareAssemblies
ms.date: 03/30/2017
api_name:
- StrongNameCompareAssemblies
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameCompareAssemblies
helpviewer_keywords:
- StrongNameCompareAssemblies function [.NET Framework strong naming]
ms.assetid: 763f2375-efc6-4219-8806-a3b0567ef72b
topic_type:
- apiref
ms.openlocfilehash: e59bb96a89dc1e1cf8b809c3e0d538aaffe83b8e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736482"
---
# <a name="strongnamecompareassemblies-function"></a>Função StrongNameCompareAssemblies

Determina se dois assemblies diferem somente por suas assinaturas de nome forte.  
  
 Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: StrongNameCompareAssemblies](../hosting/iclrstrongname-strongnamecompareassemblies-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOLEAN StrongNameCompareAssemblies (  
    [in]  LPCWSTR   wszAssembly1,  
    [in]  LPCWSTR   wszAssembly2,  
    [out] DWORD     *pdwResult  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wszAssembly1`  
 no O caminho para o primeiro assembly.  
  
 `wszAssembly2`  
 no O caminho para o segundo assembly.  
  
 `pdwResult`  
 fora Um dos seguintes valores:  
  
- `SN_CMP_DIFFERENT` (0)-especifica que os assemblies contêm dados diferentes.  
  
- `SN_CMP_IDENTICAL` (1)-especifica que os assemblies são exatamente iguais, incluindo suas assinaturas e soma de verificação.  
  
- `SN_CMP_SIGONLY` (2)-especifica que os assemblies diferem somente por assinatura e soma de verificação.  
  
## <a name="return-value"></a>Valor retornado  

 `true` após a conclusão bem-sucedida; caso contrário, `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="remarks"></a>Comentários  

 A assinatura de nome forte de um assembly consiste no nome de texto, versão, cultura e token de chave pública do assembly.  
  
 Se a `StrongNameCompareAssemblies` função não for concluída com êxito, chame a função [StrongNameErrorInfo](strongnameerrorinfo-function.md) para recuperar o último erro gerado.  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameCompareAssemblies](../hosting/iclrstrongname-strongnamecompareassemblies-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
