---
description: 'Saiba mais sobre: como personalizar feeds com o provedor de Entity Framework (WCF Data Services)'
title: 'Como: Personalizar feeds com o provedor de Entity Framework (WCF Data Services)'
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, customizing
- WCF Data Services, customizing feeds
ms.assetid: fd16272e-36f2-415e-850e-8a81f2b17525
ms.openlocfilehash: b2d2432065ee0982822d0f332744f988d80add12
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765666"
---
# <a name="how-to-customize-feeds-with-the-entity-framework-provider-wcf-data-services"></a>Como: Personalizar feeds com o provedor de Entity Framework (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services permite que você personalize a serialização Atom em uma resposta do serviço de dados para que as propriedades de uma entidade possam ser mapeadas para elementos não utilizados que são definidos no protocolo AtomPub. Este tópico mostra como definir atributos de mapeamento para os tipos de entidade em um modelo de dados que é definido em um arquivo. edmx usando o provedor de Entity Framework. Para obter mais informações, consulte [personalização de feed](feed-customization-wcf-data-services.md).  
  
 Neste tópico, você modificará manualmente o arquivo. edmx gerado por ferramenta que contém o modelo de dados. Você deve modificar manualmente o arquivo, pois as extensões para o modelo de dados não são suportadas pelo Entity Designer. Para obter mais informações sobre o arquivo. edmx que as ferramentas de Modelo de Dados de Entidade geram, consulte [visão geral do arquivo. edmx (Entity Framework)](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)). O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
### <a name="to-manually-modify-the-northwindedmx-file-to-add-feed-customization-attributes"></a>Para modificar manualmente o arquivo Northwind. edmx para adicionar atributos de personalização do feed  
  
1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no `Northwind.edmx` arquivo e clique em **abrir com**.  
  
2. Na caixa de diálogo **abrir com-Northwind. edmx** , selecione **Editor de XML** e clique em **OK**.  
  
3. Localize o `ConceptualModels` elemento e substitua o `Customers` tipo de entidade existente pelo seguinte elemento que contém os atributos de mapeamento de personalização do feed:  
  
     [!code-xml[Astoria Custom Feeds#EdmFeedCustomers](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/northwind.csdl#edmfeedcustomers)]  
  
4. Salve as alterações e feche o arquivo Northwind. edmx.  
  
5. Adicional Clique com o botão direito do mouse no arquivo Northwind. edmx e clique em **executar ferramenta personalizada**.  
  
     Isso regenera o arquivo de camada de objeto, que pode ser necessário.  
  
6. Recompile o projeto.  
  
## <a name="example"></a>Exemplo  

 O exemplo anterior retorna o seguinte resultado para o URI `http://myservice/Northwind.svc/Customers('ALFKI')` .  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/edmfeedresult.xml#edmfeedresult)]  
  
## <a name="see-also"></a>Consulte também

- [Provedor de Entity Framework](entity-framework-provider-wcf-data-services.md)
