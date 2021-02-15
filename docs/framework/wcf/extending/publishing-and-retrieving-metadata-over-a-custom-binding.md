---
description: 'Saiba mais sobre: publicando e Recuperando metadados em uma associação personalizada'
title: Publicando e recuperando metadados através de uma associação personalizada
ms.date: 03/30/2017
ms.assetid: 904e11b4-d90e-45c6-9ee5-c3472c90008c
ms.openlocfilehash: 26532c3478d8250e9f6ec7dbb9431be5052239b4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644119"
---
# <a name="publishing-and-retrieving-metadata-over-a-custom-binding"></a>Publicando e recuperando metadados através de uma associação personalizada

O <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> fornece suporte para adicionar um ponto de extremidade de metadados a um serviço. Esses pontos de extremidade de metadados podem responder a solicitações HTTP GET em uma URL que tem uma `?wsdl` QueryString e para WS-Transfer solicitações GET, conforme definido na especificação de WS-MetadataExchange (MEX). Os pontos de extremidade MEX implementam o <xref:System.ServiceModel.Description.IMetadataExchange?displayProperty=nameWithType> contrato.  
  
## <a name="publishing-metadata-over-a-custom-binding"></a>Publicando metadados em uma associação personalizada  

 Os pontos de extremidade de metadados de GET de HTTP e de metadados GET de HTTPS são habilitados definindo as <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A?displayProperty=nameWithType> <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A?displayProperty=nameWithType> Propriedades ou como `true` . As associações para esses pontos de extremidade não podem ser configuradas.  
  
 O <xref:System.ServiceModel.Description.IMetadataExchange> contrato, no entanto, pode ser usado com qualquer ponto de extremidade, incluindo aqueles que usam associações personalizadas, porque os <xref:System.ServiceModel.Description.IMetadataExchange> pontos de extremidade são idênticos a qualquer outro ponto final de serviço do Windows Communication Foundation (WCF). Se você souber como modificar a configuração de uma associação fornecida pelo sistema ou souber como configurar uma <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> , poderá configurar uma associação para uso com um <xref:System.ServiceModel.Description.IMetadataExchange> ponto de extremidade.  
  
## <a name="retrieving-metadata-over-a-custom-binding"></a>Recuperando metadados em uma associação personalizada  

 Os metadados podem ser recuperados de pontos de extremidade HTTP Get e HTTPS Get de metadados usando solicitações HTTP GET padrão ou HTTPS.  
  
 Para recuperar metadados de um ponto de extremidade de metadados MEX, você geralmente pode usar uma das associações MEX padrão com suporte pelo WCF. Para obter mais informações, consulte <xref:System.ServiceModel.Description.MetadataExchangeBindings?displayProperty=nameWithType>. O <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> tipo e a ferramenta de Svcutil.exe selecionam automaticamente uma dessas associações de MEX padrão com base no endereço do ponto de extremidade de metadados especificado.  
  
 Se um ponto de extremidade de metadados MEX usar uma associação diferente de uma das associações de MEX padrão, você poderá configurar a associação usada pelo <xref:System.ServiceModel.Description.MetadataExchangeClient> código de uso ou fornecendo uma <xref:System.ServiceModel.Description.IMetadataExchange> configuração de ponto de extremidade do cliente. A ferramenta de Svcutil.exe é carregada automaticamente de seu arquivo de configuração uma <xref:System.ServiceModel.Description.IMetadataExchange> configuração de ponto de extremidade de cliente que tem o mesmo nome que o esquema de URI para o endereço do ponto de extremidade de metadados.  
  
## <a name="security"></a>Segurança  

 Ao publicar metadados em uma associação personalizada, verifique se a associação fornece o suporte de segurança que seus metadados exigem. Por exemplo, para evitar a divulgação de informações e garantir que o cliente tenha o direito de obter os metadados, você pode tornar seus metadados e seu aplicativo mais seguros configurando seu <xref:System.ServiceModel.Description.IMetadataExchange> ponto de extremidade para exigir autenticação e criptografia. O [ponto de extremidade de metadados seguro personalizado](../samples/custom-secure-metadata-endpoint.md) de exemplo demonstra esse cenário.  
  
## <a name="see-also"></a>Consulte também

- [Serviços de segurança](../securing-services.md)
- [WS-MetadataExchange Bindings](ws-metadataexchange-bindings.md)
- [Como: configurar uma associação personalizada do WS-Metadata Exchange](how-to-configure-a-custom-ws-metadata-exchange-binding.md)
- [Como: recuperar metadados através de uma associação não MEX](how-to-retrieve-metadata-over-a-non-mex-binding.md)
