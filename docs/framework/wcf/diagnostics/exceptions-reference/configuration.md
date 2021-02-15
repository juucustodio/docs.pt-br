---
description: 'Saiba mais sobre: configuração'
title: Configuração
ms.date: 03/30/2017
ms.assetid: 86a6e12f-73b5-450e-8725-f4ca5fe0702c
ms.openlocfilehash: a0eaafc9f2b33441e80a35d103f6e13bd562dd70
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99759777"
---
# <a name="configuration"></a>Configuração

Este tópico lista todas as exceções geradas pela configuração do Windows Communication Foundation (WCF).  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|ConfigBindingCannotBeConfigured|A associação no ponto de extremidade de serviço não pode ser configurada.|  
|ConfigElementKeyNull|A chave de elemento de configuração específica não pode ser nula.|  
|ConfigExtensionTypeNotRegisteredInCollection|O tipo de extensão específico não está registrado na coleção de extensão específica.|  
|ConfigIndexOutOfRange|O valor do atributo específico está fora do intervalo.|  
|ConfigInvalidBindingConfigurationName|A configuração específica não tem uma associação com o nome específico.|  
|ConfigInvalidBindingName|A configuração específica não tem uma associação com o nome específico. Este é um valor inválido para a associação.|  
|ConfigInvalidCommonEndpointBehaviorType|Não é possível adicionar a extensão de comportamento específica ao comportamento de ponto de extremidade comum porque ela não implementa o tipo específico.|  
|ConfigInvalidCommonServiceBehaviorType|Não é possível adicionar a extensão de comportamento específica ao comportamento de serviço comum porque ela não implementa o tipo específico.|  
|ConfigInvalidEndpointBehaviorType|Não é possível adicionar a extensão de comportamento específica ao comportamento de ponto de extremidade específico porque o tipo de comportamento subjacente não implementa a interface IServiceBehavior.|  
|ConfigInvalidExtensionType|O tipo específico deve derivar da extensão específica a ser usada na coleção.|  
|ConfigInvalidServiceBehaviorType|Não é possível adicionar a extensão de comportamento ' ao comportamento do serviço com o nome específico porque o tipo de comportamento subjacente não implementa a interface IServiceBehavior.|  
|ConfigMessageEncodingAlreadyInBinding|Não é possível adicionar o elemento de codificação de mensagem específico. Outro elemento de codificação de mensagem já existe na associação específica. Só pode haver um elemento de codificação de mensagem para cada associação.|  
|ConfigNoExtensionCollectionAssociatedWithType|Não é possível localizar a coleção de extensões associada à extensão do tipo específico.|  
|ConfigSectionNotFound|Não é possível criar a seção de configuração específica. As informações estão faltando no arquivo de Machine.config. Verifique se esta seção de configuração está corretamente registrada e se você escreveu corretamente o nome da seção. Para Windows Communication Foundation seções, execute ServiceModelReg.exe-i para corrigir esse erro.|  
|ConfigTransportAlreadyInBinding|Não é possível adicionar o elemento de transporte específico. Outro elemento de transporte já existe na associação específica. Só pode haver um elemento de codificação de mensagem para cada associação.|
