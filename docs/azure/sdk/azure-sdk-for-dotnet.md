---
title: Visão geral do SDK do Azure para .NET
description: Fornece uma visão geral do que é o SDK do Azure para .NET e as etapas básicas para usar o SDK em um aplicativo .NET
ms.date: 11/30/2020
ms.custom: devx-track-dotnet
ms.author: daberry
author: daberry
ms.openlocfilehash: b547e105b13d380ffae049ab55e76aa25abe8cc3
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189194"
---
# <a name="azure-sdk-for-net-overview"></a>Visão geral do SDK do Azure para .NET

## <a name="what-is-the-azure-sdk-for-net"></a>O que é o SDK do Azure para .NET

O **SDK do Azure para .net** foi projetado para facilitar o uso dos serviços do Azure de seus aplicativos .net.  Se estiver carregando e baixando arquivos no armazenamento de BLOBs, recuperando os segredos do aplicativo de Azure Key Vault ou processando notificações de hubs de eventos do Azure, o SDK do Azure para .NET fornece uma interface consistente e familiar para acessar os serviços do Azure.  

O SDK do Azure para .NET está disponível como uma série de pacotes NuGet que podem ser usados em aplicativos .NET Core (2,1 e superior) e .NET Framework (4.6.1 e superior).

![Diagrama mostrando como os aplicativos .NET usam o SDK do Azure para acessar os serviços do Azure](./media/azure-sdk-for-dotnet-overview.png)

## <a name="use-the-azure-sdk-for-net-in-your-applications"></a>Usar o SDK do Azure para .NET em seus aplicativos

Para usar um pacote do SDK do Azure em um de seus aplicativos .NET, você deve seguir estas etapas.

1. **Localize o pacote SDK apropriado-** Use a [lista pacote](../packages.md) para localizar o pacote apropriado para o serviço do Azure com o qual você está trabalhando.  É recomendável que a maioria dos serviços tenha um pacote de cliente para trabalhar com o serviço e um pacote de gerenciamento para criar e gerenciar instâncias do serviço.  Na maioria dos casos, você desejará o pacote do cliente.  Instale este pacote em seu aplicativo usando o NuGet.

2. **Configurar a autenticação para seu aplicativo-** Para acessar os recursos do Azure, seu aplicativo precisará ter as credenciais apropriadas e os direitos de acesso atribuídos no Azure.  Saiba como configurar a autenticação na [autenticação de aplicativos .net para o Azure](../authentication.md).

3. **Escrever código usando o SDK em seu aplicativo-** Ao trabalhar com os serviços do Azure, seu código criará primeiro um objeto de cliente para trabalhar com o serviço e, em seguida, chamará métodos nesse objeto de cliente para interagir com o serviço.  Os métodos síncrono e assíncrono são fornecidos.  Os exemplos de uso de cada pacote do SDK individual são fornecidos em toda a documentação do Azure.

4. **Configurar o registro em log para o SDK (opcional)-** Se precisar diagnosticar problemas entre seu aplicativo e o Azure, você poderá [habilitar o registro em log no SDK do Azure para .net](../logging.md).
