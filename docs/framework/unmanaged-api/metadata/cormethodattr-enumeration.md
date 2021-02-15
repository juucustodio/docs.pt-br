---
description: 'Saiba mais sobre: Enumeração CorMethodAttr'
title: Enumeração CorMethodAttr
ms.date: 03/30/2017
api_name:
- CorMethodAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorMethodAttr
helpviewer_keywords:
- CorMethodAttr enumeration [.NET Framework metadata]
ms.assetid: 4e0c3521-e54d-43c1-9857-cc76b49b8ffc
topic_type:
- apiref
ms.openlocfilehash: 4050235675f4b237b184d31378a614a0613ab3df
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784373"
---
# <a name="cormethodattr-enumeration"></a>Enumeração CorMethodAttr

Contém valores que descrevem os recursos de um método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorMethodAttr {  
  
    mdMemberAccessMask          =   0x0007,  
    mdPrivateScope              =   0x0000,  
    mdPrivate                   =   0x0001,  
    mdFamANDAssem               =   0x0002,  
    mdAssem                     =   0x0003,  
    mdFamily                    =   0x0004,  
    mdFamORAssem                =   0x0005,  
    mdPublic                    =   0x0006,  
  
    mdStatic                    =   0x0010,  
    mdFinal                     =   0x0020,  
    mdVirtual                   =   0x0040,  
    mdHideBySig                 =   0x0080,  
  
    mdVtableLayoutMask          =   0x0100,  
    mdReuseSlot                 =   0x0000,  
    mdNewSlot                   =   0x0100,  
  
    mdCheckAccessOnOverride     =   0x0200,  
    mdAbstract                  =   0x0400,  
    mdSpecialName               =   0x0800,  
  
    mdPinvokeImpl               =   0x2000,  
    mdUnmanagedExport           =   0x0008,  
  
    mdReservedMask              =   0xd000,  
    mdRTSpecialName             =   0x1000,  
    mdHasSecurity               =   0x4000,  
    mdRequireSecObject          =   0x8000,  
  
} CorMethodAttr;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`mdMemberAccessMask`|Especifica o acesso de membro.|  
|`mdPrivateScope`|Especifica que o membro não pode ser referenciado.|  
|`mdPrivate`|Especifica que o membro é acessível somente pelo tipo pai.|  
|`mdFamANDAssem`|Especifica que o membro é acessível por subtipos somente neste assembly.|  
|`mdAssem`|Especifica que o membro é accessibly por qualquer pessoa no assembly.|  
|`mdFamily`|Especifica que o membro é acessível somente por tipo e subtipos.|  
|`mdFamORAssem`|Especifica que o membro é acessível pelas classes derivadas e por outros tipos em seu assembly.|  
|`mdPublic`|Especifica que o membro é acessível por todos os tipos com acesso ao escopo.|  
|`mdStatic`|Especifica que o membro é definido como parte do tipo em vez de como um membro de uma instância.|  
|`mdFinal`|Especifica que o método não pode ser substituído.|  
|`mdVirtual`|Especifica que o método pode ser substituído.|  
|`mdHideBySig`|Especifica que o método oculta por nome e assinatura, em vez de apenas pelo nome.|  
|`mdVtableLayoutMask`|Especifica o layout da tabela virtual.|  
|`mdReuseSlot`|Especifica que o slot usado para esse método na tabela virtual seja reutilizado. Este é o padrão.|  
|`mdNewSlot`|Especifica que o método sempre Obtém um novo slot na tabela virtual.|  
|`mdCheckAccessOnOverride`|Especifica que o método pode ser substituído pelos mesmos tipos aos quais está visível.|  
|`mdAbstract`|Especifica que o método não está implementado.|  
|`mdSpecialName`|Especifica que o método é especial e que seu nome descreve como.|  
|`mdPinvokeImpl`|Especifica que a implementação do método é encaminhada usando PInvoke.|  
|`mdUnmanagedExport`|Especifica que o método é um método gerenciado exportado para código não gerenciado.|  
|`mdReservedMask`|Reservado para uso interno pelo Common Language Runtime.|  
|`mdRTSpecialName`|Especifica que a Common Language Runtime deve verificar a codificação do nome do método.|  
|`mdHasSecurity`|Especifica que o método tem segurança associada a ele.|  
|`mdRequireSecObject`|Especifica que o método chama outro método que contém o código de segurança.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
