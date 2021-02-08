---
description: 'Saiba mais sobre: segurança'
title: Segurança
ms.date: 03/30/2017
ms.assetid: 737ec121-bfc5-4b75-a504-2d53c2c8af39
ms.openlocfilehash: 8f095292deac77c1c72cf87a93064569f7dab982
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798089"
---
# <a name="security"></a>Segurança

A instância Store de fluxo de trabalho do SQL usa as seguintes funções de segurança de base de dados para proteger o acesso a informações do estado da instância na base de dados de persistência.  
  
- **System. Activities. DurableInstancing. InstanceStoreUsers**. Essa função tem acesso de leitura e gravação para a exibição e a direita públicas de execução procedimentos armazenados que estão envolvidos na criação, em carregar e salvar em instâncias.  
  
- **System. Activities. DurableInstancing. InstanceStoreObservers**. Essa função tem acesso somente leitura modos de exibição públicas.  
  
- **System. Activities. DurableInstancing. WorkflowActivationUsers**. Essa função tem direitos de execução procedimentos armazenados que estão envolvidos no processo de ativação da instância. Para obter mais informações sobre a ativação da instância, consulte [ativação da instância](instance-activation.md). A conta de usuário sob a qual um host genérico (como o serviço de gerenciamento de fluxo de trabalho dos recursos de hospedagem do Windows Server AppFabric) é executada deve ser adicionada a essa função de banco de dados.  
  
 Para obter mais informações sobre segurança para armazenamentos de persistência com o Windows Server app Fabric, consulte [configuração de segurança para repositórios de persistência no app Fabric](/previous-versions/appfabric/ff431727(v=azure.10))  
  
> [!CAUTION]
> Um cliente que tenha acesso a seus próprios dados de instância no armazenamento de instância tem acesso a todas as outras instâncias no mesmo armazenamento de instância. O armazenamento de instância não suporta especificar permissões de segurança no nível da instância. Você deve criar armazenamentos separados de instância e mapear grupos/usuários diferentes para ter acesso aos armazenamentos diferentes.
