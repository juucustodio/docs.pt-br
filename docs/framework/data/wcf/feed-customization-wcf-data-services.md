---
description: 'Saiba mais sobre: personalização do feed (WCF Data Services)'
title: Personalização do feed (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, feeds
- WCF Data Services, Atom protocol
- Atom Publishing Protocol [WCF Data Services]
- WCF Data Services, customizing feeds
ms.assetid: 0d1a39bc-6462-4683-bd7d-e74e0fd28a85
ms.openlocfilehash: 9c9e0ead05c446b293fd728c3720472529a0cf0c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765945"
---
# <a name="feed-customization-wcf-data-services"></a>Personalização do feed (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services usa o Protocolo Open Data (OData) para expor dados como um feed. O OData dá suporte a formatos Atom e JavaScript Object Notation (JSON) para feeds de dados. Quando você usa um Feed Atom, o OData fornece um método padrão para serializar dados, como entidades e relações, em um formato XML que pode ser incluído no corpo da mensagem HTTP. O OData define um mapeamento de propriedade de entidade padrão entre os dados contidos em entidades e elementos Atom. Para obter mais informações, consulte [OData: Atom Format](https://www.odata.org/documentation/odata-version-2-0/atom-format/).  
  
 Você pode ter um cenário de aplicativo que exige que os dados de propriedade retornados pelo serviço de dados sejam serializados de uma maneira personalizada em vez de no formato de feed padrão. Com o OData, você pode personalizar a serialização em um feed de dados para que as propriedades de uma entidade possam ser mapeadas para elementos não utilizados e atributos de uma entrada ou para elementos personalizados de uma entrada no feed.  
  
> [!NOTE]
> A personalização do feed só tem suporte para feeds ATOM. Os feeds personalizados não são retornados quando o formato JSON é solicitado para o feed retornado.  
  
 Com WCF Data Services, você pode definir um mapeamento de propriedade de entidade alternativo para um conteúdo Atom aplicando manualmente os atributos aos tipos de entidade no modelo de dados. O provedor de fonte de dados do serviço de dados determina como você deve aplicar esses atributos.  
  
> [!IMPORTANT]
> Ao definir feeds personalizados, você deve garantir que todas as propriedades de entidade que têm mapeamentos personalizados definidos sejam incluídas na projeção. Quando uma propriedade de entidade mapeada não é incluída na projeção, pode ocorrer perda de dados. Para obter mais informações, consulte [projeções de consulta](query-projections-wcf-data-services.md).  
  
## <a name="customizing-feeds-with-the-entity-framework-provider"></a>Personalizando feeds com o provedor de Entity Framework  

 O modelo de dados usado com o provedor de Entity Framework é representado como XML no arquivo. edmx. Nesse caso, os atributos que definem feeds personalizados são adicionados aos `EntityType` `Property` elementos e que representam tipos de entidade e propriedades no modelo de dados. Esses atributos de personalização do feed não são definidos no [ \[ formato de arquivo de definição de esquema MC-CSDL \] : conceitual](/openspecs/windows_protocols/mc-csdl/c03ad8c3-e8b7-4306-af96-a9e52bb3df12), que é o formato que o provedor de Entity Framework usa para definir o modelo de dados. Portanto, você deve declarar atributos de personalização de feed em um namespace de esquema específico, que é definido como `m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"` . O fragmento XML a seguir mostra os atributos de personalização do feed aplicados aos `Property` elementos do `Products` tipo de entidade que definem as `ProductName` `ReorderLevel` Propriedades, e `UnitsInStock` .  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedAttributes](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/northwind.csdl#edmfeedattributes)]  
  
 Esses atributos produzem o seguinte feed de dados personalizado para o `Products` conjunto de entidades. No feed de dados personalizado, o `ProductName` valor da propriedade é exibido em ambos no `author` elemento e como o `ProductName` elemento Property, e a `UnitsInStock` propriedade é exibida em um elemento personalizado que tem seu próprio namespace exclusivo e com a `ReorderLevel` propriedade como um atributo:  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResultProduct](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/edmfeedresult.xml#edmfeedresultproduct)]  
  
 Para obter mais informações, consulte [como: Personalizar feeds com o provedor de Entity Framework](how-to-customize-feeds-with-ef-provider-wcf-data-services.md).  
  
> [!NOTE]
> Como as extensões para o modelo de dados não são suportadas pelo Entity Designer, você deve modificar manualmente o arquivo XML que contém o modelo de dados. Para obter mais informações sobre o arquivo. edmx gerado pelas ferramentas de Modelo de Dados de Entidade, consulte [visão geral do arquivo. edmx (Entity Framework)](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)).  
  
### <a name="custom-feed-attributes"></a>Atributos de feed personalizados  

 A tabela a seguir mostra os atributos XML que personalizam feeds que você pode adicionar ao CSDL (linguagem de definição de esquema conceitual) que define o modelo de dados. Esses atributos são equivalentes às propriedades do <xref:System.Data.Services.Common.EntityPropertyMappingAttribute> usadas com o provedor de reflexão.  
  
|Nome do atributo|Descrição|  
|--------------------|-----------------|  
|`FC_ContentKind`|Indica o tipo do conteúdo. As palavras-chave a seguir definem tipos de conteúdo de distribuição.<br /><br /> `text:` O valor da propriedade é exibido no feed como texto.<br /><br /> `html:` O valor da propriedade é exibido no feed como HTML.<br /><br /> `xhtml:` O valor da propriedade é exibido no feed como HTML formatado em XML.<br /><br /> Essas palavras-chave são equivalentes aos valores da <xref:System.Data.Services.Common.SyndicationTextContentKind> enumeração usada com o provedor de reflexão.<br /><br /> Não há suporte para esse atributo quando `FC_NsPrefix` os `FC_NsUri` atributos e são usados.<br /><br /> Ao especificar um valor de `xhtml` para o `FC_ContentKind` atributo, você deve garantir que o valor da propriedade contenha XML formatado corretamente. O serviço de dados retorna o valor sem executar nenhuma transformação. Você também deve garantir que todos os prefixos de elemento XML no XML retornado tenham um URI de namespace e um prefixo definidos no feed mapeado.|  
|`FC_KeepInContent`|Indica que o valor da propriedade referenciada deve ser incluído na seção de conteúdo do feed e no local mapeado. Os valores válidos são `true` e `false`. Para tornar o feed resultante compatível com versões anteriores do WCF Data Services, especifique um valor de para certificar-se `true` de que o valor está incluído na seção de conteúdo do feed.|  
|`FC_NsPrefix`|O prefixo do namespace do elemento XML em um mapeamento que não é de distribuição. Esse atributo deve ser usado com o `FC_NsUri` atributo e não pode ser usado com o `FC_ContentKind` atributo.|  
|`FC_NsUri`|O URI do namespace do elemento XML em um mapeamento que não é de distribuição. Esse atributo deve ser usado com o `FC_NsPrefix` atributo e não pode ser usado com o `FC_ContentKind` atributo.|  
|`FC_SourcePath`|O caminho da propriedade da entidade à qual esta regra de mapeamento de feed se aplica. Só há suporte para esse atributo quando ele é usado em um `EntityType` elemento.<br /><br /> A <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A> propriedade não pode referenciar diretamente um tipo complexo. Para tipos complexos, você deve usar uma expressão de caminho na qual os nomes de propriedade são separados por um caractere de barra invertida ( `/` ). Por exemplo, os valores a seguir são permitidos para um tipo de entidade `Person` com uma propriedade de número inteiro `Age` e uma propriedade complexa<br /><br /> `Address`:<br /><br /> `Age`<br /><br /> `Address/Street`<br /><br /> A <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A> propriedade não pode ser definida como um valor que contenha um espaço ou qualquer outro caractere que não seja válido em um nome de propriedade.|  
|`FC_TargetPath`|O nome do elemento de destino do feed resultante para mapear a propriedade. Esse elemento pode ser um elemento definido pela especificação Atom ou um elemento personalizado.<br /><br /> As palavras-chave a seguir são valores de caminho de destino de agregação predefinidos que apontam para um local específico em um feed OData.<br /><br /> `SyndicationAuthorEmail:` O `atom:email` elemento filho do `atom:author` elemento.<br /><br /> `SyndicationAuthorName:` O `atom:name` elemento filho do `atom:author` elemento.<br /><br /> `SyndicationAuthorUri:` O `atom:uri` elemento filho do `atom:author` elemento.<br /><br /> `SyndicationContributorEmail:` O `atom:email` elemento filho do `atom:contributor` elemento.<br /><br /> `SyndicationContributorName:` O `atom:name` elemento filho do `atom:contributor` elemento.<br /><br /> `SyndicationContributorUri:` O `atom:uri` elemento filho do `atom:contributor` elemento.<br /><br /> `SyndicationCustomProperty:` Um elemento Property personalizado. Ao mapear para um elemento personalizado, o destino deve ser uma expressão de caminho na qual os elementos aninhados são separados por uma barra invertida ( `/` ) e os atributos são especificados por um e comercial ( `@` ). No exemplo a seguir, a cadeia de caracteres `UnitsInStock/@ReorderLevel` mapeia um valor de propriedade para um atributo chamado `ReorderLevel` em um elemento filho denominado `UnitsInStock` do elemento de entrada raiz.<br /><br /> `<Property Name="ReorderLevel" Type="Int16"               m:FC_TargetPath="UnitsInStock/@ReorderLevel"               m:FC_NsPrefix="Northwind"               m:FC_NsUri="http://schemas.examples.microsoft.com/dataservices"               m:FC_KeepInContent="false"               />`<br /><br /> Quando o destino for um nome de elemento personalizado, `FC_NsPrefix` os `FC_NsUri` atributos e também deverão ser especificados.<br /><br /> `SyndicationPublished:` O `atom:published` elemento.<br /><br /> `SyndicationRights:` O `atom:rights` elemento.<br /><br /> `SyndicationSummary:` O `atom:summary` elemento.<br /><br /> `SyndicationTitle:` O `atom:title` elemento.<br /><br /> `SyndicationUpdated:` O `atom:updated` elemento.<br /><br /> Essas palavras-chave são equivalentes aos valores da <xref:System.Data.Services.Common.SyndicationItemProperty> enumeração usada com o provedor de reflexão.|  
  
> [!NOTE]
> Os nomes e valores de atributo diferenciam maiúsculas de minúsculas. Os atributos podem ser aplicados ao `EntityType` elemento ou a um ou mais `Property` elementos, mas não a ambos.  
  
## <a name="customizing-feeds-with-the-reflection-provider"></a>Personalizando feeds com o provedor de reflexão  

 Para personalizar feeds para um modelo de dados que foi implementado usando o provedor de reflexão, adicione uma ou mais instâncias do <xref:System.Data.Services.Common.EntityPropertyMappingAttribute> atributo às classes que representam tipos de entidade no modelo de dados. As propriedades da <xref:System.Data.Services.Common.EntityPropertyMappingAttribute> classe correspondem aos atributos de personalização do feed que são descritos na seção anterior. Veja a seguir um exemplo da declaração do `Order` tipo, com o mapeamento de feed personalizado definido para ambas as propriedades.  
  
> [!NOTE]
> O modelo de dados para este exemplo é definido no tópico [como criar um serviço de dados usando o provedor de reflexão](create-a-data-service-using-rp-wcf-data-services.md).  
  
 [!code-csharp[Astoria Custom Feeds#CustomOrderFeed](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_custom_feeds/cs/orderitems.svc.cs#customorderfeed)]
 [!code-vb[Astoria Custom Feeds#CustomOrderFeed](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_custom_feeds/vb/orderitems.svc.vb#customorderfeed)]  
  
 Esses atributos produzem o seguinte feed de dados personalizado para o `Orders` conjunto de entidades. Nesse feed personalizado, o `OrderId` valor da propriedade é exibido somente no `title` elemento do `entry` e o valor da propriedade é `Customer` exibido no `author` elemento e como o elemento de `Customer` Propriedade:  
  
 [!code-xml[Astoria Custom Feeds#IQueryableFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/iqueryablefeedresult.xml#iqueryablefeedresult)]  
  
 Para obter mais informações, consulte [como: Personalizar feeds com o provedor de reflexão](how-to-customize-feeds-with-the-reflection-provider-wcf-data-services.md).  
  
## <a name="customizing-feeds-with-a-custom-data-service-provider"></a>Personalizando feeds com um provedor de serviços de dados personalizado  

 A personalização do feed para um modelo de dados definido usando um provedor de serviço de dados personalizado é definida para um tipo de recurso chamando o <xref:System.Data.Services.Providers.ResourceType.AddEntityPropertyMappingAttribute%2A> no <xref:System.Data.Services.Providers.ResourceType> que representa um tipo de entidade no modelo de dados. Para obter mais informações, consulte [provedores de serviço de dados personalizados](custom-data-service-providers-wcf-data-services.md).  
  
## <a name="consuming-custom-feeds"></a>Consumindo feeds personalizados  

 Quando o aplicativo consome diretamente um feed OData, ele deve ser capaz de processar quaisquer elementos e atributos personalizados no feed retornado. Quando você implementou feeds personalizados em seu modelo de dados, independentemente do provedor de serviços de dados, o `$metadata` ponto de extremidade retorna informações de feed personalizadas como atributos de feed personalizados no CSDL retornado pelo serviço de dados. Quando você usa a caixa de diálogo **Adicionar referência de serviço** ou a ferramenta [datasvcutil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) para gerar classes de serviço de dados do cliente, os atributos de feed personalizados são usados para garantir que as solicitações e respostas para o serviço de dados sejam manipuladas corretamente.  
  
## <a name="feed-customization-considerations"></a>Considerações de personalização do feed  

 Você deve considerar o seguinte ao definir mapeamentos de feed personalizados.  
  
- O cliente WCF Data Services trata os elementos mapeados em um feed como vazios quando contêm apenas espaços em branco. Por isso, os elementos mapeados que contêm apenas espaços em branco não são materializados no cliente com o mesmo espaço em branco. Para preservar esse espaço em branco no cliente, você deve definir o valor de `KeepInContext` como `true` no atributo de mapeamento de feed.  
  
## <a name="versioning-requirements"></a>Requisitos de controle de versão  

 A personalização do feed tem os seguintes requisitos de controle de versão do protocolo OData:  
  
- A personalização do feed requer que o cliente e o serviço de dados ofereçam suporte à versão 2,0 do protocolo OData e versões posteriores.  
  
 Para obter mais informações, consulte [controle de versão do serviço de dados](data-service-versioning-wcf-data-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Provedor de reflexão](reflection-provider-wcf-data-services.md)
- [Provedor de Entity Framework](entity-framework-provider-wcf-data-services.md)
