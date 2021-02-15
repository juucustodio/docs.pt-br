---
title: Configuração centralizada
description: Centralizando a configuração para aplicativos nativos de nuvem usando o Azure App Configuration e o cofre AzureKey.
ms.date: 01/19/2021
ms.openlocfilehash: 770c0c19a6de01250c59a586badb6a4afa2e9ae5
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505707"
---
# <a name="centralized-configuration"></a>Configuração centralizada

Ao contrário de um aplicativo monolítico no qual tudo é executado em uma única instância, um aplicativo nativo de nuvem consiste em serviços independentes distribuídos entre máquinas virtuais, contêineres e regiões geográficas. O gerenciamento de definições de configuração para dezenas de serviços interdependentes pode ser desafiador. Cópias duplicadas de definições de configuração em locais diferentes são propensas a erros e são difíceis de gerenciar. A configuração centralizada é um requisito crítico para aplicativos nativos de nuvem distribuída.

Conforme discutido no [capítulo 1](introduction.md), as recomendações de aplicativo Twelve-Factor exigem uma separação estrita entre código e configuração. A configuração deve ser armazenada externamente do aplicativo e de leitura, conforme necessário. O armazenamento de valores de configuração como constantes ou valores literais no código é uma violação. Os mesmos valores de configuração geralmente são usados por muitos serviços no mesmo aplicativo. Além disso, devemos dar suporte aos mesmos valores em vários ambientes, como desenvolvimento, teste e produção. A prática recomendada é armazená-los em um repositório de configurações centralizado.

A nuvem do Azure apresenta várias ótimas opções.

## <a name="azure-app-configuration"></a>Configuração de Aplicativo do Azure

A [configuração de Azure app](/azure/azure-app-configuration/overview) é um serviço do Azure totalmente gerenciado que armazena definições de configuração não secretas em um local seguro e centralizado. Os valores armazenados podem ser compartilhados entre vários serviços e aplicativos.

O serviço é simples de usar e fornece vários benefícios:

- Representações e mapeamentos flexíveis de chave/valor
- Marcação com rótulos do Azure
- Interface do usuário dedicada para gerenciamento
- Criptografia de informações confidenciais
- Consulta e recuperação em lote

Azure App configuração mantém as alterações feitas nas configurações de valor de chave por sete dias. O recurso de instantâneo point-in-time permite reconstruir o histórico de uma configuração e até mesmo reverter para uma implantação com falha.

A configuração de aplicativo armazena em cache automaticamente cada configuração para evitar chamadas excessivas para o repositório de configuração. A operação de atualização aguarda até o valor em cache de uma configuração expirar para atualizar essa configuração, mesmo quando o valor é alterado no repositório de configurações. O tempo de término de cache padrão é de 30 segundos. Você pode substituir o tempo de expiração.

A configuração de aplicativo criptografa todos os valores de configuração em trânsito e em repouso. Nomes de chave e rótulos são usados como índices para recuperar dados de configuração e não são criptografados.

Embora a configuração de aplicativo forneça segurança protegida, Azure Key Vault ainda é o melhor lugar para armazenar os segredos do aplicativo. O Key Vault fornece criptografia no nível de hardware, políticas de acesso granulares e operações de gerenciamento, como a rotação de certificado. Você pode criar valores de configuração de aplicativo que fazem referência a segredos armazenados em um Key Vault.

## <a name="azure-key-vault"></a>Cofre de Chave do Azure

Key Vault é um serviço gerenciado para armazenar e acessar segredos com segurança. Um segredo é tudo a que você deseja controlar rigorosamente o acesso, como certificados, senhas ou chaves de API. Um cofre é um grupo lógico de segredos.

O Key Vault reduz consideravelmente a probabilidade de os segredos serem vazados acidentalmente. Ao usar o Key Vault, os desenvolvedores de aplicativos não precisam mais armazenar informações de segurança no aplicativo. Essa prática elimina a necessidade de armazenar essas informações dentro do seu código. Por exemplo, um aplicativo pode precisar se conectar a um banco de dados. Em vez de armazenar a cadeia de conexão no código do aplicativo, armazene-o com segurança no Key Vault.

Os aplicativos podem acessar com segurança as informações necessárias usando URIs. Esses URIs permitem que os aplicativos recuperem versões específicas de um segredo. Não há necessidade de escrever código personalizado para proteger qualquer informação secreta armazenada no Key Vault.

O acesso a Key Vault requer autenticação e autorização apropriadas de chamador. Normalmente, cada microserviço nativo de nuvem usa uma combinação ClientId/ClientSecret. É importante manter essas credenciais fora do controle do código-fonte. Uma prática recomendada é defini-los no ambiente do aplicativo. O acesso direto a Key Vault do AKS pode ser obtido usando [Key Vault FlexVolume](https://github.com/Azure/kubernetes-keyvault-flexvol).

## <a name="configuration-in-eshop"></a>Configuração no eShop

O aplicativo eShopOnContainers inclui arquivos de configurações de aplicativo local com cada microserviço. Esses arquivos são verificados no controle do código-fonte, mas não incluem segredos de produção, como cadeias de conexão ou chaves de API. Em produção, as configurações individuais podem ser substituídas por variáveis de ambiente por serviço. Injetar segredos em variáveis de ambiente é uma prática comum para aplicativos hospedados, mas não fornece um repositório de configuração central. Para dar suporte ao gerenciamento centralizado de definições de configuração, cada microserviço inclui uma configuração para alternar entre o uso de configurações locais ou configurações de Azure Key Vault.

## <a name="references"></a>Referências

- [A arquitetura eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Architecture)
- [Orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade](../microservices/architect-microservice-container-applications/scalable-available-multi-container-microservice-applications.md)
- [Gerenciamento de API do Azure](/azure/api-management/api-management-key-concepts)
- [Visão geral do banco de dados SQL do Azure](/azure/sql-database/sql-database-technical-overview)
- [Cache Redis do Azure](https://azure.microsoft.com/services/cache/)
- [API do Azure Cosmos DB para MongoDB](/azure/cosmos-db/mongodb-introduction)
- [Barramento de Serviço do Azure](/azure/service-bus-messaging/service-bus-messaging-overview)
- [Visão geral do Azure Monitor](/azure/azure-monitor/overview)
- [eShopOnContainers: criar cluster kubernetes no AKS](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Deploy-to-Azure-Kubernetes-Service-(AKS)#create-kubernetes-cluster-in-aks)
- [eShopOnContainers: Azure Dev Spaces](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Azure-Dev-Spaces)
- [Azure Dev Spaces](/azure/dev-spaces/about)

>[!div class="step-by-step"]
>[Anterior](deploy-eshoponcontainers-azure.md) 
> [Avançar](scale-applications.md)
