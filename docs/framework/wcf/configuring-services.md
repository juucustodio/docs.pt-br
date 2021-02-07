---
description: 'Saiba mais sobre: Configurando serviços WCF'
title: Configurando serviços WCF
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [WCF]
ms.assetid: beac771e-f28e-4f84-9ff1-ad9251c726d3
ms.openlocfilehash: 1c0df8c7d9b4e2b1a032f02e74db2de4a8de020c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720833"
---
# <a name="configuring-wcf-services"></a>Configurando serviços WCF

Depois de criar e implementar seu contrato de serviço, você estará pronto para configurar seu serviço. É aí que você define e personaliza como o serviço é exposto aos clientes, incluindo a especificação do endereço onde ele pode ser encontrado, o transporte e a codificação de mensagens que ele usa para enviar e receber mensagens e o tipo de segurança que ela exige.  
  
 A configuração conforme usada aqui inclui todas as formas, imperativamente no código ou usando um arquivo de configuração, no qual você pode definir e personalizar os vários aspectos de um serviço, como especificar seus endereços de ponto de extremidade, os transportes usados e seus esquemas de segurança. Na prática, escrever a configuração é uma parte importante da programação de aplicativos WCF.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Configuração simplificada](simplified-configuration.md)  
 A partir do .NET Framework 4, o WCF vem com um novo modelo de configuração padrão que simplifica os requisitos de configuração do WCF. Se você não fornecer nenhuma configuração do WCF para um serviço específico, o tempo de execução configurará automaticamente seu serviço com pontos de extremidade padrão, associações e comportamentos.  
  
 [Configurando serviços usando arquivos de configuração](configuring-services-using-configuration-files.md)  
 Um serviço do Windows Communication Foundation (WCF) é configurável usando a tecnologia de configuração do .NET Framework. Normalmente, os elementos XML são adicionados ao arquivo de Web.config para um site Serviços de Informações da Internet (IIS) que hospeda um serviço WCF. Os elementos permitem que você altere os detalhes, como os endereços de ponto de extremidade (os endereços reais usados para se comunicar com o serviço) em uma base de máquina por máquina.  
  
 [Associações](bindings.md)  
 Além disso, o WCF inclui várias configurações comuns fornecidas pelo sistema na forma de associações que permitem selecionar rapidamente os recursos mais básicos de como um cliente e serviço se comunicam, como os transportes, a segurança e as codificações de mensagens usadas.  
  
 [Pontos de extremidade](endpoints.md)  
 Toda a comunicação com um serviço WCF ocorre por meio dos *pontos de extremidade* do serviço. Os pontos de extremidade contêm o contrato, as informações de configuração especificadas nas associações e os endereços que indicam onde encontrar o serviço ou onde obter informações sobre o serviço.  
  
 [Serviços de segurança](securing-services.md)  
 Usando o WCF e mecanismos de segurança existentes, você pode implementar confidencialidade, integridade, autenticação e autorização em qualquer serviço. Você também pode auditar as falhas e êxitos de segurança.  
  
 [Criando serviços interoperáveis de perfil básico de WS-I 1.1](./creating-ws-i-basic-profile-1-1-interoperable-services.md)  
 Os requisitos para a implantação de um serviço que é interoperável com serviços e clientes em qualquer outra plataforma ou sistema operacional são descritos na especificação WS-I Basic Profile 1,1.  
  
## <a name="reference"></a>Referência  

 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Ciclo de vida de programação básica](basic-programming-lifecycle.md)  
  
 [Serviços de implantação e projeção](designing-and-implementing-services.md)  
  
 [Serviços de hospedagem](hosting-services.md)  
  
 [Compilando clientes](building-clients.md)  
  
 [Introdução à extensibilidade](introduction-to-extensibility.md)  
  
 [Administração e diagnósticos](./diagnostics/index.md)  
  
## <a name="see-also"></a>Consulte também

- [Programação de WCF básica](basic-wcf-programming.md)
- [Visão geral conceitual](conceptual-overview.md)
- [Detalhes de funcionalidades do WCF](./feature-details/index.md)
