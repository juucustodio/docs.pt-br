---
title: 'Tutorial: introdução aos aplicativos Windows Communication Foundation'
description: Esses tutoriais fornecem uma introdução para a criação de aplicativos WCF.
ms.date: 01/25/2019
helpviewer_keywords:
- WCF [WCF], get started
- Windows Communication Foundation [WCF], get started
- get started [WCF]
ms.assetid: df939177-73cb-4440-bd95-092a421516a1
ms.openlocfilehash: 620a83260f01e27a19b19227165695a621c88e5e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96238230"
---
# <a name="tutorial-get-started-with-windows-communication-foundation-applications"></a>Tutorial: introdução aos aplicativos Windows Communication Foundation

A série de tutoriais a seguir apresenta a experiência de programação do Windows Communication Foundation (WCF). Trabalhar com esses tutoriais em ordem fornecerá uma compreensão introdutória das etapas necessárias para criar aplicativos WCF. Depois de concluir, você terá um serviço WCF em execução e um cliente WCF que chama o serviço.

O tutorial pressupõe que você esteja usando o Visual Studio como o ambiente de desenvolvimento. Se você estiver usando outro ambiente de desenvolvimento, ignore as instruções específicas do Visual Studio.

Para aplicativos WCF de exemplo que você pode baixar e executar, consulte [exemplos de Windows Communication Foundation](samples/index.md). Para obter uma introdução aos exemplos, consulte [exemplo de introdução](samples/getting-started-sample.md).

Para obter informações mais detalhadas sobre a criação de serviços e clientes, consulte [programação básica do WCF](basic-wcf-programming.md).

## <a name="wcf-tutorials"></a>Tutoriais do WCF

Os três primeiros tutoriais descrevem como definir um contrato de serviço do WCF, como implementá-lo e como hospedá-lo. O serviço que você cria é hospedado internamente em um aplicativo de console. Você também pode hospedar serviços no Microsoft Serviços de Informações da Internet (IIS). Para obter mais informações, consulte [como hospedar um serviço WCF no IIS](feature-details/how-to-host-a-wcf-service-in-iis.md). Embora você use código para configurar o serviço no tutorial, você também pode [Configurar serviços em um arquivo de configuração](configuring-services-using-configuration-files.md).

- [Tutorial: definir um contrato de serviço](how-to-define-a-wcf-service-contract.md)

    Você cria um contrato do WCF com uma interface definida pelo usuário. Este contrato define a funcionalidade que o serviço expõe.

- [Tutorial: implementar um contrato de serviço](how-to-implement-a-wcf-contract.md)

    Depois de definir um contrato, você deve implementá-lo com uma classe de serviço.

- [Tutorial: hospedar e executar um serviço básico](how-to-host-and-run-a-basic-wcf-service.md)

    Configure um ponto de extremidade para o serviço e hospede o serviço em um aplicativo de console. Para que um serviço se torne ativo, você deve configurá-lo e hospedá-lo em um ambiente de tempo de execução. Esse ambiente de tempo de execução cria o serviço e controla seu contexto e seu tempo de vida.

Os próximos dois tutoriais descrevem como criar, configurar e usar um aplicativo cliente para chamar as operações que o serviço expõe. Os serviços publicam metadados que definem as informações que um aplicativo cliente precisa para se comunicar com o serviço. O Visual Studio automatiza o processo de acessar esses metadados e o utiliza para construir o aplicativo cliente para o serviço. Se você decidir não usar o Visual Studio, poderá usar a [ferramenta de utilitário de metadados ServiceModel (*Svcutil.exe*)](servicemodel-metadata-utility-tool-svcutil-exe.md) em vez disso.

- [Tutorial: criar um cliente](how-to-create-a-wcf-client.md)

    Recuperar metadados para criar um proxy de cliente WCF de um serviço WCF. Você recupera metadados usando o Visual Studio para adicionar uma referência de serviço ou pode usar a ferramenta de utilitário de metadados ServiceModel. Você especifica o ponto de extremidade que o cliente usa para acessar o serviço.

- [Tutorial: usar um cliente](how-to-use-a-wcf-client.md)

    Use o proxy do cliente WCF para chamar as operações de serviço.

## <a name="reference"></a>Referência

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>

## <a name="see-also"></a>Veja também

- [Visão geral conceitual](conceptual-overview.md)
- [Guia da documentação](guide-to-the-documentation.md)
- [O que é Windows Communication Foundation](whats-wcf.md)
- [Detalhes de recursos do WCF](feature-details/index.md)
- [Ciclo de vida da programação básica](basic-programming-lifecycle.md)
- [Criando clientes](building-clients.md)
- [Programação básica do WCF](basic-wcf-programming.md)
- [Como: criar um contrato duplex](feature-details/how-to-create-a-duplex-contract.md)
- [Como acessar serviços com um contrato duplex](feature-details/how-to-access-services-with-a-duplex-contract.md)
- [Ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md)
- [Como: usar Svcutil.exe para baixar documentos de metadados](feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)
- [Como: publicar metadados para um serviço usando um arquivo de configuração](feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)
- [Usando associações para configurar serviços e clientes](using-bindings-to-configure-services-and-clients.md)
- [Exemplo de introdução](samples/getting-started-sample.md)
- [Exemplos de Windows Communication Foundation](samples/index.md)
- [Self-Host](samples/self-host.md)
