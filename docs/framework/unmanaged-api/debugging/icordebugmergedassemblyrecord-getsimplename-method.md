---
description: 'Saiba mais sobre: método ICorDebugMergedAssemblyRecord:: getsimplesname'
title: 'Método ICorDebugMergedAssemblyRecord:: getsimplesname'
ms.date: 03/30/2017
ms.assetid: bc3410f6-ebca-4bca-9b45-fc38c74fa9cb
ms.openlocfilehash: e77a5cc7df009a5bc55a7eb952ead80e5f81f271
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650385"
---
# <a name="icordebugmergedassemblyrecordgetsimplename-method"></a>Método ICorDebugMergedAssemblyRecord:: getsimplesname

Obtém o nome simples do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSimpleName(  
   [in] ULONG32 cchName,
   [out] ULONG32 *pcchName,
   [out, size_is(cchName), length_is(*pcchName)] WCHAR szName[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchName`  
 no O número de caracteres no `szName` buffer.  
  
 `pcchName`  
 fora Um ponteiro para o número de caracteres realmente gravados no `szName` buffer.  
  
 `szName`  
 Um ponteiro para uma matriz de caracteres.  
  
## <a name="remarks"></a>Comentários  

 Esse método recupera o nome simples de um assembly (como "System. Collections"), sem uma extensão de arquivo, versão, cultura ou token de chave pública. Ele corresponde à <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType> propriedade no código gerenciado.  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMergedAssemblyRecord](icordebugmergedassemblyrecord-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
