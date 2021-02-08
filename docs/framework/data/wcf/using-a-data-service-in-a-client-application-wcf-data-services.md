---
description: 'Saiba mais sobre: usando um serviço de dados em um aplicativo cliente (WCF Data Services)'
title: Usando um serviço de dados em um aplicativo cliente (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, getting started
ms.assetid: 90872d0c-e989-4490-b3e9-54afb10d33d4
ms.openlocfilehash: f16b927a00aae55a3cb95630fc5d75a1c4c9e238
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791719"
---
# <a name="using-a-data-service-in-a-client-application-wcf-data-services"></a>Usando um serviço de dados em um aplicativo cliente (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Você pode acessar um serviço que expõe um feed Protocolo Open Data (OData) fornecendo um URI para um navegador da Web. O URI fornece o endereço de um recurso e, em seguida, são enviadas a esses endereços mensagens de solicitação para acessar ou alterar os dados subjacentes que o recurso representa. O navegador emite um comando HTTP GET e retorna o recurso solicitado como um feed OData. Para obter mais informações, consulte [acessando o serviço em um navegador da Web](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).  
  
 Embora um navegador da Web possa ser útil para testar se um serviço OData retorna os dados esperados, os serviços OData de produção que permitem que você também crie, atualize e exclua dados são geralmente acessados pelo código do aplicativo ou por linguagens de script em uma página da Web. Este tópico fornece uma visão geral de como acessar feeds OData de um aplicativo cliente.  
  
## <a name="accessing-and-changing-data-using-rest-semantics"></a>Acessando e alterando dados usando a semântica REST  

 O OData ajuda a garantir a interoperabilidade entre serviços que expõem feeds OData e aplicativos que consomem feeds OData. Os aplicativos acessam e alteram dados em um serviço baseado em OData enviando mensagens de solicitação de uma ação HTTP específica e com um URI que resolve um recurso de entidade no qual a ação deve ser executada. Quando os dados de entidade devem ser fornecidos, eles são fornecidos como uma carga especificamente codificada no corpo da mensagem.  
  
### <a name="http-actions"></a>Ações HTTP  

 O OData dá suporte às seguintes ações HTTP para executar operações de criação, leitura, atualização e exclusão nos dados da entidade que o recurso endereçado representa:  
  
- **Http Get** -essa é a ação padrão quando um recurso é acessado de um navegador. Nenhuma carga é fornecida na mensagem de solicitação, e é retornado um método de resposta com uma carga que contém os dados solicitados.  
  
- **Http post** -insere novos dados de entidade no recurso fornecido. Os dados a serem inseridos são fornecidos na carga da mensagem de solicitação. A carga da mensagem de resposta contém os dados da entidade recém-criada. Isso inclui os valores de chave gerados automaticamente. O cabeçalho também contém o URI que direciona o novo recurso de entidade.  
  
- **Http Delete** -exclui os dados de entidade que o recurso especificado representa. Não há uma carga presente nas mensagens de resposta ou solicitação.  
  
- **Http Put** – substitui os dados de entidade existentes no recurso solicitado por novos dados que são fornecidos no conteúdo da mensagem de solicitação.  
  
- **Mesclagem http** -devido a ineficiências na execução de uma exclusão seguida por uma inserção na fonte de dados apenas para alterar os dados da entidade, o OData apresenta uma nova ação de mesclagem http. A carga da mensagem de solicitação contém as propriedades que devem ser alteradas no recurso de entidade direcionado. Como a MESCLAgem HTTP não é definida na especificação HTTP, ela pode exigir processamento adicional para rotear uma solicitação de MESCLAgem HTTP por meio de servidores não cientes de OData.  
  
 Para obter mais informações, consulte [OData: Operations](https://www.odata.org/documentation/odata-version-2-0/operations/).
  
### <a name="payload-formats"></a>Formatos de carga  

 Para uma solicitação HTTP PUT, HTTP POST ou HTTP MERGE, a carga de uma mensagem de solicitação contém os dados de entidade que você envia ao serviço de dados. O conteúdo da carga depende do formato de dados da mensagem. As respostas HTTP a todas as ações, exceto DELETE, também contêm tal carga. O OData dá suporte aos seguintes formatos de carga para acessar e alterar dados com o serviço:  
  
- **Atom** – uma codificação de mensagem baseada em XML que é definida pelo OData como uma extensão para o protocolo de publicação Atom (AtomPub) para habilitar a troca de dados por http para Web feeds, podcasts, wikis e funcionalidade de Internet baseada em XML. Para obter mais informações, consulte [OData: Atom Format](https://www.odata.org/documentation/odata-version-2-0/atom-format/).
  
- **JSON** -JavaScript Object Notation (JSON) é um formato de intercâmbio de dados leve baseado em um subconjunto da linguagem de programação JavaScript. Para obter mais informações, consulte [OData: JSON Format](https://www.odata.org/documentation/odata-version-2-0/json-format/).
  
 O formato de mensagem da carga é solicitado no cabeçalho da mensagem de solicitação HTTP. Para obter mais informações, consulte [OData: Operations](https://www.odata.org/documentation/odata-version-2-0/operations/).
  
## <a name="accessing-and-changing-data-using-client-libraries"></a>Acessando e alterando dados usando bibliotecas de cliente  

 O WCF Data Services inclui bibliotecas de cliente que permitem consumir com mais facilidade um feed OData de aplicativos cliente baseados em .NET Framework e Silverlight. Essas bibliotecas simplificam o envio e o recebimento de mensagens HTTP. Elas também convertem a carga da mensagem em objetos CLR que representam dados de entidade. As bibliotecas de cliente apresentam as duas classes principais <xref:System.Data.Services.Client.DataServiceContext> e <xref:System.Data.Services.Client.DataServiceQuery%601>. Essas classes permitem que você consulte um serviço de dados e depois trabalhe com os dados de entidade retornados como objetos CLR. Para obter mais informações, consulte [WCF Data Services biblioteca de cliente](wcf-data-services-client-library.md) e [WCF Data Services (Silverlight)](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc838234(v=vs.95)).  
  
 Você pode usar a caixa de diálogo **Adicionar referência de serviço** no Visual Studio para adicionar uma referência a um serviço de dados. Essa ferramenta solicita os metadados de serviço de um serviço de dados referenciado e gera o <xref:System.Data.Services.Client.DataServiceContext> que representa um serviço de dados, além de gerar as classes de serviço de dados cliente que representam entidades. Para obter mais informações, consulte [gerando a biblioteca de cliente do serviço de dados](generating-the-data-service-client-library-wcf-data-services.md).  
  
 Há bibliotecas de programação disponíveis que você pode usar para consumir um feed OData em outros tipos de aplicativos cliente. Para obter mais informações sobre o SDK do OData, consulte [SDK do OData – código de exemplo](https://www.odata.org/ecosystem/#sdk).
  
## <a name="see-also"></a>Consulte também

- [Acessar recursos do serviço de dados](accessing-data-service-resources-wcf-data-services.md)
- [Início rápido](quickstart-wcf-data-services.md)
