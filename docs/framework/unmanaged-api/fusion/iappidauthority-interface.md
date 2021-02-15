---
description: 'Saiba mais sobre: interface IAppIdAuthority'
title: Interface IAppIdAuthority
ms.date: 03/30/2017
api_name:
- IAppIdAuthority
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAppIdAuthority
helpviewer_keywords:
- IAppIdAuthority interface [.NET Framework fusion]
ms.assetid: ec354fa1-1efd-41b0-bc43-b90597b6e253
topic_type:
- apiref
ms.openlocfilehash: 238885c7f080571b414511c24f9772dbc19b4683
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760988"
---
# <a name="iappidauthority-interface"></a>Interface IAppIdAuthority

Fornece métodos que geram e comparam chaves para identidades e referências de aplicativos.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|`IAppIdAuthority::AreDefinitionsEqual`|Obtém um valor que indica se as duas instâncias de [IDefinitionAppId](idefinitionappid-interface.md) especificadas são iguais. Você pode passar o valor do sinalizador IAPPIDAUTHORITY_ARE_DEFINITIONS_EQUAL_FLAG_IGNORE_VERSION para ignorar suas respectivas informações de versão.|  
|`IAppIdAuthority::AreReferencesEqual`|Obtém um valor que indica se as duas instâncias de [IReferenceAppId](ireferenceappid-interface.md) especificadas são iguais. Você pode passar o valor do sinalizador IAPPIDAUTHORITY_ARE_REFERENCES_EQUAL_FLAG_IGNORE_VERSION para ignorar suas respectivas informações de versão.|  
|`IAppIdAuthority::AreTextualDefinitionsEqual`|Obtém um valor que indica se as duas definições de cadeia de caracteres especificadas são iguais. Você pode passar o valor do sinalizador IAPPIDAUTHORITY_ARE_DEFINITIONS_EQUAL_FLAG_IGNORE_VERSION para ignorar suas respectivas informações de versão.|  
|`IAppIdAuthority::AreTextualReferencesEqual`|Obtém um valor que indica se as duas referências de cadeia de caracteres especificadas são iguais. Você pode passar o valor do sinalizador IAPPIDAUTHORITY_ARE_REFERENCES_EQUAL_FLAG_IGNORE_VERSION para ignorar suas respectivas informações de versão.|  
|`IAppIdAuthority::CreateDefinition`|Obtém um ponteiro de interface para uma instância gerada recentemente `IDefinitionAppId` que representa o assembly no escopo atual.|  
|`IAppIdAuthority::CreateReference`|Obtém um ponteiro de interface para um recém-criado `IReferenceAppId` que representa o assembly no escopo atual.|  
|`IAppIdAuthority::DefinitionToText`|Obtém uma versão de cadeia de caracteres do especificada `IDefinitionAppId` , usando os valores de sinalizador especificados.|  
|`IAppIdAuthority::DoesDefinitionMatchReference`|Obtém um valor que indica se o especificado `IDefinitionAppId` e `IReferenceAppId` representa o mesmo assembly.|  
|`IAppIdAuthority::DoesTextualDefinitionMatchTextualReference`|Obtém um valor que indica se a cadeia de caracteres de definição especificada e a cadeia de caracteres de referência representam o mesmo assembly.|  
|`IAppIdAuthority::GenerateDefinitionKey`|Obtém uma chave de cadeia de caracteres que representa a `IDefinitionAppId` instância especificada.|  
|`IAppIdAuthority::GenerateReferenceKey`|Obtém uma chave de cadeia de caracteres que representa a `IReferenceAppId` instância especificada.|  
|`IAppIdAuthority::HashDefinition`|Obtém uma chave de hash para a `IDefinitionAppId` instância especificada.|  
|`IAppIdAuthority::HashReference`|Obtém uma chave de hash para a `IReferenceAppId` instância especificada.|  
|`IAppIdAuthority::ReferenceToText`|Obtém uma versão de cadeia de caracteres do especificada `IReferenceAppId` , usando os valores de sinalizador especificados.|  
|`IAppIdAuthority::TextToDefinition`|Obtém um ponteiro de interface para uma `IDefinitionAppId` instância que representa o assembly referenciado pela chave de cadeia de caracteres especificada.|  
|`IAppIdAuthority::TextToReference`|Obtém um ponteiro de interface para uma `IReferenceAppId` instância que representa o assembly referenciado pela chave de cadeia de caracteres especificada.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Isolamento. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
