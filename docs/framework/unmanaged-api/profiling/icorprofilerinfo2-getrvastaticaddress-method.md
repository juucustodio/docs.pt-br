---
description: 'Saiba mais sobre o método: ICorProfilerInfo2:: GetRVAStaticAddress'
title: Método ICorProfilerInfo2::GetRVAStaticAddress
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetRVAStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetRVAStaticAddress
helpviewer_keywords:
- GetRVAStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetRVAStaticAddress method [.NET Framework profiling]
ms.assetid: a25a8f8b-5cfa-440d-9376-a1a1c3a9fc11
topic_type:
- apiref
ms.openlocfilehash: e72a136ca0d8462d19c57da021e9429528555dac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716400"
---
# <a name="icorprofilerinfo2getrvastaticaddress-method"></a>Método ICorProfilerInfo2::GetRVAStaticAddress

Obtém o endereço do campo estático de endereço virtual relativo (RVA) especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRVAStaticAddress(  
    [in] ClassID classId,  
    [in] mdFieldDef fieldToken,  
    [out] void **ppAddress);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `classId`  
 no A ID da classe que contém o campo RVA-static solicitado.  
  
 `fieldToken`  
 no Token de metadados para o campo RVA-static solicitado.  
  
 `ppAddress`  
 fora Um ponteiro para o endereço do campo RVA-estático.  
  
## <a name="remarks"></a>Comentários  

 O `GetRVAStaticAddress` método pode retornar um dos seguintes:  
  
- Um CORPROF_E_DATAINCOMPLETE HRESULT se o campo estático fornecido não tiver sido atribuído um endereço no contexto especificado.  
  
- Os endereços de objetos que podem estar no heap de coleta de lixo. Esses endereços podem se tornar inválidos após a coleta de lixo, portanto, após a coleta de lixo, os profileres não devem presumir que eles são válidos.  
  
 Antes que o construtor de classe de uma classe seja concluído, o `GetRVAStaticAddress` retornará CORPROF_E_DATAINCOMPLETE para todos os seus campos estáticos, embora alguns dos campos estáticos já possam ser inicializados e possam estar enraizadando objetos de coleta de lixo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Interface ICorProfilerInfo2](icorprofilerinfo2-interface.md)
