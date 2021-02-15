---
description: 'Saiba mais sobre: recuperação de dados e operações CUD em aplicativos de N camadas (LINQ to SQL)'
title: Recuperação de dados e operações de COMIDA RUMINADA em aplicativos de n camadas (LINQ to SQL)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c3133d53-83ed-4a4d-af8b-82edcf3831db
ms.openlocfilehash: dbad65e1bd29227f434166dca364946a68256177
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672160"
---
# <a name="data-retrieval-and-cud-operations-in-n-tier-applications-linq-to-sql"></a>Recuperação de dados e operações de COMIDA RUMINADA em aplicativos de n camadas (LINQ to SQL)

Quando você serializa objetos de entidade como clientes ou pedidos para um cliente em uma rede, essas entidades são desanexadas de seu contexto de dados. O contexto de dados não controla as alterações ou suas associações com outros objetos. Isso não é um problema que os clientes estão lê apenas os dados. Também é relativamente simples permitir que clientes para adicionar novas linhas em uma base de dados. No entanto, se seu aplicativo requer que os clientes possam atualizar ou excluir dados, você deve anexar as entidades a um novo contexto de dados antes de chamar <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType>. Além disso, se você estiver usando uma verificação de simultaneidade otimista com valores originais, então você também precisará de uma maneira de fornecer a base de dados a entidade original e a entidade como modificada. Os métodos de `Attach` são fornecidos para permite que você coloque entidades em um novo contexto de dados depois que foram separados.  
  
 Mesmo que você esteja serializando objetos de proxy no lugar das [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] entidades, você ainda precisará construir uma entidade na Dal (camada de acesso a dados) e anexá-la a uma nova <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> , a fim de enviar os dados para ele.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] é completamente diferente de como as entidades são serializadas. Para obter mais informações sobre como usar as ferramentas Object Relational Designer e SqlMetal para gerar classes que são serializáveis usando o Windows Communication Foundation (WCF), consulte [como: tornar entidades serializáveis](how-to-make-entities-serializable.md).  
  
> [!NOTE]
> Chamar apenas os métodos de `Attach` em novos ou entidades desserializado. A única maneira para uma entidade é desanexada de seu contexto de dados original é para que é serializada. Se você tentar anexar uma entidade undetached a um novo contexto de dados, e a entidade tem adiado ainda carregadores de seu contexto de dados anterior, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] seja lançada uma exceção. Uma entidade com os carregadores adiados de dois contextos diferentes de dados pode causar resultados indesejados enquanto você executa a inserção, atualiazação, e as operações de exclusão na entidade. Para obter mais informações sobre carregadores adiados, consulte [carregamento adiado versus imediato](deferred-versus-immediate-loading.md).  
  
## <a name="retrieving-data"></a>Recuperando dados  
  
### <a name="client-method-call"></a>Chamada de método de cliente  

 Os seguintes exemplos mostram uma chamada de método de exemplo para DAL de um cliente Windows Forms. Nesse exemplo, o DAL é implementado como uma biblioteca de serviço do Windows:  
  
```vb  
Private Function GetProdsByCat_Click(ByVal sender As Object, ByVal e _  
    As EventArgs)  
  
    ' Create the WCF client proxy.  
    Dim proxy As New NorthwindServiceReference.Service1Client  
  
    ' Call the method on the service.  
    Dim products As NorthwindServiceReference.Product() = _  
        proxy.GetProductsByCategory(1)  
  
    ' If the database uses original values for concurrency checks,  
    ' the client needs to store them and pass them back to the  
    ' middle tier along with the new values when updating data.  
  
    For Each v As NorthwindClient1.NorthwindServiceReference.Product _  
        In products  
        ' Persist to a List(Of Product) declared at class scope.  
        ' Additional change-tracking logic is the responsibility  
        ' of the presentation tier and/or middle tier.  
        originalProducts.Add(v)  
    Next  
  
    ' (Not shown) Bind the products list to a control  
    ' and/or perform whatever processing is necessary.  
End Function  
```  
  
```csharp  
private void GetProdsByCat_Click(object sender, EventArgs e)  
{  
    // Create the WCF client proxy.  
    NorthwindServiceReference.Service1Client proxy =
    new NorthwindClient.NorthwindServiceReference.Service1Client();  
  
    // Call the method on the service.  
    NorthwindServiceReference.Product[] products =
    proxy.GetProductsByCategory(1);  
  
    // If the database uses original values for concurrency checks,
    // the client needs to store them and pass them back to the
    // middle tier along with the new values when updating data.  
    foreach (var v in products)  
    {  
        // Persist to a list<Product> declared at class scope.  
        // Additional change-tracking logic is the responsibility  
        // of the presentation tier and/or middle tier.  
        originalProducts.Add(v);  
    }  
  
    // (Not shown) Bind the products list to a control  
    // and/or perform whatever processing is necessary.  
    }  
```  
  
### <a name="middle-tier-implementation"></a>Implementação de camada intermediária  

 O exemplo a seguir mostra uma implementação do método de interface na camada intermediária. A seguir estão as duas problemas básicas para a observação:  
  
- <xref:System.Data.Linq.DataContext> é declarado no escopo do método.  
  
- O método retorna uma coleção de <xref:System.Collections.IEnumerable> de resultados reais. O serializador executar a consulta para enviar os resultados de volta para o cliente/camada de apresentação. Para acessar localmente os resultados da consulta na camada intermediária, você pode forçar a execução chamando `ToList` ou `ToArray` na variável de consulta. Você pode então retornar a lista ou matriz como `IEnumerable`.  
  
```vb  
Public Function GetProductsByCategory(ByVal categoryID As Integer) _  
    As IEnumerable(Of Product)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    Dim productQuery = _  
    From prod In db.Products _  
    Where prod.CategoryID = categoryID _  
    Select prod  
  
    Return productQuery.AsEnumerable()  
  
End Function  
```  
  
```csharp  
public IEnumerable<Product> GetProductsByCategory(int categoryID)  
{  
    NorthwindClasses1DataContext db =
    new NorthwindClasses1DataContext(connectionString);  
  
    IEnumerable<Product> productQuery =  
    from prod in db.Products  
    where prod.CategoryID == categoryID  
    select prod;  
  
    return productQuery.AsEnumerable();
}  
```  
  
 Uma instância de um contexto de dados deve ter um tempo de vida de uma unidade de trabalho “.” Em um ambiente fracamente acoplado, uma unidade de trabalho é normalmente pequena, talvez uma transação otimista, incluindo uma única chamada a `SubmitChanges`. Portanto, o contexto de dados é criado e descartado no escopo de método. Se a unidade de trabalho inclui chamadas a lógica das regras comerciais, então você geralmente deseja manter a instância de `DataContext` para essa operação inteira. Em qualquer caso, as instâncias de `DataContext` não sejam mantidas ativas por longos períodos de tempo entre os números arbitrários de transações.  
  
 Este método retornará objetos do produto mas não a coleção de objetos de Order_Detail que são associados a cada produto. Use o objeto de <xref:System.Data.Linq.DataLoadOptions> para alterar esse comportamento padrão. Para obter mais informações, consulte [como controlar a quantidade de dados relacionados recuperados](how-to-control-how-much-related-data-is-retrieved.md).  
  
## <a name="inserting-data"></a>Inserindo dados  

 Para inserir um novo objeto, chamadas camada de apresentação apenas o método relevante na interface de camada intermediária, e passa no novo objeto inserção. Em alguns casos, pode ser mais eficiente para o cliente envia somente em alguns valores e com a camada intermediária construir o objeto completo.  
  
### <a name="middle-tier-implementation"></a>Implementação de camada intermediária  

 Na camada intermediária, novo <xref:System.Data.Linq.DataContext> é criado, o objeto é anexado a <xref:System.Data.Linq.DataContext> usando o método <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> , e o objeto é inserido quando <xref:System.Data.Linq.DataContext.SubmitChanges%2A> é chamado. Exceções, callbacks, e as condições de erro podem ser tratados assim como em qualquer outro cenário de serviço Web.  
  
```vb  
' No call to Attach is necessary for inserts.  
Public Sub InsertOrder(ByVal o As Order)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    db.Orders.InsertOnSubmit(o)  
  
    ' Exception handling not shown.  
    db.SubmitChanges()  
  
End Sub  
```  
  
```csharp  
// No call to Attach is necessary for inserts.  
    public void InsertOrder(Order o)  
    {  
        NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
        db.Orders.InsertOnSubmit(o);  
  
        // Exception handling not shown.  
        db.SubmitChanges();  
    }  
```  
  
## <a name="deleting-data"></a>Excluindo dados  

 Para excluir um objeto existente de base de dados, de chamadas camada de apresentação o método relevante na interface de camada intermediária, e passa em sua cópia que inclui valores originais do objeto a ser excluído.  
  
 Operações de exclusão envolvem verificação de simultaneidade otimista, e o objeto a ser excluído deve primeiro ser anexado ao novo contexto de dados. Nesse exemplo, o parâmetro de `Boolean` é definido como `false` para indicar que o objeto não tem um carimbo de data/hora (RowVersion). Se sua tabela de base de dados gerencia carimbos de data/hora para cada registro, então a verificação de simultaneidade são muito mais simples, especialmente para o cliente. Basta passar no original ou o objeto alterado e define o parâmetro de `Boolean` a `true`. Em qualquer caso, na camada intermediária é geralmente necessário capturar <xref:System.Data.Linq.ChangeConflictException>. Para obter mais informações sobre como lidar com conflitos de simultaneidade otimista, consulte [simultaneidade otimista: visão geral](optimistic-concurrency-overview.md).  
  
 Para excluir as entidades que têm restrições de chave externa em tabelas associadas, você deve primeiro excluir todos os objetos nas coleções de <xref:System.Data.Linq.EntitySet%601> .  
  
```vb  
' Attach is necessary for deletes.  
Public Sub DeleteOrder(ByVal order As Order)  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
  
    db.Orders.Attach(order, False)  
    ' This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order)  
  
    Try  
        ' ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict)  
  
    Catch ex As ChangeConflictException  
        ' Get conflict information, and take actions  
        ' that are appropriate for your application.  
        ' See MSDN Article "How to: Manage Change  
        ' Conflicts (LINQ to SQL).  
  
    End Try  
End Sub  
```  
  
```csharp  
// Attach is necessary for deletes.  
public void DeleteOrder(Order order)  
{  
    NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
  
    db.Orders.Attach(order, false);  
    // This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order);  
    try  
    {  
        // ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict);  
    }  
    catch (ChangeConflictException e)  
    {  
       // Get conflict information, and take actions  
       // that are appropriate for your application.  
       // See MSDN Article How to: Manage Change Conflicts (LINQ to SQL).  
    }  
}  
```  
  
## <a name="updating-data"></a>Atualizando dados  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] suporta atualizações nesses cenários que envolvem concorrência otimista:  
  
- Concorrência otimista com base em carimbos de data/hora ou em números de RowVersion.  
  
- Concorrência otimista com base em valores originais de um subconjunto de propriedades de entidade.  
  
- Concorrência otimista com base nas entidades originais e modificadas completos.  
  
 Você também pode executar atualizações e exclusões em uma entidade junto com suas relações, por exemplo um cliente e uma coleção de seus objetos associados de ordem. Quando você faz alterações no cliente a um gráfico de objetos de entidade e das coleções filho (de`EntitySet`), e as verificações de simultaneidade otimista exigem valores originais, o cliente deve fornecer os valores originais para cada entidade e objeto de <xref:System.Data.Linq.EntitySet%601> . Se você deseja permitir que clientes para fazer um conjunto de atualizações, de exclusões, e de inserções relacionadas em uma única chamada de método, você deve fornecer o cliente uma maneira para indicar que tipo de operação para executar em cada entidade. Na camada intermediária, então você deve chamar o método apropriado e então <xref:System.Data.Linq.ITable.Attach%2A>de <xref:System.Data.Linq.ITable.InsertOnSubmit%2A> , <xref:System.Data.Linq.ITable.DeleteAllOnSubmit%2A>, ou <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> (sem `Attach`, porque inserções) para cada entidade antes de chamar <xref:System.Data.Linq.DataContext.SubmitChanges%2A>. Não recuperar dados de base de dados como uma maneira para obter valores originais antes de tentar atualizações.  
  
 Para obter mais informações sobre simultaneidade otimista, consulte [simultaneidade otimista: visão geral](optimistic-concurrency-overview.md). Para obter informações detalhadas sobre como resolver conflitos de alteração de simultaneidade otimista, consulte [como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md).  
  
 Os seguintes exemplos demonstram cada cenário:  
  
### <a name="optimistic-concurrency-with-timestamps"></a>Concorrência otimista com carimbos de data/hora  
  
```vb  
' Assume that "customer" has been sent by client.  
' Attach with "true" to say this is a modified entity  
' and it can be checked for optimistic concurrency  
' because it has a column that is marked with the  
' "RowVersion" attribute.  
  
db.Customers.Attach(customer, True)  
  
Try  
    ' Optional: Specify a ConflictMode value  
    ' in call to SubmitChanges.  
    db.SubmitChanges()  
Catch ex As ChangeConflictException  
    ' Handle conflict based on options provided.  
    ' See MSDN article "How to: Manage Change  
    ' Conflicts (LINQ to SQL)".  
End Try  
```  
  
```csharp  
// Assume that "customer" has been sent by client.  
// Attach with "true" to say this is a modified entity  
// and it can be checked for optimistic concurrency because  
//  it has a column that is marked with "RowVersion" attribute  
db.Customers.Attach(customer, true)  
try  
{  
    // Optional: Specify a ConflictMode value  
    // in call to SubmitChanges.  
    db.SubmitChanges();  
}  
catch(ChangeConflictException e)  
{  
    // Handle conflict based on options provided  
    // See MSDN article How to: Manage Change Conflicts (LINQ to SQL).  
}  
```  
  
### <a name="with-subset-of-original-values"></a>Com subconjunto de valores originais  

 Nessa abordagem, o cliente retorna o objeto serializado completo, juntamente com os valores a serem alterados.  
  
```vb  
Public Sub UpdateProductInventory(ByVal p As Product, ByVal _  
    unitsInStock As Short?, ByVal unitsOnOrder As Short?)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        ' p is the original unmodified product  
        ' that was obtained from the database.  
        ' The client kept a copy and returns it now.  
        db.Products.Attach(p, False)  
  
        ' Now that the original values are in the data context,  
        ' apply the changes.  
        p.UnitsInStock = unitsInStock  
        p.UnitsOnOrder = unitsOnOrder  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle conflict based on options provided.  
            ' See MSDN article "How to: Manage Change Conflicts  
            ' (LINQ to SQL)".  
        End Try  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInventory(Product p, short? unitsInStock, short? unitsOnOrder)  
{  
    using (NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString))  
    {  
        // p is the original unmodified product  
        // that was obtained from the database.  
        // The client kept a copy and returns it now.  
        db.Products.Attach(p, false);  
  
        // Now that the original values are in the data context, apply the changes.  
        p.UnitsInStock = unitsInStock;  
        p.UnitsOnOrder = unitsOnOrder;  
        try  
        {  
             // Optional: Specify a ConflictMode value  
             // in call to SubmitChanges.  
             db.SubmitChanges();  
        }  
        catch (ChangeConflictException e)  
        {  
            // Handle conflict based on provided options.  
            // See MSDN article How to: Manage Change Conflicts  
            // (LINQ to SQL).  
        }  
    }  
}  
```  
  
### <a name="with-complete-entities"></a>Com entidades completos  
  
```vb  
Public Sub UpdateProductInfo(ByVal newProd As Product, ByVal _  
    originalProd As Product)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        db.Products.Attach(newProd, originalProd)  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle potential change conflicgt in whatever way  
            ' is appropriate for your application.  
            ' For more information, see the MSDN article  
            ' "How to: Manage Change Conflicts (LINQ to  
            ' SQL)".  
        End Try  
  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInfo(Product newProd, Product originalProd)  
{  
     using (NorthwindClasses1DataContext db = new  
        NorthwindClasses1DataContext(connectionString))  
     {  
         db.Products.Attach(newProd, originalProd);  
         try  
         {  
               // Optional: Specify a ConflictMode value  
               // in call to SubmitChanges.  
               db.SubmitChanges();  
         }  
        catch (ChangeConflictException e)  
        {  
            // Handle potential change conflict in whatever way  
            // is appropriate for your application.  
            // For more information, see the MSDN article  
            // How to: Manage Change Conflicts (LINQ to SQL)/  
        }
    }  
}  
```  
  
 Para atualizar uma coleção, chame <xref:System.Data.Linq.ITable.AttachAll%2A> em vez de `Attach`.  
  
### <a name="expected-entity-members"></a>Membros esperados de entidade  

 Conforme observado anteriormente, somente certos membros do objeto de entidade são necessários ser definidos antes de chamar os métodos de `Attach` . Membros de entidade que são necessários devem ser definidos atender aos seguintes critérios:  
  
- É parte da identidade de entidade.  
  
- É esperado ser alterado.  
  
- É um carimbo de data/hora ou tem o atributo de <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> definido como algo além de `Never`.  
  
 Se uma tabela usa um carimbo de data/hora ou número de versão para uma verificação de simultaneidade otimista, você deve definir esses membros antes de chamar <xref:System.Data.Linq.ITable.Attach%2A>. Um membro é dedicado para concorrência otimista verificando quando a propriedade de <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> é definida para retificar no atributo de coluna. Todas as atualizações solicitadas serão enviadas somente se os valores de número de versão ou de carimbo de data/hora são os mesmos na base de dados.  
  
 Um membro é usado também na verificação de simultaneidade otimista do membro não tem <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> definido como `Never`. O valor padrão é `Always` se nenhum outro valor é especificado.  
  
 Se qualquer um desses membros necessários estiver faltando, <xref:System.Data.Linq.ChangeConflictException> é acionada durante <xref:System.Data.Linq.DataContext.SubmitChanges%2A> a linha (“não encontrado ou alterado”).  
  
### <a name="state"></a>Estado  

 Depois que um objeto de entidade é conectado à instância de <xref:System.Data.Linq.DataContext> , o objeto é considerado estar no estado de `PossiblyModified` . Existem três maneiras para forçar um objeto anexado a ser considerado `Modified`.  
  
1. Como anexá-lo inalterados, e então altere-o diretamente os campos.  
  
2. Anexa com a sobrecarga de <xref:System.Data.Linq.Table%601.Attach%2A> que recebe a atuais e originais instâncias de objeto. Isso fornece o perseguidor de alteração com valores antigo e novo de modo que sabe como automaticamente campos que foram alterados.  
  
3. Anexa com a sobrecarga de <xref:System.Data.Linq.Table%601.Attach%2A> que leva um segundo parâmetro boolean (definido para retificar). Isso dirá o perseguidor de alteração para ver o objeto alterado sem ter que fornecer os valores originais. Nessa abordagem, o objeto deve ter um campo de versão/carimbo de data/hora.  
  
 Para obter mais informações, consulte [Estados de objetos e controle de alterações](object-states-and-change-tracking.md).  
  
 Se um objeto de entidade já ocorre no cache de identificação com a mesma identidade que o objeto sendo anexado, <xref:System.Data.Linq.DuplicateKeyException> é lançada.  
  
 Quando você anexa com `IEnumerable` conjunto de objetos, <xref:System.Data.Linq.DuplicateKeyException> é acionada quando uma chave já existente estiver presente. Os objetos restantes não estão conectados.  
  
## <a name="see-also"></a>Consulte também

- [Aplicativos de n camadas e remoto com LINQ to SQL](n-tier-and-remote-applications-with-linq-to-sql.md)
- [Informações gerais](background-information.md)
