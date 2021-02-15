---
description: 'Saiba mais sobre: interface IMetaDataFilter'
title: Interface IMetaDataFilter
ms.date: 03/30/2017
api_name:
- IMetaDataFilter
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataFilter
helpviewer_keywords:
- IMetaDataFilter interface [.NET Framework metadata]
ms.assetid: ec0856ef-8c56-40ba-bf60-86e0ce8b337f
topic_type:
- apiref
ms.openlocfilehash: c994574207ccb26a5cb317e1673145a41f0d837d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99677919"
---
# <a name="imetadatafilter-interface"></a>Interface IMetaDataFilter

Fornece métodos para marcação e filtragem de tokens de metadados para evitar ações repetidas que já foram realizadas.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método IsTokenMarked](imetadatafilter-istokenmarked-method.md)|Obtém um valor que indica se o token de metadados especificado foi processado.|  
|[Método MarkToken](imetadatafilter-marktoken-method.md)|Define um valor que indica que o token de metadados especificado foi processado.|  
|[Método UnmarkAll](imetadatafilter-unmarkall-method.md)|Remove as marcas de processamento de todos os tokens no escopo de metadados atual.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de metadados](metadata-interfaces.md)
