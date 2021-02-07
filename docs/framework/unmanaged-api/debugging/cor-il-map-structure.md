---
description: 'Saiba mais sobre: estrutura de COR_IL_MAP'
title: Estrutura COR_IL_MAP
ms.date: 03/30/2017
api_name:
- COR_IL_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_IL_MAP
helpviewer_keywords:
- COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type:
- apiref
ms.openlocfilehash: ff3d636429f51119342baea5d71163eb9d764e03
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712306"
---
# <a name="cor_il_map-structure"></a>Estrutura COR_IL_MAP

Especifica mudanças no deslocamento relativo de uma função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;
    ULONG32 newOffset;
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`oldOffset`|O antigo deslocamento da MSIL (Microsoft Intermediate Language) relativo ao início da função.|  
|`newOffset`|O novo deslocamento MSIL relativo ao início da função.|  
|`fAccurate`|`true` Se o mapeamento é conhecido como preciso; caso contrário, `false` .|  
  
## <a name="remarks"></a>Comentários  

 O formato do mapa é o seguinte: o depurador irá pressupor que `oldOffset` se refere a um deslocamento MSIL dentro do código MSIL original e não modificado. O `newOffset` parâmetro refere-se ao deslocamento MSIL correspondente dentro do novo código instrumentado.  
  
 Para que a depuração funcione corretamente, os requisitos a seguir devem ser atendidos:  
  
- O mapa deve ser classificado em ordem crescente.  
  
- O código MSIL instrumentado não deve ser reordenado.  
  
- O código MSIL original não deve ser removido.  
  
- O mapa deve incluir entradas para mapear todos os pontos de sequência do arquivo de banco de dados do programa (PDB).  
  
 O mapa não interpola as entradas ausentes. O exemplo a seguir mostra um mapa e seus resultados.  
  
 Mapeada  
  
- 0 deslocamento antigo, 0 deslocamento novo  
  
- 5 deslocamento antigo, 10 novos deslocamentos  
  
- 9 deslocamento antigo, 20 deslocamento novo  
  
 Resultados:  
  
- Um deslocamento antigo de 0, 1, 2, 3 ou 4 será mapeado para um novo deslocamento de 0.  
  
- Um deslocamento antigo de 5, 6, 7 ou 8 será mapeado para o novo deslocamento 10.  
  
- Um deslocamento antigo de 9 ou superior será mapeado para o novo deslocamento 20.  
  
- Um novo deslocamento de 0, 1, 2, 3, 4, 5, 6, 7, 8 ou 9 será mapeado para o deslocamento antigo 0.  
  
- Um novo deslocamento de 10, 11, 12, 13, 14, 15, 16, 17, 18 ou 19 será mapeado para o deslocamento antigo 5.  
  
- Um novo deslocamento de 20 ou mais será mapeado para o deslocamento antigo 9.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug. idl, CorProf. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
