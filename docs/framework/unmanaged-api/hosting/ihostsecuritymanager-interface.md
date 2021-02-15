---
description: 'Saiba mais sobre: interface IHostSecurityManager'
title: Interface IHostSecurityManager
ms.date: 03/30/2017
api_name:
- IHostSecurityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager
helpviewer_keywords:
- IHostSecurityManager interface [.NET Framework hosting]
ms.assetid: c3be2cbd-2d93-438b-9888-9a0251b63c03
topic_type:
- apiref
ms.openlocfilehash: 76ba26443fa2a4e65459dd073eb6d22031548112
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99671523"
---
# <a name="ihostsecuritymanager-interface"></a>Interface IHostSecurityManager

Fornece métodos que permitem o acesso e o controle sobre o contexto de segurança do thread em execução no momento.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetSecurityContext](ihostsecuritymanager-getsecuritycontext-method.md)|Obtém o [IHostSecurityContext](ihostsecuritycontext-interface.md) solicitado do host.|  
|[Método ImpersonateLoggedOnUser](ihostsecuritymanager-impersonateloggedonuser-method.md)|Solicita que o código seja executado usando as credenciais da identidade do usuário atual.|  
|[Método OpenThreadToken](ihostsecuritymanager-openthreadtoken-method.md)|Abre o token de acesso discricionário associado ao thread atual.|  
|[Método RevertToSelf](ihostsecuritymanager-reverttoself-method.md)|Encerra a representação da identidade do usuário atual e retorna o token do thread original.|  
|[Método SetSecurityContext](ihostsecuritymanager-setsecuritycontext-method.md)|Define o contexto de segurança para o thread em execução no momento.|  
|[Método SetThreadToken](ihostsecuritymanager-setthreadtoken-method.md)|Define um identificador para o thread em execução no momento.|  
  
## <a name="remarks"></a>Comentários  

 Um host pode controlar todo o acesso de código aos tokens de thread pelo Common Language Runtime (CLR) e pelo código do usuário. Ele também pode garantir que as informações completas do contexto de segurança sejam passadas entre operações assíncronas ou pontos de código com acesso restrito ao código. `IHostSecurityContext` encapsula essas informações de contexto de segurança, que são opacas para o CLR.  
  
 O CLR lida internamente com o contexto de thread gerenciado. Ele consulta o processo específico `IHostSecurityManager` nas seguintes situações:  
  
- No thread do finalizador, durante a execução do finalizador.  
  
- Durante a execução do construtor de classes e módulos.  
  
- Em pontos assíncronos no thread de trabalho, em chamadas para o método [IHostThreadPoolManager:: QueueUserWorkItem](ihostthreadpoolmanager-queueuserworkitem-method.md) .  
  
- Em serviços de portas de conclusão de e/s.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostSecurityContext](ihostsecuritycontext-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
