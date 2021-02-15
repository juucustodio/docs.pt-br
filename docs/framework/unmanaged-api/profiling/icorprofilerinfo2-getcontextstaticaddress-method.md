---
description: 'Saiba mais sobre o método: ICorProfilerInfo2:: GetContextStaticAddress'
title: Método ICorProfilerInfo2::GetContextStaticAddress
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetContextStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetContextStaticAddress
helpviewer_keywords:
- GetContextStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetContextStaticAddress method [.NET Framework profiling]
ms.assetid: 2b374116-0972-416a-8cf5-79213129be9a
topic_type:
- apiref
ms.openlocfilehash: 7ea8b81c8b1dba4577e070eda68e760cc39f9131
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760459"
---
# <a name="icorprofilerinfo2getcontextstaticaddress-method"></a>Método ICorProfilerInfo2::GetContextStaticAddress

Obtém o endereço do campo estático de contexto especificado que está no escopo do contexto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetContextStaticAddress(  
    [in] ClassID classId,  
    [in] mdFieldDef fieldToken,  
    [in] ContextID contextId,  
    [out] void **ppAddress);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `classId`  
 no A ID da classe que contém o campo estático de contexto solicitado.  
  
 `fieldToken`  
 no O token de metadados para o campo estático de contexto solicitado.  
  
 `contextId`  
 no A ID do contexto que é o escopo do campo estático de contexto solicitado.  
  
 `ppAddress`  
 fora Um ponteiro para o endereço do campo estático que está dentro do contexto especificado.  
  
## <a name="remarks"></a>Comentários  

 O `GetContextStaticAddress` método pode retornar um dos seguintes:  
  
- Um CORPROF_E_DATAINCOMPLETE HRESULT se o campo estático fornecido não tiver sido atribuído um endereço no contexto especificado.  
  
- Os endereços de objetos que podem estar no heap de coleta de lixo. Esses endereços podem se tornar inválidos após a coleta de lixo, portanto, após a coleta de lixo, os profileres não devem presumir que eles são válidos.  
  
 Antes que o construtor de classe de uma classe seja concluído, o `GetContextStaticAddress` retornará CORPROF_E_DATAINCOMPLETE para todos os seus campos estáticos, embora alguns dos campos estáticos já possam ser inicializados e a raiz dos objetos de coleta de lixo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Interface ICorProfilerInfo2](icorprofilerinfo2-interface.md)
