---
description: 'Saiba mais sobre: interface ICorDebugAppDomain'
title: Método ICorDebugAppDomain
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain
helpviewer_keywords:
- ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: be7ae711-1217-4a44-be40-166e29641b77
topic_type:
- apiref
ms.openlocfilehash: 5f1ac20a7376a741da2e34de74c810c0f45e8293
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754189"
---
# <a name="icordebugappdomain-interface"></a>Método ICorDebugAppDomain

Fornece métodos para depurar domínios de aplicativo. Essa interface é uma subclasse de ICorDebugController.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Attach](icordebugappdomain-attach-method.md)|Anexa o depurador ao domínio do aplicativo.|  
|[Método EnumerateAssemblies](icordebugappdomain-enumerateassemblies-method.md)|Obtém um enumerador para os assemblies no domínio do aplicativo.|  
|[Método EnumerateBreakpoints](icordebugappdomain-enumeratebreakpoints-method.md)|Obtém um enumerador para todos os pontos de interrupção ativos no domínio do aplicativo.|  
|[Método EnumerateSteppers](icordebugappdomain-enumeratesteppers-method.md)|Obtém um enumerador para todos os percorridos ativos no domínio do aplicativo.|  
|[Método GetId](icordebugappdomain-getid-method.md)|Obtém a ID exclusiva do domínio do aplicativo.|  
|[Método GetModuleFromMetaDataInterface](icordebugappdomain-getmodulefrommetadatainterface-method.md)|Obtém o objeto ICorDebugModule com a interface de metadados fornecida.|  
|[Método GetName](icordebugappdomain-getname-method.md)|Obtém o nome do domínio do aplicativo.|  
|[Método GetObject](icordebugappdomain-getobject-method.md)|Obtém um ponteiro de interface para o domínio do aplicativo Common Language Runtime (CLR).|  
|[Método GetProcess](icordebugappdomain-getprocess-method.md)|Obtém o processo que contém o domínio do aplicativo.|  
|[Método IsAttached](icordebugappdomain-isattached-method.md)|Determina se o depurador está anexado ao domínio do aplicativo.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
