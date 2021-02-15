---
description: 'Saiba mais sobre: enumeração CorGenericParamAttr'
title: Enumeração CorGenericParamAttr
ms.date: 03/30/2017
api_name:
- CorGenericParamAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorGenericParamAttr
helpviewer_keywords:
- CorGenericParamAttr enumeration [.NET Framework metadata]
ms.assetid: 36c76266-71d8-48dc-bd89-54943fa659c1
topic_type:
- apiref
ms.openlocfilehash: 8fe8cb20834ecbc5477bbe8b01bf77d6b1af0eea
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784451"
---
# <a name="corgenericparamattr-enumeration"></a>Enumeração CorGenericParamAttr

Contém valores que descrevem os <xref:System.Type> parâmetros para tipos genéricos, conforme usado em chamadas para [IMetaDataEmit2::D efinegenericparam](imetadataemit2-definegenericparam-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum CorGenericParamAttr {  
  
    gpVarianceMask                     =   0x0003,  
    gpNonVariant                       =   0x0000,
    gpCovariant                        =   0x0001,  
    gpContravariant                    =   0x0002,  
  
    gpSpecialConstraintMask            =   0x001C,  
    gpNoSpecialConstraint              =   0x0000,  
    gpReferenceTypeConstraint          =   0x0004,
    gpNotNullableValueTypeConstraint   =   0x0008,  
    gpDefaultConstructorConstraint     =   0x0010  
  
} CorGenericParamAttr;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`gpVarianceMask`|A variação de parâmetro aplica-se somente a parâmetros genéricos para interfaces e delegados.|  
|`gpNonVariant`|Indica a ausência de variação.|  
|`gpCovariant`|Indica covariância.|  
|`gpContravariant`|Indica contravariância.|  
|`gpSpecialConstraintMask`|Restrições especiais podem ser aplicadas a qualquer <xref:System.Type> parâmetro.|  
|`gpNoSpecialConstraint`|Indica que nenhuma restrição se aplica ao <xref:System.Type> parâmetro.|  
|`gpReferenceTypeConstraint`|Indica que o <xref:System.Type> parâmetro deve ser um tipo de referência.|  
|`gpNotNullableValueTypeConstraint`|Indica que o <xref:System.Type> parâmetro deve ser um tipo de valor que não pode ser um valor nulo.|  
|`gpDefaultConstructorConstraint`|Indica que o <xref:System.Type> parâmetro deve ter um construtor público padrão que não aceite parâmetros.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](metadata-enumerations.md)
