---
description: 'Saiba mais sobre: trabalhando com dados binários (WCF Data Services)'
title: Trabalhando com dados binários (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, binary data
- WCF Data Services, streams
ms.assetid: aeccc45c-d5c5-4671-ad63-a492ac8043ac
ms.openlocfilehash: dfcc5f03376d2f84267d8648acf55fb1aa96e318
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748096"
---
# <a name="working-with-binary-data-wcf-data-services"></a>Trabalhando com dados binários (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

A biblioteca de cliente WCF Data Services permite que você recupere e atualize dados binários de um feed Protocolo Open Data (OData) de uma das seguintes maneiras:

- Como uma propriedade de tipo primitivo de uma entidade. Esse é o método recomendado para trabalhar com objetos de dados binários pequenos que podem ser facilmente carregados na memória. Nesse caso, a propriedade binária é uma propriedade de entidade exposta pelo modelo de dados, e o serviço de dados serializa os dados binários como XML com codificação binária de Base 64 na mensagem de resposta.

- Como um fluxo de recursos binários separado. Esse é o método recomendado para acessar e alterar dados BLOB (objeto binário grande) que podem representar uma fotografia, um vídeo ou qualquer outro tipo de dados codificados binários.

WCF Data Services implementa o streaming de dados binários usando HTTP, conforme definido no OData. Nesse mecanismo, os dados binários são tratados como um recurso de mídia que é separado de uma entidade, mas relativo a uma entidade, que é chamado de uma entrada de link de mídia. Para obter mais informações, consulte [streaming Provider](streaming-provider-wcf-data-services.md).

> [!TIP]
> Para obter um exemplo passo a passo de como criar um aplicativo cliente do Windows Presentation Foundation (WPF) que baixa arquivos de imagem binários de um serviço OData que armazena fotos, consulte o [provedor de streaming do serviços de dados Series-Part 2: acessando um fluxo de recursos de mídia do cliente](/archive/blogs/astoriateam/data-services-streaming-provider-series-part-2-accessing-a-media-resource-stream-from-the-client). Para baixar o código de exemplo para o serviço de dados de foto de transmissão em destaque na postagem do blog, consulte o [exemplo serviço de streaming de dados de fotos](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/Streaming%20Photo%20OData%20Service%20Sample) no github.

## <a name="entity-metadata"></a>Metadados de entidade

Uma entidade que tenha um fluxo de recursos de mídia relacionado é indicada nos metadados do serviço de dados pelo atributo `HasStream` aplicado a um tipo de entidade que é a entrada do link da mídia. No exemplo a seguir, a `PhotoInfo` entidade é uma entrada de link de mídia que tem um recurso de mídia relacionado, indicado pelo `HasStream` atributo.

[!code-xml[Astoria Photo Streaming Service#HasStream](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_photo_streaming_service/xml/photodata.edmx#hasstream)]

Os outros exemplos deste tópico mostram como acessar e alterar o fluxo de recursos de mídia. Para obter um exemplo completo de como consumir um fluxo de recursos de mídia em um aplicativo cliente .NET Framework usando a biblioteca de cliente do WCF Data Services, consulte a postagem [acessando um fluxo de recursos de mídia do cliente](/archive/blogs/astoriateam/data-services-streaming-provider-series-part-2-accessing-a-media-resource-stream-from-the-client).

## <a name="accessing-the-binary-resource-stream"></a>Acessando o fluxo de recursos binários

A biblioteca de cliente do WCF Data Services fornece métodos para acessar fluxos de recursos binários de um serviço de dados baseado em OData. Ao baixar um recurso de mídia, você pode usar o URI do recurso de mídia ou obter um fluxo binário que contém os dados próprios do recurso de mídia. Você também pode carregar dados dos recursos de mídia como um fluxo binário.

> [!TIP]
> Para obter um exemplo passo a passo de como criar um aplicativo cliente do Windows Presentation Foundation (WPF) que baixa arquivos de imagem binários de um serviço OData que armazena fotos, consulte o [provedor de streaming do serviços de dados Series-Part 2: acessando um fluxo de recursos de mídia do cliente](/archive/blogs/astoriateam/data-services-streaming-provider-series-part-2-accessing-a-media-resource-stream-from-the-client). Para baixar o código de exemplo para o serviço de dados de foto de transmissão em destaque na postagem do blog, consulte o [exemplo serviço de streaming de dados de fotos](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/Streaming%20Photo%20OData%20Service%20Sample) no github.

### <a name="getting-the-uri-of-the-binary-stream"></a>Obtendo o URI do fluxo binário

Para recuperar determinados tipos de recursos de mídia, como imagens e outros arquivos de mídia, geralmente é mais fácil usar o URI do recurso de mídia em seu aplicativo do que manipular o próprio fluxo de dados binários. Para obter o URI de um fluxo de recursos associado a uma determinada entrada de link de mídia, você deve chamar o método <xref:System.Data.Services.Client.DataServiceContext.GetReadStreamUri%2A> na instância de <xref:System.Data.Services.Client.DataServiceContext> que está controlando a entidade. O exemplo a seguir mostra como chamar o método <xref:System.Data.Services.Client.DataServiceContext.GetReadStreamUri%2A> para obter o URI de um fluxo de recursos de mídia que é usado para criar uma nova imagem no cliente:

[!code-csharp[Astoria Photo Streaming Client#GetReadStreamUri](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_photo_streaming_client/cs/photowindow.xaml.cs#getreadstreamuri)]
[!code-vb[Astoria Photo Streaming Client#GetReadStreamUri](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_photo_streaming_client/vb/photowindow.xaml.vb#getreadstreamuri)]

### <a name="downloading-the-binary-resource-stream"></a>Baixando o fluxo de recursos binários

Para recuperar um fluxo de recursos binários, você deve chamar o método <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> na instância de <xref:System.Data.Services.Client.DataServiceContext> que está controlando a entrada de link de mídia. Esse método envia uma solicitação ao serviço de dados que retorna um objeto <xref:System.Data.Services.Client.DataServiceStreamResponse>, que tem uma referência ao fluxo que contém o recurso. Use esse método quando o aplicativo exigir o recurso binário como um <xref:System.IO.Stream>. O exemplo a seguir mostra como chamar o método <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> para recuperar um fluxo que é usado para criar uma nova imagem no cliente:

[!code-csharp[Astoria Streaming Client#GetReadStreamClient](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_streaming_client/cs/customerphotowindow.xaml.cs#getreadstreamclient)]
[!code-vb[Astoria Streaming Client#GetReadStreamClient](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_streaming_client/vb/customerphotowindow.xaml.vb#getreadstreamclient)]

> [!NOTE]
> O cabeçalho do comprimento do conteúdo na mensagem de resposta que contém o vapor binário não é definido pelo serviço de dados. Esse valor pode não refletir o comprimento real do fluxo de dados binários.

### <a name="uploading-a-media-resource-as-a-stream"></a>Carregando um recurso de mídia como um fluxo

Para inserir ou atualizar um recurso de mídia, chame o método <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> na instância de <xref:System.Data.Services.Client.DataServiceContext> que está controlando a entidade. Esse método envia uma solicitação para o serviço de dados que contém a leitura dos recursos de mídia do fluxo fornecido. O exemplo a seguir mostra como chamar o método <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> para enviar uma imagem ao serviço de dados:

[!code-csharp[Astoria Photo Streaming Client#SetSaveStream](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_photo_streaming_client/cs/photodetailswindow.xaml.cs#setsavestream)]
[!code-vb[Astoria Photo Streaming Client#SetSaveStream](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_photo_streaming_client/vb/photodetailswindow.xaml.vb#setsavestream)]

Neste exemplo, o método <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> é chamado fornecendo um valor de `true` para o parâmetro `closeStream`. Isso garante que o <xref:System.Data.Services.Client.DataServiceContext> feche o fluxo depois que os dados binários forem carregados no serviço de dados.

> [!NOTE]
> Quando você chama o <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A>, o fluxo não é enviado ao serviço de dados até que <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> seja chamado.

## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
- [Associar dados a controles](binding-data-to-controls-wcf-data-services.md)
