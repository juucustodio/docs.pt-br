---
title: Controle de versão de serviço
ms.date: 03/30/2017
ms.assetid: 37575ead-d820-4a67-8059-da11a2ab48e2
ms.openlocfilehash: fae0a5eca5737c3d7885cbe6c678678adabbea01
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245338"
---
# <a name="service-versioning"></a>Controle de versão de serviço

Após a implantação inicial e, potencialmente, várias vezes durante o tempo de vida, os serviços (e os pontos de extremidade que eles expõem) talvez precisem ser alterados por vários motivos, como mudanças nas necessidades dos negócios, requisitos de tecnologia da informação ou para resolver outros problemas. Cada alteração introduz uma nova versão do serviço. Este tópico explica como considerar o controle de versão no Windows Communication Foundation (WCF).  
  
## <a name="four-categories-of-service-changes"></a>Quatro categorias de alterações de serviço  

 As alterações nos serviços que podem ser necessárias podem ser classificadas em quatro categorias:  
  
- Alterações de contrato: por exemplo, uma operação pode ser adicionada ou um elemento de dados em uma mensagem pode ser adicionado ou alterado.  
  
- Alterações de endereço: por exemplo, um serviço é movido para um local diferente em que os pontos de extremidade têm novos endereços.  
  
- Alterações de associação: por exemplo, um mecanismo de segurança muda ou suas configurações são alteradas.  
  
- Alterações de implementação: por exemplo, quando uma implementação de método interno é alterada.  
  
 Algumas dessas alterações são chamadas de "quebra" e outras são "não separáveis". Uma alteração será não *quebrada* se todas as mensagens que tiverem sido processadas com êxito na versão anterior forem processadas com êxito na nova versão. Qualquer alteração que não atenda a esse critério é uma alteração *interruptiva*.  
  
## <a name="service-orientation-and-versioning"></a>Orientação do serviço e controle de versão  

 Uma das filosofias da orientação do serviço é que os serviços e os clientes são autônomos (ou independentes). Entre outras coisas, isso implica que os desenvolvedores de serviço não podem pressupor que eles controlam ou sequer conhecem todos os clientes de serviço. Isso elimina a opção de recompilar e reimplantar todos os clientes quando um serviço altera versões. Este tópico pressupõe que o serviço atende a essa filosofia e, portanto, deve ser alterado ou "com controle de versão" independente de seus clientes.  
  
 Nos casos em que uma alteração interruptiva é inesperada e não pode ser evitada, um aplicativo pode optar por ignorar essa filosofia e exigir que os clientes sejam recriados e reimplantados com uma nova versão do serviço.  
  
## <a name="contract-versioning"></a>Controle de versão de contrato  

 Os contratos usados por um cliente não precisam ser iguais aos do contrato usado pelo serviço; Eles precisam apenas ser compatíveis.  
  
 Para contratos de serviço, compatibilidade significa que novas operações expostas pelo serviço podem ser adicionadas, mas as operações existentes não podem ser removidas ou alteradas semanticamente.  
  
 Para contratos de dados, compatibilidade significa que novas definições de tipo de esquema podem ser adicionadas, mas as definições de tipo de esquema existentes não podem ser alteradas de maneiras significativas. As alterações interruptivas podem incluir a remoção de membros de dados ou a alteração do tipo de dados deles de maneira incompatível. Esse recurso permite que o serviço de alguma latitude altere a versão de seus contratos sem quebrar clientes. As próximas duas seções explicam alterações não interruptivas e interruptivas que podem ser feitas em contratos de dados e de serviço do WCF.  
  
## <a name="data-contract-versioning"></a>Controle de versão de contrato de dados  

 Esta seção lida com o controle de versão de dados ao usar as <xref:System.Runtime.Serialization.DataContractSerializer> <xref:System.Runtime.Serialization.DataContractAttribute> classes e.  
  
### <a name="strict-versioning"></a>Controle de versão estrito  

 Em muitos cenários em que a alteração de versões é um problema, o desenvolvedor de serviço não tem controle sobre os clientes e, portanto, não pode fazer suposições sobre como eles reagirão às alterações no XML ou no esquema da mensagem. Nesses casos, você deve garantir que as novas mensagens serão validadas em relação ao esquema antigo, por dois motivos:  
  
- Os clientes antigos foram desenvolvidos com a suposição de que o esquema não será alterado. Eles podem falhar ao processar as mensagens para as quais nunca foram projetadas.  
  
- Os clientes antigos podem executar a validação de esquema real no esquema antigo antes mesmo de tentar processar as mensagens.  
  
 A abordagem recomendada em tais cenários é tratar os contratos de dados existentes como imutáveis e criar novos com nomes qualificados XML exclusivos. O desenvolvedor de serviço então adicionaria novos métodos a um contrato de serviço existente ou criaria um novo contrato de serviço com métodos que usam o novo contrato de dados.  
  
 Geralmente, será o caso de um desenvolvedor de serviços precisar escrever alguma lógica de negócios que deva ser executada em todas as versões de um contrato de dados mais um código comercial específico da versão para cada versão do contrato de dados. O apêndice no final deste tópico explica como as interfaces podem ser usadas para atender a essa necessidade.  
  
### <a name="lax-versioning"></a>Controle de versão LAX  

 Em muitos outros cenários, o desenvolvedor de serviços pode tomar a suposição de que adicionar um novo membro opcional ao contrato de dados não interromperá os clientes existentes. Isso requer que o desenvolvedor de serviço investigue se os clientes existentes não estão executando a validação de esquema e se eles ignoram membros de dados desconhecidos. Nesses cenários, é possível tirar proveito dos recursos de contrato de dados para adicionar novos membros de uma maneira não-separável. O desenvolvedor do serviço pode tomar essa suposição com confiança se os recursos de contrato de dados para controle de versão já foram usados para a primeira versão do serviço.  
  
 WCF, ASP.NET Web Services e muitas outras pilhas de serviço Web dão suporte ao *controle de versão LAX*: ou seja, eles não geram exceções para novos membros de dados desconhecidos em dados recebidos.  
  
 É fácil acreditar erroneamente que a adição de um novo membro não interromperá os clientes existentes. Se você não tiver certeza de que todos os clientes podem lidar com o controle de versão LAX, a recomendação é usar as diretrizes estritas de controle de versão e tratar os contratos de dados como imutáveis.  
  
 Para obter diretrizes detalhadas para versões negligentes e estritas de contratos de dados, consulte [práticas recomendadas: controle de versão de contrato de dados](best-practices-data-contract-versioning.md).  
  
### <a name="distinguishing-between-data-contract-and-net-types"></a>Diferenciando entre os tipos de contrato de dados e .NET  

 Uma classe ou estrutura .NET pode ser projetada como um contrato de dados aplicando o <xref:System.Runtime.Serialization.DataContractAttribute> atributo à classe. O tipo .NET e suas projeções de contrato de dados são duas coisas distintas. É possível ter vários tipos .NET com a mesma projeção de contrato de dados. Essa distinção é especialmente útil para permitir que você altere o tipo .NET mantendo o contrato de dados projetado, mantendo a compatibilidade com os clientes existentes, mesmo no sentido estrito da palavra. Há duas coisas que você deve fazer sempre para manter essa distinção entre o tipo .NET e o contrato de dados:  
  
- Especifique um <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> e <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A> . Você sempre deve especificar o nome e o namespace do contrato de dados para impedir que o nome e o namespace do seu tipo .NET sejam expostos no contrato. Dessa forma, se você decidir posteriormente alterar o namespace .NET ou o nome do tipo, seu contrato de dados permanecerá o mesmo.  
  
- Especifique <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>. Você sempre deve especificar o nome dos seus membros de dados para impedir que o nome do membro do .NET seja exposto no contrato. Dessa forma, se você decidir posteriormente alterar o nome do .NET do membro, seu contrato de dados permanecerá o mesmo.  
  
### <a name="changing-or-removing-members"></a>Alterando ou removendo membros  

 A alteração do nome ou do tipo de dados de um membro ou a remoção de membros de dados é uma alteração interruptiva, mesmo que o uso de um controle de versão flexível seja permitido. Se isso for necessário, crie um novo contrato de dados.  
  
 Se a compatibilidade de serviço for de alta importância, você pode considerar ignorar membros de dados não utilizados em seu código e deixá-los em vigor. Se estiver dividindo um membro de dados em vários membros, você pode considerar deixar o membro existente em vigor como uma propriedade que pode executar a divisão necessária e a reagregação para clientes de nível inferior (clientes que não são atualizados para a versão mais recente).  
  
 Da mesma forma, as alterações no nome ou namespace do contrato de dados são alterações interruptivas.  
  
### <a name="round-trips-of-unknown-data"></a>Round-Trips de dados desconhecidos  

 Em alguns cenários, há a necessidade de "viagem de ida e volta" dados desconhecidos provenientes de membros adicionados em uma nova versão. Por exemplo, um serviço "versionNew" envia dados com alguns membros adicionados recentemente a um cliente "versionOld". O cliente ignora os membros recém-adicionados ao processar a mensagem, mas reenvia os mesmos dados, incluindo os membros adicionados recentemente, de volta ao serviço versionNew. O cenário típico para isso são as atualizações de dados em que os dados são recuperados do serviço, alterados e retornados.  
  
 Para habilitar a ida e volta para um tipo específico, o tipo deve implementar a <xref:System.Runtime.Serialization.IExtensibleDataObject> interface. A interface contém uma propriedade, <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> que retorna o <xref:System.Runtime.Serialization.ExtensionDataObject> tipo. A propriedade é usada para armazenar quaisquer dados de versões futuras do contrato de dados que são desconhecidos para a versão atual. Esses dados são opacos para o cliente, mas quando a instância é serializada, o conteúdo da <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> propriedade é gravado com o restante dos dados dos membros do contrato de dados.  
  
 É recomendável que todos os seus tipos implementem essa interface para acomodar Membros futuros novos e desconhecidos.  
  
### <a name="data-contract-libraries"></a>Bibliotecas de contratos de dados  

 Pode haver bibliotecas de contratos de dados em que um contrato é publicado em um repositório central, e implementadores de serviço e tipo implementam e expõem contratos de dados desse repositório. Nesse caso, quando você publica um contrato de dados no repositório, não tem controle sobre quem cria tipos que o implementam. Portanto, você não pode modificar o contrato depois que ele é publicado, renderizando-o de forma efetiva.  
  
### <a name="when-using-the-xmlserializer"></a>Ao usar o XmlSerializer  

 Os mesmos princípios de controle de versão se aplicam ao usar a <xref:System.Xml.Serialization.XmlSerializer> classe. Quando o controle de versão estrito é necessário, trate os contratos de dados como imutáveis e crie novos contratos de dados com nomes qualificados exclusivos para as novas versões. Quando tiver certeza de que o controle de versão negligente pode ser usado, você pode adicionar novos membros serializáveis em novas versões, mas não alterar ou remover membros existentes.  
  
> [!NOTE]
> O <xref:System.Xml.Serialization.XmlSerializer> usa os <xref:System.Xml.Serialization.XmlAnyElementAttribute> <xref:System.Xml.Serialization.XmlAnyAttributeAttribute> atributos e para dar suporte a ida e volta de dados desconhecidos.  
  
## <a name="message-contract-versioning"></a>Controle de versão do contrato de mensagem  

 As diretrizes para controle de versão de contrato de mensagem são muito semelhantes ao controle de versão de contratos de dados. Se o controle de versão estrito for necessário, você não deverá alterar o corpo da mensagem, mas, em vez disso, criar um novo contrato de mensagem com um nome qualificado exclusivo. Se você sabe que pode usar o controle de versão negligente, você pode adicionar novas partes de corpo de mensagem, mas não alterar ou remover as existentes. Essa orientação se aplica a contratos de mensagem Bare-and-Wrapped.  
  
 Os cabeçalhos de mensagem sempre podem ser adicionados, mesmo se o controle de versão estrito estiver em uso. O sinalizador MustUnderstand pode afetar o controle de versão. Em geral, o modelo de controle de versão para cabeçalhos no WCF é conforme descrito na especificação SOAP.  
  
## <a name="service-contract-versioning"></a>Controle de versão do contrato de serviço  

 Semelhante ao controle de versão de contrato de dados, o controle de versão de contrato de serviço também envolve a adição, alteração e remoção de operações.  
  
### <a name="specifying-name-namespace-and-action"></a>Especificando o nome, o namespace e a ação  

 Por padrão, o nome de um contrato de serviço é o nome da interface. Seu namespace padrão é " http://tempuri.org ", e cada ação de operação é " http://tempuri.org/contractname/methodname ". É recomendável especificar explicitamente um nome e um namespace para o contrato de serviço, e uma ação para cada operação para evitar o uso de " http://tempuri.org " e impedir que os nomes de interface e método sejam expostos no contrato do serviço.  
  
### <a name="adding-parameters-and-operations"></a>Adicionando parâmetros e operações  

 A adição de operações de serviço expostas pelo serviço é uma alteração sem interrupção porque os clientes existentes não precisam se preocupar com essas novas operações.  
  
> [!NOTE]
> A adição de operações a um contrato do retorno de chamada duplex é uma alteração interruptiva.  
  
### <a name="changing-operation-parameter-or-return-types"></a>Alterando o parâmetro de operação ou tipos de retorno  

 A alteração de parâmetros ou tipos de retorno geralmente é uma alteração interruptiva, a menos que o novo tipo implemente o mesmo contrato de dados implementado pelo tipo antigo. Para fazer essa alteração, adicione uma nova operação ao contrato de serviço ou defina um novo contrato de serviço.  
  
### <a name="removing-operations"></a>Removendo operações  

 A remoção de operações também é uma alteração interruptiva. Para fazer essa alteração, defina um novo contrato de serviço e expor-o em um novo ponto de extremidade.  
  
### <a name="fault-contracts"></a>Contratos de falha  

 O <xref:System.ServiceModel.FaultContractAttribute> atributo permite que um desenvolvedor de contrato de serviço Especifique informações sobre as falhas que podem ser retornadas das operações do contrato.  
  
 A lista de falhas descritas no contrato de um serviço não é considerada exaustiva. A qualquer momento, uma operação pode retornar falhas que não estão descritas em seu contrato. Portanto, a alteração do conjunto de falhas descritas no contrato não é considerada uma interrupção. Por exemplo, adicionar uma nova falha ao contrato usando <xref:System.ServiceModel.FaultContractAttribute> ou removendo uma falha existente do contrato.  
  
### <a name="service-contract-libraries"></a>Bibliotecas de contratos de serviço  

 As organizações podem ter bibliotecas de contratos em que um contrato é publicado em um repositório central e implementadores de serviço implementam contratos desse repositório. Nesse caso, quando você publica um contrato de serviço no repositório, não tem controle sobre quem cria serviços que o implementam. Portanto, você não pode modificar o contrato de serviço depois de publicado, renderizando-o efetivamente imutável. O WCF dá suporte à herança de contrato, que pode ser usada para criar um novo contrato que estende os contratos existentes. Para usar esse recurso, defina uma nova interface de contrato de serviço que herda da interface antiga do contrato de serviço e, em seguida, adicione métodos à nova interface. Em seguida, altere o serviço que implementa o contrato antigo para implementar o novo contrato e altere a definição de ponto de extremidade "versionOld" para usar o novo contrato. Para clientes "versionOld", o ponto de extremidade continuará a aparecer como expondo o contrato "versionOld"; para clientes "versionNew", o ponto de extremidade será exibido para expor o contrato "versionNew".  
  
## <a name="address-and-binding-versioning"></a>Controle de versão de endereço e ligação  

 As alterações à associação e ao endereço do ponto de extremidade são alterações interruptivas, a menos que os clientes possam descobrir dinamicamente a nova associação ou o novo endereço do ponto de extremidade. Um mecanismo para implementar esse recurso é usando um registro UDDI (descrição de descoberta universal) e o padrão de invocação de UDDI, em que um cliente tenta se comunicar com um ponto de extremidade e, após a falha, consulta um registro UDDI bem conhecido para os metadados do ponto de extremidade atual. Em seguida, o cliente usa o endereço e a associação desses metadados para se comunicar com o ponto de extremidade. Se essa comunicação for realizada com sucesso, o cliente armazenará em cache o endereço e as informações de associação para uso futuro.  
  
## <a name="routing-service-and-versioning"></a>Serviço de roteamento e controle de versão  

 Se as alterações feitas a um serviço forem alterações interruptivas e você precisar ter duas ou mais versões diferentes de um serviço em execução simultaneamente, você poderá usar o WCF Routing Service para rotear mensagens para a instância de serviço apropriada. O serviço de roteamento do WCF usa o roteamento baseado em conteúdo, em outras palavras, ele usa informações dentro da mensagem para determinar onde rotear a mensagem. Para obter mais informações sobre o serviço de roteamento do WCF, consulte [serviço de roteamento](./feature-details/routing-service.md). Para obter um exemplo de como usar o serviço de roteamento do WCF para controle de versão de serviço, consulte [como: controle de versão de serviço](./feature-details/how-to-service-versioning.md).  
  
## <a name="appendix"></a>Apêndice  

 As diretrizes de controle de versão de contrato de dados gerais quando o controle de versão estrito é necessário é tratar os contratos de dados como imutáveis e criar novos quando forem necessárias alterações. Uma nova classe precisa ser criada para cada novo contrato de dados, portanto, um mecanismo é necessário para evitar a necessidade de usar o código existente que foi escrito em termos da classe antiga de contrato de dados e reescrevê-lo em termos da nova classe de contrato de dados.  
  
 Um desses mecanismos é usar interfaces para definir os membros de cada contrato de dados e escrever o código de implementação interno em termos das interfaces em vez das classes de contrato de dados que implementam as interfaces. O código a seguir para a versão 1 de um serviço mostra uma `IPurchaseOrderV1` interface e um `PurchaseOrderV1` :  
  
```csharp  
public interface IPurchaseOrderV1  
{  
    string OrderId { get; set; }  
    string CustomerId { get; set; }  
}  
  
[DataContract(  
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2005/10/PurchaseOrder")]  
public class PurchaseOrderV1 : IPurchaseOrderV1  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
}  
```  
  
 Embora as operações do contrato de serviço sejam escritas em termos de `PurchaseOrderV1` , a lógica de negócios real seria em termos de `IPurchaseOrderV1` . Em seguida, na versão 2, haveria uma nova `IPurchaseOrderV2` interface e uma nova `PurchaseOrderV2` classe, conforme mostrado no código a seguir:  
  
```csharp
public interface IPurchaseOrderV2  
{  
    DateTime OrderDate { get; set; }  
}

[DataContract(
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2006/02/PurchaseOrder")]  
public class PurchaseOrderV2 : IPurchaseOrderV1, IPurchaseOrderV2  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
    [DataMember(...)]  
    public DateTime OrderDate { ... }  
}  
```  
  
 O contrato de serviço seria atualizado para incluir novas operações que são gravadas em termos de `PurchaseOrderV2` . A lógica de negócios existente escrita em termos de `IPurchaseOrderV1` continuaria a funcionar para `PurchaseOrderV2` e a nova lógica de negócios que precisa da `OrderDate` propriedade seria escrita em termos de `IPurchaseOrderV2` .  
  
## <a name="see-also"></a>Confira também

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>
- <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>
- <xref:System.Runtime.Serialization.IExtensibleDataObject>
- <xref:System.Runtime.Serialization.ExtensionDataObject>
- <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>
- <xref:System.Xml.Serialization.XmlSerializer>
- [Equivalência de contrato de dados](./feature-details/data-contract-equivalence.md)
- [Retornos de chamada de serialização tolerantes à versão](./feature-details/version-tolerant-serialization-callbacks.md)
