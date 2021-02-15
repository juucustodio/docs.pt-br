---
description: 'Saiba mais sobre: interface ICLRMetadataLocator'
title: Interface ICLRMetadataLocator
ms.date: 03/30/2017
api_name:
- ICLRMetadataLocator
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRMetadataLocator
helpviewer_keywords:
- ICLRMetadataLocator interface [.NET Framework debugging]
ms.assetid: 43c944f4-406a-4df6-981e-0eabb33dd5d0
topic_type:
- apiref
ms.openlocfilehash: 6e7fd45197294563e12da020379d1bd54b088698
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772595"
---
# <a name="iclrmetadatalocator-interface"></a>Interface ICLRMetadataLocator

Usado pela camada de serviços de acesso a dados para localizar metadados de assemblies em um processo de destino.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetMetadata](iclrmetadatalocator-getmetadata-method.md)|Recupera os metadados de uma imagem do processo de destino.|  
  
## <a name="remarks"></a>Comentários  

 O cliente da API (ou seja, o depurador) deve implementar a interface conforme o apropriado para o processo de destino específico. Por exemplo, a implementação de um processo ao vivo seria diferente da de um despejo de memória.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
