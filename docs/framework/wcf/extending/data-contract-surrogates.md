---
description: 'Saiba mais sobre: substitutos de contrato de dados'
title: Substitutos de contrato de dados
ms.date: 03/30/2017
helpviewer_keywords:
- data contracts [WCF], surrogates
ms.assetid: 8c31134c-46c5-4ed7-94af-bab0ac0dfce5
ms.openlocfilehash: 335e7f64868177d00c747e29c463808f3eff3056
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685797"
---
# <a name="data-contract-surrogates"></a>Substitutos de contrato de dados

O *substituto* do contrato de dados é um recurso avançado criado com base no modelo de contrato de dados. Esse recurso foi projetado para ser usado para personalização de tipo e substituição em situações em que os usuários desejam alterar a forma como um tipo é serializado, desserializado ou projetado em metadados. Alguns cenários em que um substituto pode ser usado é quando um contrato de dados não foi especificado para o tipo, os campos e as propriedades não são marcados com o <xref:System.Runtime.Serialization.DataMemberAttribute> atributo ou os usuários desejam criar dinamicamente variações de esquema.  
  
 A serialização e a desserialização são realizadas com o substituto de contrato de dados ao usar <xref:System.Runtime.Serialization.DataContractSerializer> para converter de .NET Framework em um formato adequado, como XML. O substituto de contrato de dados também pode ser usado para modificar os metadados exportados para tipos, ao produzir representações de metadados, como XSD (documentos de esquema XML). Após a importação, o código é criado a partir de metadados e o substituto pode ser usado nesse caso para personalizar o código gerado também.  
  
## <a name="how-the-surrogate-works"></a>Como funciona o substituto  

 Um substituto funciona mapeando um tipo (o tipo "original") para outro tipo (o tipo "substituto"). O exemplo a seguir mostra o tipo original `Inventory` e um novo `InventorySurrogated` tipo de substituto. O `Inventory` tipo não é serializável, mas o `InventorySurrogated` tipo é:  
  
 [!code-csharp[C_IDataContractSurrogate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#1)]  
  
 Como um contrato de dados não foi definido para essa classe, converta a classe em uma classe substituta com um contrato de dados. A classe substituta é mostrada no exemplo a seguir:  
  
 [!code-csharp[C_IDataContractSurrogate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#2)]  
  
## <a name="implementing-the-idatacontractsurrogate"></a>Implementando o IDataContractSurrogate  

 Para usar o substituto de contrato de dados, implemente a <xref:System.Runtime.Serialization.IDataContractSurrogate> interface.  
  
 Veja a seguir uma visão geral de cada método do <xref:System.Runtime.Serialization.IDataContractSurrogate> com uma possível implementação.  
  
### <a name="getdatacontracttype"></a>GetDataContractType  

 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> método mapeia um tipo para outro. Esse método é necessário para serialização, desserialização, importação e exportação.  
  
 A primeira tarefa é definir quais tipos serão mapeados para outros tipos. Por exemplo:  
  
 [!code-csharp[C_IDataContractSurrogate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#3)]  
  
- Na serialização, o mapeamento retornado por esse método é usado posteriormente para transformar a instância original em uma instância substituta chamando o <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> método.  
  
- Na desserialização, o mapeamento retornado por esse método é usado pelo serializador para desserializar em uma instância do tipo substituto. Em seguida, ele chama a <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%2A> transformação da instância substituta em uma instância do tipo original.  
  
- Na exportação, o tipo substituto retornado por esse método é refletido para obter o contrato de dados a ser usado para gerar metadados.  
  
- Na importação, o tipo inicial é alterado para um tipo substituto que é refletido para obter o contrato de dados a ser usado para fins como referência de suporte.  
  
 O <xref:System.Type> parâmetro é o tipo do objeto que está sendo serializado, desserializado, importado ou exportado. O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> método deve retornar o tipo de entrada se o substituto não tratar o tipo. Caso contrário, retorne o tipo alternativo apropriado. Se vários tipos substitutos existirem, vários mapeamentos poderão ser definidos nesse método.  
  
 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> método não é chamado para primitivos de contrato de dados internos, como <xref:System.Int32> ou <xref:System.String> . Para outros tipos, como matrizes, tipos definidos pelo usuário e outras estruturas de dados, esse método será chamado para cada tipo.  
  
 No exemplo anterior, o método verifica se o `type` parâmetro e `Inventory` é comparável. Se for o caso, o método o mapeará para `InventorySurrogated` . Sempre que uma serialização, desserialização, importar esquema ou exportar esquema é chamada, essa função é chamada primeiro para determinar o mapeamento entre os tipos.  
  
### <a name="getobjecttoserialize-method"></a>Método GetObjectToSerialize  

 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> método converte a instância do tipo original na instância do tipo de substituição. O método é necessário para a serialização.  
  
 A próxima etapa é definir a maneira como os dados físicos serão mapeados da instância original para o substituto, implementando o <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> método. Por exemplo:  
  
 [!code-csharp[C_IDataContractSurrogate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#4)]  
  
 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> método é chamado quando um objeto é serializado. Esse método transfere dados do tipo original para os campos do tipo substituto. Os campos podem ser mapeados diretamente para campos substitutos ou as manipulações dos dados originais podem ser armazenadas no substituto. Alguns usos possíveis incluem: mapear diretamente os campos, executar operações nos dados a serem armazenados nos campos substituídos ou armazenar o XML do tipo original no campo substituído.  
  
 O `targetType` parâmetro refere-se ao tipo declarado do membro. Esse parâmetro é o tipo substituto retornado pelo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> método. O serializador não impõe que o objeto retornado seja atribuível a esse tipo. O `obj` parâmetro é o objeto a ser serializado e será convertido em seu substituto, se necessário. Esse método deve retornar o objeto de entrada se o substituto não tratar o objeto. Caso contrário, o novo objeto substituto será retornado. O substituto não será chamado se o objeto for nulo. Vários mapeamentos substitutos para diferentes instâncias podem ser definidos dentro desse método.  
  
 Ao criar um <xref:System.Runtime.Serialization.DataContractSerializer> , você pode instruí-lo para preservar as referências de objeto. (Para obter mais informações, consulte [serialização e desserialização](../feature-details/serialization-and-deserialization.md).) Isso é feito definindo o `preserveObjectReferences` parâmetro em seu construtor como `true` . Nesse caso, o substituto é chamado apenas uma vez para um objeto, já que todas as serializações subsequentes apenas gravam a referência no fluxo. Se `preserveObjectReferences` é definido como `false` , o substituto é chamado toda vez que uma instância é encontrada.  
  
 Se o tipo da instância serializada diferir do tipo declarado, as informações de tipo serão gravadas no fluxo, por exemplo, `xsi:type` para permitir que a instância seja desserializada na outra extremidade. Esse processo ocorre se o objeto é substituído ou não.  
  
 O exemplo acima converte os dados da `Inventory` instância para o de `InventorySurrogated` . Ele verifica o tipo do objeto e executa as manipulações necessárias para converter para o tipo substituto. Nesse caso, os campos da `Inventory` classe são copiados diretamente para os campos de `InventorySurrogated` classe.  
  
### <a name="getdeserializedobject-method"></a>Método GetDeserializedObject  

 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%2A> método converte a instância do tipo substituto para a instância do tipo original. Ele é necessário para desserialização.  
  
 A próxima tarefa é definir a maneira como os dados físicos serão mapeados da instância substituta para o original. Por exemplo:  
  
 [!code-csharp[C_IDataContractSurrogate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#5)]  
  
 Esse método é chamado somente durante a desserialização de um objeto. Ele fornece mapeamento de dados inverso para a desserialização do tipo substituto de volta para seu tipo original. Semelhante ao `GetObjectToSerialize` método, alguns usos possíveis podem ser trocar diretamente os dados de campo, executar operações nos dados e armazenar dados XML. Ao desserializar, nem sempre é possível obter os valores de dados exatos do original devido a manipulações na conversão de dados.  
  
 O `targetType` parâmetro refere-se ao tipo declarado do membro. Esse parâmetro é o tipo substituto retornado pelo `GetDataContractType` método. O `obj` parâmetro refere-se ao objeto que foi desserializado. O objeto pode ser convertido de volta para seu tipo original se ele for substituído. Esse método retornará o objeto de entrada se o substituto não tratar o objeto. Caso contrário, o objeto desserializado será retornado quando sua conversão for concluída. Se houver vários tipos substitutos, você poderá fornecer conversão de dados de substituto para o tipo principal para cada um indicando cada tipo e sua conversão.  
  
 Ao retornar um objeto, as tabelas de objeto interno são atualizadas com o objeto retornado por esse substituto. Todas as referências subsequentes a uma instância obterão a instância substituta das tabelas de objeto.  
  
 O exemplo anterior converte objetos do tipo de `InventorySurrogated` volta para o tipo inicial `Inventory` . Nesse caso, os dados são transferidos diretamente de volta do `InventorySurrogated` para seus campos correspondentes no `Inventory` . Como não há manipulações de dados, cada um dos campos de membro conterá os mesmos valores de antes da serialização.  
  
### <a name="getcustomdatatoexport-method"></a>Método GetCustomDataToExport  

 Ao exportar um esquema, o <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%2A> método é opcional. Ele é usado para inserir dados ou dicas adicionais no esquema exportado. Dados adicionais podem ser inseridos no nível de membro ou nível de tipo. Por exemplo:  
  
 [!code-csharp[C_IDataContractSurrogate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#6)]  
  
 Esse método (com duas sobrecargas) permite a inclusão de informações extras nos metadados no nível de membro ou de tipo. É possível incluir dicas sobre se um membro é público ou privado e comentários que seriam preservados durante a exportação e a importação do esquema. Essas informações seriam perdidas sem esse método. Esse método não causa a inserção ou exclusão de membros ou tipos, mas, em vez disso, adiciona dados adicionais aos esquemas em qualquer um desses níveis.  
  
 O método está sobrecarregado e pode ter um `Type` ( `clrtype` parâmetro) ou <xref:System.Reflection.MemberInfo> ( `memberInfo` parâmetro). O segundo parâmetro é sempre um `Type` ( `dataContractType` parâmetro). Esse método é chamado para cada membro e tipo do `dataContractType` tipo substituto.  
  
 Qualquer uma dessas sobrecargas deve retornar um `null` ou um objeto serializável. Um objeto não nulo será serializado como anotação no esquema exportado. Para a `Type` sobrecarga, cada tipo exportado para o esquema é enviado para esse método no primeiro parâmetro, juntamente com o tipo substituto como o `dataContractType` parâmetro. Para a `MemberInfo` sobrecarga, cada membro exportado para o esquema envia suas informações como o `memberInfo` parâmetro com o tipo substituto no segundo parâmetro.  
  
#### <a name="getcustomdatatoexport-method-type-type"></a>Método GetCustomDataToExport (tipo, tipo)  

 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%28System.Type%2CSystem.Type%29?displayProperty=nameWithType> método é chamado durante a exportação de esquema para cada definição de tipo. O método adiciona informações aos tipos no esquema durante a exportação. Cada tipo definido é enviado para esse método para determinar se há dados adicionais que precisam ser incluídos no esquema.  
  
#### <a name="getcustomdatatoexport-method-memberinfo-type"></a>Método GetCustomDataToExport (MemberInfo, Type)  

 O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=nameWithType> é chamado durante a exportação para cada membro nos tipos exportados. Essa função permite que você personalize todos os comentários para os membros que serão incluídos no esquema após a exportação. As informações para cada membro dentro da classe são enviadas para esse método para verificar se os dados adicionais precisam ser adicionados ao esquema.  
  
 O exemplo acima pesquisa o `dataContractType` para cada membro do substituto. Em seguida, ele retorna o modificador de acesso apropriado para cada campo. Sem essa personalização, o valor padrão para modificadores de acesso é público. Portanto, todos os membros seriam definidos como públicos no código gerado usando o esquema exportado, independentemente de quais são suas restrições de acesso reais. Quando não estiver usando essa implementação, o membro `numpens` seria público no esquema exportado, embora ele tenha sido definido no substituto como particular. Com o uso desse método, no esquema exportado, o modificador de acesso pode ser gerado como particular.  
  
### <a name="getreferencedtypeonimport-method"></a>Método GetReferencedTypeOnImport  

 Esse método mapeia o <xref:System.Type> do substituto para o tipo original. Esse método é opcional para a importação de esquema.  
  
 Ao criar um substituto que importa um esquema e gera código para ele, a próxima tarefa é definir o tipo de uma instância substituta para seu tipo original.  
  
 Se o código gerado precisar fazer referência a um tipo de usuário existente, isso é feito com a implementação do <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%2A> método.  
  
 Ao importar um esquema, esse método é chamado para cada declaração de tipo para mapear o contrato de dados substitutos para um tipo. Os parâmetros de cadeia de caracteres `typeName` e `typeNamespace` definem o nome e o namespace do tipo substituto. O valor de retorno para <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%2A> é usado para determinar se um novo tipo precisa ser gerado. Este método deve retornar um tipo válido ou nulo. Para tipos válidos, o tipo retornado será usado como um tipo referenciado no código gerado. Se NULL for retornado, nenhum tipo será referenciado e um novo tipo deverá ser criado. Se houver vários substitutos, será possível executar o mapeamento para cada tipo substituto de volta para seu tipo inicial.  
  
 O `customData` parâmetro é o objeto retornado originalmente de <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%2A> . Isso `customData` é usado quando os autores substitutos desejam inserir dados/dicas extras nos metadados a serem usados durante a importação para gerar código.  
  
### <a name="processimportedtype-method"></a>Método ProcessImportedType  

 O <xref:System.Runtime.Serialization.IDataContractSurrogate.ProcessImportedType%2A> método personaliza qualquer tipo criado a partir da importação de esquema. Esse método é opcional.  
  
 Ao importar um esquema, esse método permite que qualquer tipo importado e informações de compilação sejam personalizadas. Por exemplo:  
  
 [!code-csharp[C_IDataContractSurrogate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#7)]  
  
 Durante a importação, esse método é chamado para cada tipo gerado. Altere o especificado <xref:System.CodeDom.CodeTypeDeclaration> ou modifique o <xref:System.CodeDom.CodeCompileUnit> . Isso inclui alterar o nome, os membros, os atributos e muitas outras propriedades do `CodeTypeDeclaration` . Ao processar o `CodeCompileUnit` , é possível modificar as diretivas, os namespaces, os assemblies referenciados e vários outros aspectos.  
  
 O `CodeTypeDeclaration` parâmetro contém a declaração de tipo dom de código. O `CodeCompileUnit` parâmetro permite a modificação para o processamento do código.  Retornando `null` resultados na declaração de tipo que está sendo descartada. Por outro lado, ao retornar um `CodeTypeDeclaration` , as modificações são preservadas.  
  
 Se os dados personalizados forem inseridos durante a exportação de metadados, ele precisará ser fornecido ao usuário durante a importação para que possa ser usado. Esses dados personalizados podem ser usados para dicas de modelo de programação ou outros comentários. Cada `CodeTypeDeclaration` <xref:System.CodeDom.CodeTypeMember> instância do e inclui dados personalizados como a <xref:System.CodeDom.CodeObject.UserData%2A> propriedade, convertida para o `IDataContractSurrogate` tipo.  
  
 O exemplo acima executa algumas alterações no esquema importado. O código preserva os membros privados do tipo original usando um substituto. O modificador de acesso padrão ao importar um esquema é `public` . Portanto, todos os membros do esquema substituto serão públicos, a menos que sejam modificados, como neste exemplo. Durante a exportação, os dados personalizados são inseridos nos metadados sobre os quais os membros são privados. O exemplo pesquisa os dados personalizados, verifica se o modificador de acesso é privado e, em seguida, modifica o membro apropriado para ser privado definindo seus atributos. Sem essa personalização, o `numpens` membro seria definido como público em vez de privado.  
  
### <a name="getknowncustomdatatypes-method"></a>Método GetKnownCustomDataTypes  

 Esse método obtém tipos de dados personalizados definidos a partir do esquema. O método é opcional para a importação de esquema.  
  
 O método é chamado no início da exportação e importação de esquema. O método retorna os tipos de dados personalizados usados no esquema exportado ou importado. O método é passado a <xref:System.Collections.ObjectModel.Collection%601> (o `customDataTypes` parâmetro), que é uma coleção de tipos. O método deve adicionar tipos conhecidos adicionais a esta coleção. Os tipos de dados personalizados conhecidos são necessários para habilitar a serialização e a desserialização de dados personalizados usando o <xref:System.Runtime.Serialization.DataContractSerializer> . Para obter mais informações, consulte [tipos conhecidos de contrato de dados](../feature-details/data-contract-known-types.md).  
  
## <a name="implementing-a-surrogate"></a>Implementando um substituto  

 Para usar o substituto de contrato de dados no WCF, você deve seguir alguns procedimentos especiais.  
  
### <a name="to-use-a-surrogate-for-serialization-and-deserialization"></a>Para usar um substituto para serialização e desserialização  

 Use o <xref:System.Runtime.Serialization.DataContractSerializer> para executar a serialização e a desserialização de dados com o substituto. O <xref:System.Runtime.Serialization.DataContractSerializer> é criado pelo <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> . O substituto também deve ser especificado.  
  
##### <a name="to-implement-serialization-and-deserialization"></a>Para implementar a serialização e desserialização  
  
1. Crie uma instância do <xref:System.ServiceModel.ServiceHost> para o seu serviço. Para obter instruções completas, consulte [programação básica do WCF](../basic-wcf-programming.md).  
  
2. Para cada <xref:System.ServiceModel.Description.ServiceEndpoint> host de serviço especificado, localize seu <xref:System.ServiceModel.Description.OperationDescription> .  
  
3. Pesquise os comportamentos de operação para determinar se uma instância do <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> foi encontrada.  
  
4. Se <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> for encontrado, defina sua <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractSurrogate%2A> propriedade como uma nova instância do substituto. Se não <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> for encontrado, crie uma nova instância e defina o <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractSurrogate%2A> membro do novo comportamento como uma nova instância do substituto.  
  
5. Por fim, adicione esse novo comportamento aos comportamentos de operação atuais, conforme mostrado no exemplo a seguir:  
  
     [!code-csharp[C_IDataContractSurrogate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#8)]  
  
### <a name="to-use-a-surrogate-for-metadata-import"></a>Para usar um substituto para importação de metadados  

 Ao importar metadados como WSDL e XSD para gerar o código do lado do cliente, o substituto precisa ser adicionado ao componente responsável pela geração de código do esquema XSD, <xref:System.Runtime.Serialization.XsdDataContractImporter> . Para fazer isso, modifique diretamente o <xref:System.ServiceModel.Description.WsdlImporter> usado para importar os metadados.  
  
##### <a name="to-implement-a-surrogate-for-metadata-importation"></a>Para implementar um substituto para a importação de metadados  
  
1. Importe os metadados usando a <xref:System.ServiceModel.Description.WsdlImporter> classe.  
  
2. Use o <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> método para verificar se um <xref:System.Runtime.Serialization.XsdDataContractImporter> foi definido.  
  
3. Se o <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> método retornar `false` , crie um novo <xref:System.Runtime.Serialization.XsdDataContractImporter> e defina sua <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A> propriedade como uma nova instância da <xref:System.Runtime.Serialization.ImportOptions> classe. Caso contrário, use o importador retornado pelo `out` parâmetro do <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> método.  
  
4. Se o <xref:System.Runtime.Serialization.XsdDataContractImporter> não tiver <xref:System.Runtime.Serialization.ImportOptions> definido, defina a propriedade como uma nova instância da <xref:System.Runtime.Serialization.ImportOptions> classe.  
  
5. Defina a <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A> Propriedade do <xref:System.Runtime.Serialization.ImportOptions> de <xref:System.Runtime.Serialization.XsdDataContractImporter> para uma nova instância do substituto.  
  
6. Adicione o <xref:System.Runtime.Serialization.XsdDataContractImporter> à coleção retornada pela <xref:System.ServiceModel.Description.MetadataExporter.State%2A> Propriedade do <xref:System.ServiceModel.Description.WsdlImporter> (herdado da <xref:System.ServiceModel.Description.MetadataExporter> classe).  
  
7. Use o <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A> método do <xref:System.ServiceModel.Description.WsdlImporter> para importar todos os contratos de dados dentro do esquema. Durante a última etapa, o código é gerado a partir dos esquemas carregados chamando o substituto.  
  
     [!code-csharp[C_IDataContractSurrogate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#9)]  
  
### <a name="to-use-a-surrogate-for-metadata-export"></a>Para usar um substituto para exportação de metadados  

 Por padrão, ao exportar metadados do WCF para um serviço, o esquema WSDL e XSD precisa ser gerado. O substituto precisa ser adicionado ao componente responsável pela geração do esquema XSD para tipos de contrato de dados, <xref:System.Runtime.Serialization.XsdDataContractExporter> . Para fazer isso, use um comportamento que implementa <xref:System.ServiceModel.Description.IWsdlExportExtension> para modificar o <xref:System.ServiceModel.Description.WsdlExporter> , ou modifique diretamente o <xref:System.ServiceModel.Description.WsdlExporter> usado para exportar metadados.  
  
##### <a name="to-use-a-surrogate-for-metadata-export"></a>Para usar um substituto para exportação de metadados  
  
1. Crie um novo <xref:System.ServiceModel.Description.WsdlExporter> ou use o `wsdlExporter` parâmetro passado para o <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A> método.  
  
2. Use a <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> função para verificar se um <xref:System.Runtime.Serialization.XsdDataContractExporter> foi definido.  
  
3. Se <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> retornar `false` , crie um novo <xref:System.Runtime.Serialization.XsdDataContractExporter> com os esquemas XML gerados do <xref:System.ServiceModel.Description.WsdlExporter> e adicione-o à coleção retornada pela <xref:System.ServiceModel.Description.MetadataExporter.State%2A> Propriedade do <xref:System.ServiceModel.Description.WsdlExporter> . Caso contrário, use o exportador retornado pelo `out` parâmetro do <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> método.  
  
4. Se o <xref:System.Runtime.Serialization.XsdDataContractExporter> não tiver <xref:System.Runtime.Serialization.ExportOptions> definido, defina a <xref:System.Runtime.Serialization.XsdDataContractExporter.Options%2A> propriedade como uma nova instância da <xref:System.Runtime.Serialization.ExportOptions> classe.  
  
5. Defina a <xref:System.Runtime.Serialization.ExportOptions.DataContractSurrogate%2A> Propriedade do <xref:System.Runtime.Serialization.ExportOptions> de <xref:System.Runtime.Serialization.XsdDataContractExporter> para uma nova instância do substituto. As etapas subsequentes para exportar metadados não exigem nenhuma alteração.  
  
     [!code-csharp[C_IDataContractSurrogate#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#10)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.IDataContractSurrogate>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>
- <xref:System.Runtime.Serialization.ImportOptions>
- <xref:System.Runtime.Serialization.ExportOptions>
- [Usando contratos de dados](../feature-details/using-data-contracts.md)
