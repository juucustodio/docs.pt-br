---
description: 'Saiba mais sobre: Enumeração CeeSectionRelocType'
title: Enumeração CeeSectionRelocType
ms.date: 03/30/2017
api_name:
- CeeSectionRelocType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CeeSectionRelocType
helpviewer_keywords:
- CeeSectionRelocType enumeration [.NET Framework metadata]
ms.assetid: 124656f6-0dad-4ceb-9043-d3869ab65cde
topic_type:
- apiref
ms.openlocfilehash: 49f7b39b3cc4c2e71dd3e4e426d0ca787e9ac0b3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99678829"
---
# <a name="ceesectionreloctype-enumeration"></a>Enumeração CeeSectionRelocType

Fornece valores para influenciar o tipo de `reloc` instrução emitido em uma chamada para [ICeeGen:: AddSectionReloc](iceegen-addsectionreloc-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum  {  
    srRelocAbsolute,  
    srRelocHighLow          = 3,  
    srRelocHighAdj,
    srRelocMapToken,  
    srRelocRelative,  
    srRelocFilePos,  
    srRelocCodeRelative,  
    srRelocIA64Imm64,  
    srRelocDir64,  
    srRelocIA64PcRel25,  
    srRelocIA64PcRel64,    srRelocAbsoluteTagged,    srRelocSentinel,    srNoBaseReloc       = 0x4000,  
    srRelocPtr          = 0x8000,  
    srRelocAbsolutePtr      = srRelocPtr + srRelocAbsolute,  
    srRelocHighLowPtr       = srRelocPtr + srRelocHighLow,  
    srRelocRelativePtr      = srRelocPtr + srRelocRelative,  
    srRelocIA64Imm64Ptr     = srRelocPtr + srRelocIA64Imm64,  
    srRelocDir64Ptr         = srRelocPtr + srRelocDir64  
    } CeeSectionRelocType;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`srRelocAbsolute`|Gera apenas uma seção relativa `reloc` , enviando nada para uma seção. realocação.|  
|`srRelocHighLow`|Gera um `reloc` para um local de tamanho de ponteiro. Isso é transformado em BASED_HIGHLOW ou BASED_DIR64 dependendo da plataforma.|  
|`srRelocHighAdj`|Gera um `reloc` para os 16 bits superiores de um número de 32 bits, em que os 16 bits inferiores são incluídos na próxima palavra na tabela. realocação.|  
|`srRelocMapToken`|Gera uma realocação de mapa de token, enviando nada para uma seção. realocação.|  
|`srRelocRelative`|Indica que o valor é uma correção de endereço relativa.|  
|`srRelocFilePos`|Gera apenas uma seção relativa `reloc` , enviando nada para uma seção. realocação. Isso `reloc` é relativo à posição do arquivo da seção, não do endereço virtual da seção.|  
|`srRelocCodeRelative`|Especifica uma correção de endereço relativa ao código.|  
|`srRelocIA64Imm64`|Gera um `reloc` para um endereço de 64 bits em uma `movl` instrução IA64.|  
|`srRelocDir64`|Gera um `reloc` para um endereço de 64 bits.|  
|`srRelocIA64PcRel25`|Gere um `reloc` para um endereço de 25 bits relativo a um PC em uma `br.call` instrução IA64.|  
|`srRelocIA64PcRel64`|Gera um `reloc` para um endereço de PC de 64 bits em uma instrução IA64 `brl.call` .|  
|`srRelocAbsoluteTagged`|Gera uma seção-relativa de 30 bits `reloc` , usada para valores de ponteiros marcados.|  
|`srRelocSentinel`|Um valor de sentinela para ajudar a garantir que todas as adições a essa enumeração sejam refletidas na `reloc` matriz de nome interno.|  
|`srNoBaseReloc`|Especifica não emitir uma base `reloc` .|  
|`srRelocPtr`|Um valor que indica que o conteúdo de ajuste prévio da memória é um ponteiro em vez de um deslocamento de seção.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
- [Interface ICeeGen](iceegen-interface.md)
- [Método AddSectionReloc](iceegen-addsectionreloc-method.md)
