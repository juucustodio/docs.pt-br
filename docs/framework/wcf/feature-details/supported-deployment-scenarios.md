---
description: 'Saiba mais sobre: cenários de implantação com suporte'
title: Cenários de implantação com suporte
ms.date: 03/30/2017
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
ms.openlocfilehash: 090f0912660fc113bad8640afb1360b64071fa78
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793357"
---
# <a name="supported-deployment-scenarios"></a>Cenários de implantação com suporte

O subconjunto de recursos de Windows Communication Foundation (WCF) com suporte para uso em aplicativos parcialmente confiáveis foi projetado para atender aos requisitos de alguns cenários, mas não todos, para usar o WCF. No servidor, o WCF atende aos requisitos de provedores de hospedagem compartilhada de escala da Internet que executam aplicativos de terceiros no conjunto de permissão de confiança média ASP.NET 2,0 por motivos de segurança. No cliente, o suporte à confiança parcial do WCF foi projetado para atender aos requisitos de tecnologias de implantação, como a [implantação do ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment) ou a tecnologia de aplicativo de navegador XAML do WPF, que permite a implantação direta e segura de aplicativos da área de trabalho de sites não confiáveis.

## <a name="minimum-permission-requirements"></a>Requisitos mínimos de permissão

O WCF dá suporte a um subconjunto de recursos em aplicativos em execução em qualquer um dos seguintes conjuntos de permissões nomeados padrão:

- Permissões de confiança média

- Permissões de zona da Internet

A tentativa de usar o WCF em aplicativos parcialmente confiáveis com permissões mais restritivas pode resultar em exceções de segurança em tempo de execução.

Para obter mais informações sobre os recursos com suporte nesses conjuntos de permissões, consulte [compatibilidade parcial de recursos de confiança](partial-trust-feature-compatibility.md).

## <a name="partial-trust-on-the-server"></a>Confiança parcial no servidor

Muitos provedores comerciais de serviços de Hospedagem de aplicativos Web ASP.NET exigem que os aplicativos executados em seus servidores sejam executados no conjunto de permissões de confiança média do ASP.NET 2,0. Os serviços WCF podem ser executados nesses ambientes, desde que usem o <xref:System.ServiceModel.BasicHttpBinding> , o <xref:System.ServiceModel.WebHttpBinding> ou o <xref:System.ServiceModel.WSHttpBinding> com segurança em nível de transporte.

Os serviços WCF em execução em ambientes de Hospedagem de confiança média também podem atuar como serviços de camada intermediária enviando mensagens para outros servidores em resposta às solicitações do cliente. Os cenários de camada intermediária no servidor terão suporte se o ambiente de hospedagem tiver concedido ao aplicativo o apropriado <xref:System.Net.WebPermission> para fazer solicitações de saída para o servidor desejado.

Além das mensagens SOAP usando uma das associações SOAP com suporte, o WCF dá suporte ao <xref:System.ServiceModel.WebHttpBinding> para a criação de serviços de estilo da Web em aplicativos parcialmente confiáveis. O [modelo de programação Web http do WCF](wcf-web-http-programming-model.md), a [agregação do WCF](wcf-syndication.md)e os recursos de [suporte JSON e integração Ajax](ajax-integration-and-json-support.md) do WCF são todos compatíveis com confiança parcial.

Os serviços de fluxo de trabalho exigem permissões de confiança total e não podem ser usados em aplicativos parcialmente confiáveis.

Para obter mais informações, consulte [como: usar a confiança média no ASP.NET 2,0](/previous-versions/msp-n-p/ff648344(v=pandp.10)).

## <a name="partial-trust-on-the-client"></a>Confiança parcial no cliente

Algumas precauções de segurança devem ser tomadas durante o download e a execução de código de sites não confiáveis da Internet. A [implantação do ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment) e a tecnologia XBAP (aplicativo de navegador XAML) do WPF fazem uso de confiança parcial para conceder permissões limitadas (zona da Internet) a código não confiável.

O WCF pode ser usado para se comunicar com servidores remotos de dentro de aplicativos parcialmente confiáveis implantados pela [implantação do ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment) ou XBAP. O conjunto de permissões de zona da Internet inclui <xref:System.Net.WebPermission> para o host de origem, que permite que esses aplicativos se comuniquem com seu servidor de origem usando qualquer uma das associações do WCF com suporte descritas em [compatibilidade parcial do recurso de confiança](partial-trust-feature-compatibility.md).

## <a name="see-also"></a>Consulte também

- [Segurança de acesso do código](../../misc/code-access-security.md)
- [Visão geral dos aplicativos Windows Presentation Foundation Browser-Hosted](/dotnet/desktop/wpf/app-development/wpf-xaml-browser-applications-overview)
- [Confiança parcial](partial-trust.md)
- [ASP.NET de níveis de confiança e arquivos de política](/previous-versions/wyts434y(v=vs.140))
