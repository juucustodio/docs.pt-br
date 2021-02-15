---
description: 'Saiba mais sobre o método: ICorDebugMergedAssemblyRecord:: getculture'
title: 'Método ICorDebugMergedAssemblyRecord:: getculture'
ms.date: 03/30/2017
ms.assetid: 030b2f8c-8c21-40b7-855d-3afa78975a17
ms.openlocfilehash: f530bb68a1e7e4c4bff53b8f3046f6ae9ca42aab
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753998"
---
# <a name="icordebugmergedassemblyrecordgetculture-method"></a>Método ICorDebugMergedAssemblyRecord:: getculture

Obtém a cadeia de caracteres do nome da cultura do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCulture(  
   [in] ULONG32 cchCulture,
   [out] ULONG32 *pcchCulture,
   [out, size_is(cchCulture), length_is(*pcchCulture)] WCHAR szCulture[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchCulture`  
 no O número de caracteres no `szCulture` buffer.  
  
 `pcchCulture`  
 fora O número de caracteres realmente gravados no `szCulture` buffer.  
  
 `szCulture`  
 fora Uma matriz de caracteres que contém o nome da cultura.  
  
## <a name="remarks"></a>Comentários  

 O nome da cultura é uma cadeia de caracteres exclusiva que identifica uma cultura, como "en-US" (para a cultura em inglês (Estados Unidos)) ou "neutro" (para uma cultura neutra).  
  
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
