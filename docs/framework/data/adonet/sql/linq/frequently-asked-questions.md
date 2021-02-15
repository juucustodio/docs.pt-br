---
description: 'Saiba mais sobre: perguntas frequentes'
title: Perguntas frequentes
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 252ed666-0679-4eea-b71b-2f14117ef443
ms.openlocfilehash: 476e9adc3dc88bce786b8b8423e05e800c821320
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739073"
---
# <a name="frequently-asked-questions"></a>Perguntas frequentes

As seções a seguir respondem a alguns problemas comuns que você pode encontrar ao implementar o LINQ.

Problemas adicionais são abordados na [solução de problemas](troubleshooting.md).

## <a name="cannot-connect"></a>Não é possível conectar

Q. Não consigo me conectar a meu banco de dados.

a. Verifique se a cadeia de conexão está correta e se sua instância de SQL Server está em execução. Observe também que o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] exige que o protocolo de pipes nomeados esteja ativado. Para obter mais informações, consulte [aprendendo por instruções](learning-by-walkthroughs.md).

## <a name="changes-to-database-lost"></a>Alterações perdidas do banco de dados

Q. Fiz uma alteração nos dados no banco de dados, mas, quando executei o aplicativo, a alteração não estava mais lá.

a. Verifique se você chamou <xref:System.Data.Linq.DataContext.SubmitChanges%2A> para salvar os resultados no banco de dados.

## <a name="database-connection-open-how-long"></a>Conexão do banco de dados: há quanto tempo está aberta?

Q. Quanto tempo a conexão do banco de dados permanece aberta?

a. Uma conexão geralmente permanece aberta até você consumir os resultados da consulta. Se você pretende processar todos os resultados e não se opõe a armazenar em cache os resultados, aplique <xref:System.Linq.Enumerable.ToList%2A> à consulta. Em cenários comuns onde cada objeto é processado somente uma vez, o modelo de streaming é superior no `DataReader` e no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].

Os detalhes exatos do uso da conexão dependem do seguinte:

- Status da conexão se <xref:System.Data.Linq.DataContext> for construído com um objeto de conexão.

- Configurações da cadeia de conexão (por exemplo, permitindo MARS, Multiple Active Result Sets). Para obter mais informações, confira [MARS (Conjunto de Resultados Ativos Múltiplos)](../multiple-active-result-sets-mars.md).

## <a name="updating-without-querying"></a>Atualizar sem consultar

Q. Posso atualizar os dados da tabela sem primeiro consultar o banco de dados?

a. Embora o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não tenha comandos de atualização baseados em conjunto, você pode usar qualquer uma das seguintes técnicas para atualizar sem consultar primeiro:

- Use <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> para enviar o código SQL.

- Crie uma nova instância do objeto e inicialize todos os valores atuais (campos) que afetam a atualização. Anexe o objeto ao <xref:System.Data.Linq.DataContext> usando <xref:System.Data.Linq.Table%601.Attach%2A> e modifique o campo que você deseja alterar.

## <a name="unexpected-query-results"></a>Resultados inesperados da consulta

Q. Minha consulta está retornando resultados inesperados. Como posso inspecionar o que está ocorrendo?

a. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornece várias ferramentas para inspecionar o código SQL que produz. Um dos mais importantes é <xref:System.Data.Linq.DataContext.Log%2A>. Para obter mais informações, consulte [depuração de suporte](debugging-support.md).

## <a name="unexpected-stored-procedure-results"></a>Resultados inesperados de procedimentos armazenados

Q. Tenho um procedimento armazenado cujo valor de retorno é calculado por `MAX()`. Quando arrasto o procedimento armazenado para a superfície o/R Designer, o valor de retorno não está correto.

a. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornece duas maneiras de retornar valores gerados por banco de dados por meio de procedimentos armazenados:

- Nomeando o resultado de saída.

- Especificando explicitamente um parâmetro de saída.

O código a seguir é um exemplo de saída incorreta. Como o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não pode mapear os resultados, ele sempre retorna 0:

```sql
create procedure proc2

as

begin

select max(i) from t where name like 'hello'

end
```

O código a seguir é um exemplo de saída correta usando um parâmetro de saída:

```sql
create procedure proc2

@result int OUTPUT

as

select @result = MAX(i) from t where name like 'hello'

go
```

O código a seguir é um exemplo de saída correta nomeando o resultado de saída:

```sql
create procedure proc2

as

begin

select nax(i) AS MaxResult from t where name like 'hello'

end
```

Para obter mais informações, consulte [Personalizando operações usando procedimentos armazenados](customizing-operations-by-using-stored-procedures.md).

## <a name="serialization-errors"></a>Erros de serialização

Q. Quando tento serializar, obtenho o seguinte erro: "tipo ' System. Data. Linq. ChangeTracker + StandardChangeTracker '... Não está marcado como serializável. "

a. A geração de código no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dá suporte à serialização do <xref:System.Runtime.Serialization.DataContractSerializer>. Ela não dá suporte a <xref:System.Xml.Serialization.XmlSerializer> ou <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>. Para obter mais informações, consulte [Serialização](serialization.md).

## <a name="multiple-dbml-files"></a>Vários arquivos DBML

Q. Quando eu tenho vários arquivos DBML que compartilham algumas tabelas em comum, eu obtenho um erro do compilador.

a. Defina o **namespace de contexto** e as propriedades de **namespace de entidade** do Object Relational Designer para um valor distinto para cada arquivo dbml. Essa abordagem elimina a colisão nome/namespace.

## <a name="avoiding-explicit-setting-of-database-generated-values-on-insert-or-update"></a>Evitando a configuração explícita de valores gerados por banco de dados em Insert ou Update

Q. Tenho uma tabela de banco de dados com uma coluna `DateCreated` que usa como padrão o `Getdate()` do SQL. Quando tento inserir um novo registro usando o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], o valor é definido como `NULL`. Eu gostaria que ele fosse definido como o padrão do banco de dados.

a. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] trata essa situação automaticamente para colunas de identidade (incremento automático) e rowguidcol (GUID gerado por banco de dados) e carimbo de data/hora. Em outros casos, você deve definir <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> = `true` e <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> = <xref:System.Data.Linq.Mapping.AutoSync.Always> / <xref:System.Data.Linq.Mapping.AutoSync.OnInsert> / <xref:System.Data.Linq.Mapping.AutoSync.OnUpdate> Propriedades manualmente.

## <a name="multiple-dataloadoptions"></a>Vários DataLoadOptions

Q. Posso especificar opções de carregamento adicionais sem substituir as primeiras?

a. Sim. A primeira não é substituída, como no exemplo a seguir:

```vb
Dim dlo As New DataLoadOptions()
dlo.LoadWith(Of Order)(Function(o As Order) o.Customer)
dlo.LoadWith(Of Order)(Function(o As Order) o.OrderDetails)
```

```csharp
DataLoadOptions dlo = new DataLoadOptions();
dlo.LoadWith<Order>(o => o.Customer);
dlo.LoadWith<Order>(o => o.OrderDetails);
```

## <a name="errors-using-sql-compact-35"></a>Erros ao usar o SQL Compact 3.5

Q. Recebo um erro quando arrasto tabelas de um banco de dados SQL Server Compact 3,5.

a. O Object Relational Designer não oferece suporte a SQL Server Compact 3,5, embora o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tempo de execução faça. Nesta situação, você deve criar suas próprias classes de entidade e adicionar os atributos apropriados.

## <a name="errors-in-inheritance-relationships"></a>Erros nas relações de herança

Q. Usei a forma de herança da caixa de ferramentas no Object Relational Designer para conectar duas entidades, mas recebo erros.

a. Criar a relação não é suficiente. Você deve fornecer informações como a coluna do discriminador, o valor do discriminador da classe base e o valor do discriminador da classe derivada.

## <a name="provider-model"></a>Modelo do provedor

Q. Um modelo de provedor público está disponível?

a. Nenhum modelo de provedor público está disponível. Neste momento, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] oferece suporte apenas a SQL Server e SQL Server Compact 3,5.

## <a name="sql-injection-attacks"></a>Ataques de injeção de SQL

Q. Como o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] é protegido contra ataques de injeção de SQL?

a. A injeção de SQL tem sido um risco significativo para consultas tradicionais de SQL formadas por meio da concatenação da entrada do usuário. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] evita essa injeção usando o <xref:System.Data.SqlClient.SqlParameter> em consultas. A entrada do usuário é transformada em valores de parâmetro. Essa abordagem impede que os comandos mal-intencionados sejam usados da entrada do cliente.

## <a name="changing-read-only-flag-in-dbml-files"></a>Alterando o sinalizador somente leitura em arquivos DBML

Q. Como posso eliminar configuradores de algumas propriedades quando crio um modelo de objeto de um arquivo DBML?

a. Siga as etapas a seguir para este cenário avançado:

1. No arquivo .dbml, modifique a propriedade alterando o sinalizador do <xref:System.Data.Linq.ITable.IsReadOnly%2A> para `True`.

2. Adicione uma classe parcial. Crie um construtor com parâmetros para os membros somente leitura.

3. Examine o valor padrão <xref:System.Data.Linq.Mapping.UpdateCheck> (<xref:System.Data.Linq.Mapping.UpdateCheck.Never>) para determinar se este é o valor correto para seu aplicativo.

    > [!CAUTION]
    > Se você estiver usando o Object Relational Designer no Visual Studio, suas alterações poderão ser substituídas.

## <a name="aptca"></a>APTCA

Q. O System.Data.Linq está marcado para ser usado pelo código parcialmente confiável?

a. Sim, o assembly System.Data.Linq.dll está entre os assemblies de .NET Framework marcados com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo. Sem essa marcação, os assemblies no .NET Framework destinam-se ao uso somente por código totalmente confiável.

O cenário principal no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para permitir chamadores parcialmente confiáveis é habilitar o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] assembly a ser acessado de aplicativos Web, onde a configuração de *confiança* é média.

## <a name="mapping-data-from-multiple-tables"></a>Dados de mapeamento de várias tabelas

Q. Os dados na minha entidade vêm de várias tabelas. Como posso mapeá-los?

a. Você pode criar uma exibição em um banco de dados e mapear a entidade para a exibição. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] gera o mesmo SQL para exibições da mesma forma que faz para tabelas.

> [!NOTE]
> O uso de exibições nesse cenário tem limitações. Essa abordagem funciona com mais segurança quando as operações realizadas no <xref:System.Data.Linq.Table%601> têm suporte pela exibição subjacente. Somente você sabe quais operações são desejadas. Por exemplo, a maioria dos aplicativos são somente leitura e outro número considerável executa `Create` / `Update` / `Delete` operações somente usando procedimentos armazenados em exibições.

## <a name="connection-pooling"></a>Pool de conexões

Q. Há uma construção que possa ajudar com o pool de <xref:System.Data.Linq.DataContext>?

a. Não tente reutilizar instâncias do <xref:System.Data.Linq.DataContext>. Cada <xref:System.Data.Linq.DataContext> mantém o estado (incluindo um cache de identidade) para uma determinada sessão de edição/consulta. Para obter as novas instâncias com base no estado atual do banco de dados, use um novo <xref:System.Data.Linq.DataContext>.

Você ainda pode usar o pool de conexões ADO.NET subjacente. Para obter mais informações, consulte [Pool de Conexões do SQL Server (ADO.NET)](../../sql-server-connection-pooling.md).

## <a name="second-datacontext-is-not-updated"></a>O segundo DataContext não é atualizado

Q. Eu usei uma instância do <xref:System.Data.Linq.DataContext> para armazenar valores no banco de dados. No entanto, um segundo <xref:System.Data.Linq.DataContext> no mesmo banco de dados não reflete os valores atualizados. A segunda instância do <xref:System.Data.Linq.DataContext> parece retornar os valores armazenados em cache.

a. Este comportamento ocorre por design. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] continua a retornar as mesmas instâncias/valores que você viu na primeira instância. Quando você faz atualizações, usa a simultaneidade otimista. Os dados originais são usados para verificar o estado atual do banco de dados e declarar que ainda estão de fato inalterados. Se eles forem alterados, um conflito ocorre e seu aplicativo deve resolvê-lo. Uma opção do aplicativo é redefinir o estado original para o estado atual do banco de dados e tentar novamente a atualização. Para obter mais informações, consulte [como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md).

Você também pode definir o <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> como falso, o que desativa o cache e o controle de alterações. Você pode então recuperar os valores mais recentes toda vez que consultar.

## <a name="cannot-call-submitchanges-in-read-only-mode"></a>Não é possível chamar SubmitChanges no modo somente leitura

Q. Quando eu tento chamar <xref:System.Data.Linq.DataContext.SubmitChanges%2A> no modo somente leitura, obtenho um erro.

a. O modo somente leitura desativa a capacidade de o contexto controlar as alterações.

## <a name="see-also"></a>Consulte também

- [Referência](reference.md)
- [Solução de problemas](troubleshooting.md)
- [Segurança em LINQ to SQL](security-in-linq-to-sql.md)
