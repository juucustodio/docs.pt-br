---
description: 'Saiba mais sobre: interface ICLRStrongName2'
title: Interface ICLRStrongName2
ms.date: 03/30/2017
api_name:
- ICLRStrongName2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName2
helpviewer_keywords:
- ICLRStrongName2 interface [.NET Framework hosting]
ms.assetid: 9f098a74-201e-4628-a468-8dee9ab99b4a
topic_type:
- apiref
ms.openlocfilehash: 7442bd054af735e9f1b75b05feb8724dfa993f73
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781786"
---
# <a name="iclrstrongname2-interface"></a>Interface ICLRStrongName2

Fornece a capacidade de criar nomes fortes usando o grupo SHA-2 de algoritmos de hash seguro (SHA-256, SHA-384 e SHA-512).  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método StrongNameGetPublicKeyEx](strongnamegetpublickeyex-method.md)|Obtém a chave pública de um par de chaves pública/privada e especifica um algoritmo de hash e um algoritmo de assinatura.|  
|[Método StrongNameSignatureVerificationEx2](strongnamesignatureverificationex2-method.md)|Verifica a assinatura de um assembly com nome forte e fornece um mapeamento da chave ECMA para uma chave real.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]
