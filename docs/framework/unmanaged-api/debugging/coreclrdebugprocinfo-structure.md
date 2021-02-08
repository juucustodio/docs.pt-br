---
description: 'Saiba mais sobre: estrutura CoreClrDebugProcInfo'
title: Estrutura CoreClrDebugProcInfo
ms.date: 03/30/2017
api_name:
- CoreClrDebugProcInfo
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- CoreClrDebugProcInfo
helpviewer_keywords:
- remote debugging API [Silverlight]
- CoreClrDebugProcInfo structure
- Silverlight, remote debugging
ms.assetid: 4ddc37da-5c94-4beb-b61c-b54071c0e749
topic_type:
- apiref
ms.openlocfilehash: 04befb057be689e68dd3571a13990da9af64551f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801482"
---
# <a name="coreclrdebugprocinfo-structure"></a>Estrutura CoreClrDebugProcInfo

Representa um processo que está sendo executado em um computador remoto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
struct  CoreClrDebugProcInfo {  
    DWORD m_dwPID;  
    DWORD m_dwInternalID;  
    WCHAR m_wszName[256];  
};  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`m_dwPID`|Identificador de processo atribuído pelo sistema operacional.|  
|`m_dwInternalID`|Identificador de processo atribuído pelo proxy de depuração remota em execução no computador de destino. Esse identificador recicla com menos frequência do que o identificador do sistema operacional.|  
|`m_wszName`|Linha de comando do processo. Esse membro pode estar truncado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CoreClrRemoteDebuggingInterfaces. h  
  
 **Biblioteca:** mscordbi_macx86.dll  
  
 **Versões do .NET Framework:** 3,5 SP1
