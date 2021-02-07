---
description: 'Saiba mais sobre: como usar a ferramenta de configuração do modelo de serviço COM+'
title: 'Como: usar a ferramenta de configuração do modelo de serviço COM+'
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], using service model configuration tool
ms.assetid: 7e68cd8d-5fda-4641-b92f-290db874376e
ms.openlocfilehash: 2047604f327cd871629bbdac403e9acd816bbdb1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734081"
---
# <a name="how-to-use-the-com-service-model-configuration-tool"></a>Como: usar a ferramenta de configuração do modelo de serviço COM+

Depois que você tiver selecionado um modo de hospedagem apropriado, use a ferramenta de linha de comando Configuração de Modelo de Serviço COM+ (ComSvcConfig.exe) para configurar as interfaces de aplicativo que serão expostas como serviços Web.

> [!NOTE]
> Você deve ser administrador no computador para executar as tarefas a seguir.

 Ao usar ComSvcConfig.exe em um computador com Windows 7 para configurar um serviço Web para usar a versão mais recente do modelo de serviço (atualmente v4.5), execute as seguintes etapas:

1. Defina a chave do registro  `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` como um valor DWORD de 0x00000001

2. Executar comsvcconfig.exe

3. Reverter a chave do Registro adicionada na etapa 1 de volta para o seu valor original, ou excluí-la se não existia.

> [!IMPORTANT]
> Reverter essa chave de Registro é importante. Essa é uma chave de compatibilidade. Não reverter essa alteração pode causar problemas com outros aplicativos .NET que são executados no computador).

> [!WARNING]
> Ao usar o ComSvcConfig.exe/install em um computador com Windows 8, uma caixa de diálogo é exibida informando que "um aplicativo em seu computador precisa do seguinte recurso do Windows: .NET Framework 3,5 (inclui o .NET 2,0 e o .NET 3,0" se .NET Framework 3,5 não estiver instalado. Essa caixa de diálogo pode ser ignorada. Como alternativa, você pode definir a chave do Registro OnlyUseLatestCLR para um valor DWORD de 0x00000001

## <a name="add-an-interface-using-the-com-hosting-mode"></a>Adicionar uma interface usando o modo de hospedagem COM+

- Execute ComSvcConfig usando as opções `/install` e `/hosting:complus`, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose
    ```

     O comando adiciona a interface `IFinances` do componente `ItemOrders.IFinancial` (do aplicativo OnlineStore COM+) ao conjunto de interfaces que serão expostas como serviços Web. O serviço usa o modo de hospedagem COM+ e, portanto, exige a ativação explícita do aplicativo.

     Embora o caractere curinga asterisco ( \* ) possa ser usado para o componente e a interface, evite usá-lo, pois talvez você queira expor apenas a funcionalidade selecionada como um serviço Web. Se for executado com uma versão futura desse componente, usar o curinga pode sem querer expor interfaces que podem não terem estado presentes quando a sintaxe de configuração foi determinada.

     A opção /verbose instrui a ferramenta para exibir avisos além dos erros.

     O contrato para o serviço exposto conterá todos os métodos da interface `IFinances`.

## <a name="add-specific-methods-from-an-interface-using-the-com-hosting-mode"></a>Adicionar métodos específicos de uma interface usando o modo de hospedagem COM+

- Execute ComSvcConfig usando as opções `/install` e `/hosting:complus` com nomeação explícita dos métodos necessários, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{Credit,Debit} /hosting:complus /verbose
    ```

     O comando só pode adicionar os métodos `Credit` e `Debit` da interface `IFinances` como operações para o contrato de serviço exposto. Todos os outros métodos na interface serão omitidos do contrato e não estarão acessíveis para os clientes de serviço Web.

## <a name="add-an-interface-using-the-web-hosting-mode"></a>Adicionar uma interface usando o modo de hospedagem na Web

- Execute ComSvcConfig usando as opções `/install` e `/hosting:was`, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse /mex /verbose
    ```

     O comando adiciona a interface `IStockLevels` no componente `ItemInventory.Warehouse` (do aplicativo OnlineWarehouse COM+) ao conjunto de interfaces que serão expostas como serviços Web. O serviço Web está hospedado no diretório virtual OnlineWarehouse do IIS em vez de no COM+ e, portanto, o aplicativo é ativado automaticamente conforme o necessário.

     Para usar a configuração no processo hospedada na Web, o aplicativo COM+ deve ser configurado para ser executado como um aplicativo de biblioteca em vez de um aplicativo de servidor usando o console de administração Serviços de Componentes. Os aplicativos configurados como aplicativos de servidores usam o modo hospedado na Web padrão e implicam em um salto de processo para processar cada solicitação.

     A opção `/mex` adiciona um ponto de extremidade de serviço adicional do Metadata Exchange (MEX) que use o mesmo transporte que o ponto de extremidade do serviço do aplicativo para dar suporte aos clientes que querem recuperar uma definição de contrato do serviço.

## <a name="remove-a-web-service-for-a-specified-interface"></a>Remover um serviço Web para uma interface especificada

- Execute ComSvcConfig usando a opção `/uninstall`, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /uninstall /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus
    ```

     O comando remove a interface `IFinances` no componente `ItemOrders.Financial` (do aplicativo OnlineStore COM+).

## <a name="list-currently-exposed-interfaces"></a>Listar interfaces expostas no momento

- Execute ComSvcConfig usando a opção `/list`, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /list
    ```

     O comando lista as interfaces expostas no momento, junto com o endereço de correspondência e os detalhes da associação, no escopo do computador local.

## <a name="list-specific-currently-exposed-interfaces"></a>Listar interfaces expostas específicas no momento

- Execute ComSvcConfig usando a opção `/list`, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /list /application:OnlineStore /hosting:complus
    ```

     O comando lista as interfaces hospedadas no host COM+ expostas no momento, junto com o endereço de correspondência e os detalhes da associação, para o aplicativo OnlineStore COM+ no computador local.

## <a name="display-help-for-options"></a>Exibir a ajuda para opções

- Executar ComSvcConfig usando a opção /?, conforme mostrado no exemplo a seguir.

    ```console
    ComSvcConfig.exe /?
    ```

## <a name="see-also"></a>Consulte também

- [Visão geral da integração com aplicativos COM+](integrating-with-com-plus-applications-overview.md)
