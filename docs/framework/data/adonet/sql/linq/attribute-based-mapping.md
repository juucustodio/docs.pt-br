---
description: 'Saiba mais sobre: mapeamento de Attribute-Based'
title: Mapeamento baseado em atributos
ms.date: 03/30/2017
ms.assetid: 6dd89999-f415-4d61-b8c8-237d23d7924e
ms.openlocfilehash: 9dfe9fce10d7ba76281afd843385c734e86af245
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712721"
---
# <a name="attribute-based-mapping"></a>Mapeamento baseado em atributos

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] mapeia um banco de dados SQL Server para um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] modelo de objeto aplicando atributos ou usando um arquivo de mapeamento externo. Este tópico descreve a abordagem baseada em atributos.  
  
 Em sua forma mais elementar, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] mapeia um banco de dados para um <xref:System.Data.Linq.DataContext>, uma tabela para uma classe e colunas e relações para propriedades nessas classes. Você também pode usar atributos para mapear uma hierarquia de herança no seu modelo de objeto. Para obter mais informações, consulte [como gerar o modelo de objeto em Visual Basic ou em C#](how-to-generate-the-object-model-in-visual-basic-or-csharp.md).  
  
 Os desenvolvedores que usam o Visual Studio normalmente executam o mapeamento baseado em atributo usando o Object Relational Designer. Você também pode usar a ferramenta de linha de comando SqlMetal ou pode codificar manualmente os atributos. Para obter mais informações, consulte [como gerar o modelo de objeto em Visual Basic ou em C#](how-to-generate-the-object-model-in-visual-basic-or-csharp.md).  
  
> [!NOTE]
> Você também pode mapear usando um arquivo XML externo. Para obter mais informações, consulte [mapeamento externo](external-mapping.md).  
  
 As seguintes seções descrevem o mapeamento baseado em atributos com mais detalhes. Para obter mais informações, consulte o namespace de <xref:System.Data.Linq.Mapping>.  
  
## <a name="databaseattribute-attribute"></a>Atributo DatabaseAttribute  

 Use esse atributo para especificar o nome padrão do banco de dados quando um nome não é fornecido pela conexão. Esse atributo é opcional, mas, se você usá-lo, deverá aplicar a propriedade <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>, como descrito na tabela a seguir.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>|String|Veja <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>|Usado com sua propriedade <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>, especifica o nome do banco de dados.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.DatabaseAttribute>.  
  
## <a name="tableattribute-attribute"></a>Atributo TableAttribute  

 Use esse atributo para designar uma classe como uma classe de entidade que está associada com uma tabela de banco de dados ou uma exibição. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] trata as classes que têm esse atributo como classes persistentes. A tabela a seguir descreve a propriedade <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A>.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.TableAttribute.Name%2A>|String|Mesma cadeia de caracteres que o nome da classe|Designa uma classe como uma classe de entidade associada a uma tabela de banco de dados.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.TableAttribute>.  
  
## <a name="columnattribute-attribute"></a>Atributo ColumnAttribute  

 Use esse atributo para designar um membro de uma classe de entidade para representar uma coluna em uma tabela de banco de dados. Você pode aplicar este atributo a qualquer campo ou propriedade.  
  
 Somente os membros que você identifica como colunas são recuperados e persistidos quando o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] salva as alterações para o banco de dados. Os membros sem este atributo são considerados não persistentes e não são enviados para inserções ou atualizações.  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A>|AutoSync|Nunca|Instrui o CLR (Common Language Runtime) para recuperar o valor depois de uma operação de inserção ou atualização.<br /><br /> Opções: Always, Never, OnUpdate, OnInsert.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A>|Boolean|`true`|Indica que uma coluna pode conter valores nulos.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>|String|Tipo de coluna do banco de dados inferido|Usa tipos de banco de dados e modificadores para especificar o tipo de coluna de banco de dados.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.Expression%2A>|String|Vazio|Define uma coluna computada em um banco de dados.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>|Boolean|`false`|Indica que uma coluna contém os valores que o banco de dados gera automaticamente.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDiscriminator%2A>|Boolean|`false`|Indica que a coluna contém um valor de discriminador para uma hierarquia de herança do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>|Boolean|`false`|Especifica que este membro da classe representa uma coluna que é ou faz parte das chaves primárias da tabela.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>|Boolean|`false`|Identifica o tipo de coluna do membro como um carimbo de data/hora ou número de versão do banco de dados.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>|UpdateCheck|`Always`, a menos que <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> seja `true` para um membro|Especifica como o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] aborda a detecção de conflitos de simultaneidade otimista.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.ColumnAttribute>.  
  
> [!NOTE]
> Os valores de propriedade de armazenamento AssociationAttribute e ColumnAttribute diferenciam maiúsculas de minúsculas. Por exemplo, verifique se os valores usados no atributo para a propriedade AssociationAttribute.Storage coincidem maiúsculas e minúsculas para os nomes de propriedades correspondentes usados em outro lugar no código. Isso se aplica a todas as linguagens de programação .NET, mesmo aquelas que não costumam diferenciar maiúsculas de minúsculas, incluindo Visual Basic. Para obter mais informações sobre a propriedade Storage, consulte <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>.  
  
## <a name="associationattribute-attribute"></a>Atributo AssociationAttribute  

 Use esse atributo para designar uma propriedade para representar uma associação no banco de dados, como uma chave estrangeira para a relação de chave primária. Para obter mais informações sobre relações, consulte [como mapear relações de banco de dados](how-to-map-database-relationships.md).  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.DeleteOnNull%2A>|Boolean|`false`|Quando colocado em uma associação cujos membros de chave estrangeira são todos não anuláveis, exclui o objeto quando a associação é definida como nulo.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.DeleteRule%2A>|String|Nenhum|Adiciona o comportamento de exclusão para uma associação.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.IsForeignKey%2A>|Boolean|`false`|Se for verdadeiro, designa o membro como a chave estrangeira em uma associação que representa uma relação de banco de dados.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.IsUnique%2A>|Boolean|`false`|Se for verdadeiro, indica uma restrição de exclusividade na chave estrangeira.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A>|String|Identificação da classe relacionada|Designa um ou mais membros da classe de entidade de destino como valores chave no outro lado da associação.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.ThisKey%2A>|String|Identificação da classe recipiente|Designa os membros dessa classe de entidade para representar os valores chave nesse lado da associação.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.AssociationAttribute>.  
  
> [!NOTE]
> Os valores de propriedade de armazenamento AssociationAttribute e ColumnAttribute diferenciam maiúsculas de minúsculas. Por exemplo, verifique se os valores usados no atributo para a propriedade AssociationAttribute.Storage coincidem maiúsculas e minúsculas para os nomes de propriedades correspondentes usados em outro lugar no código. Isso se aplica a todas as linguagens de programação .NET, mesmo aquelas que não costumam diferenciar maiúsculas de minúsculas, incluindo Visual Basic. Para obter mais informações sobre a propriedade Storage, consulte <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>.  
  
## <a name="inheritancemappingattribute-attribute"></a>Atributo InheritanceMappingAttribute  

 Use esse atributo para mapear uma hierarquia de herança.  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Code%2A>|String|Nenhum. O valor deve ser fornecido.|Especifica o valor do código do discriminador.|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.IsDefault%2A>|Boolean|`false`|Se for verdadeiro, instancia objeto desse tipo quando nenhum valor de discriminador no repositório coincide com nenhum dos valores especificados.|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Type%2A>|Tipo|Nenhum. O valor deve ser fornecido.|Especifica o tipo da classe na hierarquia.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute>.  
  
## <a name="functionattribute-attribute"></a>Atributo FunctionAttribute  

 Use esse atributo para designar um método como representação de um procedimento armazenado ou uma função definida pelo usuário no banco de dados.  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.FunctionAttribute.IsComposable%2A>|Boolean|`false`|Se for falso, indica o mapeamento para um procedimento armazenado. Se for verdadeiro, indica o mapeamento para uma função definida pelo usuário.|  
|<xref:System.Data.Linq.Mapping.FunctionAttribute.Name%2A>|String|Mesma cadeia de caracteres que nome no banco de dados|Especifica o nome do procedimento armazenado ou função definida pelo usuário.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.FunctionAttribute>.  
  
## <a name="parameterattribute-attribute"></a>Atributo ParameterAttribute  

 Use esse atributo para mapear parâmetros de entrada em métodos de procedimentos armazenados.  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ParameterAttribute.DbType%2A>|String|Nenhum|Especifica o tipo de banco de dados.|  
|<xref:System.Data.Linq.Mapping.ParameterAttribute.Name%2A>|String|Mesma cadeia de caracteres que o nome do parâmetro no banco de dados|Especifica um nome para o parâmetro.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.ParameterAttribute>.  
  
## <a name="resulttypeattribute-attribute"></a>Atributo ResultTypeAttribute  

 Use esse atributo para especificar um tipo de resultado.  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ResultTypeAttribute.Type%2A>|Type|(Nenhuma)|Usado em métodos mapeados para procedimentos armazenados que retornam <xref:System.Data.Linq.IMultipleResults>. Declarar os mapeamentos de tipos válidos ou esperados para o procedimento armazenado.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.ResultTypeAttribute>.  
  
## <a name="dataattribute-attribute"></a>Atributo DataAttribute  

 Use esse atributo para especificar nomes e campos de armazenamento privado.  
  
 A tabela a seguir descreve as propriedades desse atributo.  
  
|Propriedade|Type|Padrão|Descrição|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.DataAttribute.Name%2A>|String|Mesmo que o nome no banco de dados|Especifica o nome da tabela, coluna e assim por diante.|  
|<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>|String|Acessadores públicos|Especifica o nome do campo de armazenamento subjacente.|  
  
 Para obter mais informações, consulte <xref:System.Data.Linq.Mapping.DataAttribute>.  
  
## <a name="see-also"></a>Consulte também

- [Referência](reference.md)
