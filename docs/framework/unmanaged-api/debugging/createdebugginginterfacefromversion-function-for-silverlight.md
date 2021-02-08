---
description: 'Saiba mais sobre: Função CreateDebuggingInterfaceFromVersion para o Silverlight'
title: Função CreateDebuggingInterfaceFromVersion para Silverlight
ms.date: 03/30/2017
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function
- debugging API [Silverlight]
- Silverlight, debugging
ms.assetid: 35c7a18f-133a-4584-bd25-bb338568b0c6
ms.openlocfilehash: 8c61593f2e912260ecca65efce9f905ce56e88dc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801443"
---
# <a name="createdebugginginterfacefromversion-function-for-silverlight"></a>Função CreateDebuggingInterfaceFromVersion para Silverlight

Aceita uma cadeia de caracteres de versão Common Language Runtime (CLR) retornada da [função CreateVersionStringFromModule](createversionstringfrommodule-function.md)e retorna uma interface de depurador correspondente (normalmente, [ICorDebug](icordebug-interface.md)).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  LPCWSTR      szDebuggeeVersion,  
    [out] IUnknown**   ppCordb,  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `szDebuggeeVersion`\
 no Cadeia de caracteres da versão do CLR no depurador de destino, que é retornada pela [função CreateVersionStringFromModule](createversionstringfrommodule-function.md).  
  
 `ppCordb`\
 fora Ponteiro para um ponteiro para um objeto COM ( `IUnknown` ). Esse objeto será convertido em um objeto [ICorDebug](icordebug-interface.md) antes de ser retornado.  
  
## <a name="return-value"></a>Valor retornado

 `S_OK`\
 `ppCordb` faz referência a um objeto válido que implementa a interface de [interface ICorDebug](icordebug-interface.md) .  
  
 `E_INVALIDARG`\
 `szDebuggeeVersion`Ou `ppCordb` é nulo.  
  
 `CORDBG_E_DEBUG_COMPONENT_MISSING`\
 Não é possível localizar um componente necessário para a depuração CLR. O _mscordbi.dll_ ou _mscordaccore.dll_ não foi encontrado no mesmo diretório que o CoreCLR.dll de destino.  
  
 `CORDBG_E_INCOMPATIBLE_PROTOCOL`\
 O mscordbi.dll ou mscordaccore.dll não é a mesma versão que o CoreCLR.dll de destino.  
  
 `E_FAIL` (ou outros `E_` códigos de retorno) \
 Não é possível retornar uma [interface ICorDebug](icordebug-interface.md).  
  
## <a name="remarks"></a>Comentários

 A interface retornada fornece os recursos para anexar a um CLR em um processo de destino e depurar o código gerenciado que o CLR está executando.  
  
## <a name="requirements"></a>Requisitos

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** dbgshim. h  
  
 **Biblioteca:** dbgshim.dll  
  
 **Versões do .NET Framework:** 3,5 SP1
