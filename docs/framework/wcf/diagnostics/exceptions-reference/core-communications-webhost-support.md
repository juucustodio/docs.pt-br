---
description: 'Saiba mais sobre: comunicações principais: suporte a webhosts'
title: 'Comunicações principais: Suporte de Webhost'
ms.date: 03/30/2017
ms.assetid: 034c501f-96f9-4ef7-9602-3ac21788fd3e
ms.openlocfilehash: c132527caf4d08b7423ff8af9442ca609d4e645f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686512"
---
# <a name="core-communications-webhost-support"></a>Comunicações principais: Suporte de Webhost

Este tópico lista todas as exceções geradas pelo suporte ao webhost.

## <a name="exception-list"></a>Lista de exceções

|Código do recurso|Cadeia de caracteres de recurso|
|-------------------|---------------------|
|Hosting_CompatibilityServiceNotHosted|Esse serviço requer compatibilidade com o ASP.NET. Ele também deve ser hospedado no IIS. Hospede o serviço no IIS com a compatibilidade do ASP.NET ativada no Web.config ou defina a Propriedade AspNetCompatibilityRequirementsAttribute. AspNetCompatibilityRequirementsMode com um valor diferente de required.|
|Hosting_ListenerNotFoundForActivationInRecycling|Nenhum canal está ouvindo ativamente no endereço especificado. Se um aplicativo estiver sendo reciclado, o serviço será fechado.|
|Hosting_NonHTTPInCompatibilityMode|Os únicos protocolos com suporte na compatibilidade de ASP.NET são HTTP e HTTPS. Remova o ponto de extremidade especificado ou desabilite a compatibilidade de ASP.NET para o aplicativo.|
|Hosting_ProcessNotExecutingUnderHostedContext|O processo de hospedagem especificado não pode ser invocado no ambiente de hospedagem atual. Essa API requer que o aplicativo de chamada seja hospedado no Serviços de Informações da Internet ou no serviço de ativação de processos do Windows.|
|Hosting_ServiceCompatibilityRequire|O serviço não pode ser ativado porque requer compatibilidade de ASP.NET. A compatibilidade do ASP.NET não está habilitada para este aplicativo. Habilite a compatibilidade de ASP.NET no arquivo Web.config ou defina AspNetCompatibilityRequirementsAttribute. AspNetCompatibility.|
