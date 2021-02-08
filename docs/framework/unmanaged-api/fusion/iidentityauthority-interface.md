---
description: 'Saiba mais sobre: interface IIdentityAuthority'
title: Interface IIdentityAuthority
ms.date: 03/30/2017
api_name:
- IIdentityAuthority
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IIdentityAuthority
helpviewer_keywords:
- IIdentityAuthority interface [.NET Framework fusion]
ms.assetid: 6277f914-51a8-49be-bec6-52d6d648527d
topic_type:
- apiref
ms.openlocfilehash: 3064a3d95ebe9a098a7cac0766f18654c6fab8b9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800130"
---
# <a name="iidentityauthority-interface"></a>Interface IIdentityAuthority

Gerencia chaves de identidade para objetos de código.

## <a name="methods"></a>Métodos

|Método|Descrição|
|------------|-----------------|
|`IIdentityAuthority::AreDefinitionsEqual`|Obtém um valor que indica se as duas instâncias de [IDefinitionIdentity](idefinitionidentity-interface.md) especificadas são iguais.|
|`IIdentityAuthority::AreReferencesEqual`|Obtém um valor que indica se as duas instâncias de [IReferenceIdentity](ireferenceidentity-interface.md) especificadas são iguais.|
|`IIdentityAuthority::AreTextualDefinitionsEqual`|Obtém um valor que indica se as duas representações de identidade de definição de cadeia de caracteres especificadas são iguais.|
|`IIdentityAuthority::AreTextualReferencesEqual`|Obtém um valor que indica se as duas representações de identidade de referência de cadeia de caracteres especificadas são iguais.|
|`IIdentityAuthority::CreateDefinition`|Obtém um ponteiro para uma nova `IDefinitionIdentity` instância que representa o objeto de código no escopo atual.|
|`IIdentityAuthority::CreateReference`|Obtém um ponteiro para uma nova `IReferenceIdentity` instância que representa o objeto de código no escopo atual.|
|`IIdentityAuthority::DefinitionToText`|Obtém uma versão de cadeia de caracteres formatada do especificada `IDefinitionIdentity` .|
|`IIdentityAuthority::DefinitionToTextBuffer`|Preenche o buffer de caracteres largos especificado com uma versão de cadeia de caracteres do especificado `IDefinitionIdentity` .|
|`IIdentityAuthority::DoesDefinitionMatchReference`|Obtém um valor que indica se as `IDefinitionIdentity` instâncias especificadas e `IReferenceIdentity` se referem ao mesmo objeto de código.|
|`IIdentityAuthority::DoesTextualDefinitionMatchTextualReference`|Obtém um valor que indica se as cadeias de caracteres especificadas se referem ao mesmo objeto de código.|
|`IIdentityAuthority::GenerateDefinitionKey`|Obtém um ponteiro para uma chave de cadeia de caracteres recém-criada para o especificado `IDefinitionIdentity` .|
|`IIdentityAuthority::GenerateReferenceKey`|Obtém um ponteiro para uma chave de cadeia de caracteres recém-criada para o especificado `IReferenceIdentity` .|
|`IIdentityAuthority::HashDefinition`|Obtém um valor de hash para o especificado `IDefinitionIdentity` .|
|`IIdentityAuthority::HashReference`|Obtém um valor de hash para o especificado `IReferenceIdentity` .|
|`IIdentityAuthority::ReferenceToText`|Obtém uma versão de cadeia de caracteres formatada do especificada `IReferenceIdentity` .|
|`IIdentityAuthority::ReferenceToTextBuffer`|Preenche o buffer de caracteres largos especificado com uma versão de cadeia de caracteres do especificado `IReferenceIdentity` .|
|`IIdentityAuthority::TextToDefinition`|Obtém um ponteiro de interface para uma `IDefinitionIdentity` instância gerada a partir da cadeia de caracteres formatada especificada.|
|`IIdentityAuthority::TextToReference`|Obtém um ponteiro de interface para uma `IReferenceIdentity` instância gerada a partir da cadeia de caracteres formatada especificada.|

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** Isolamento. h

**.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
