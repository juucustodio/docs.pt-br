---
description: 'Saiba mais sobre: Estados de objeto e Change-Tracking'
title: Estados e controle de alterações de objeto
ms.date: 03/30/2017
ms.assetid: 7a808b00-9c3c-479a-aa94-717280fefd71
ms.openlocfilehash: 5f3aa6197fa44d8b5ea9333c85255202cbfe519b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695496"
---
# <a name="object-states-and-change-tracking"></a>Estados e controle de alterações de objeto

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] os objetos sempre participam de algum *estado*. Por exemplo, quando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] cria um novo objeto, o objeto está no estado de `Unchanged` . Um novo objeto que você mesmo cria é desconhecido para o <xref:System.Data.Linq.DataContext> e está em `Untracked` estado. Após a execução com êxito de <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, todos os objetos conhecidos a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] estão no estado de `Unchanged` . (A única exceção é representada por aqueles que foram excluídas com êxito de base de dados, que estão no estado de `Deleted` e inutilizável que a instância de <xref:System.Data.Linq.DataContext> .)

## <a name="object-states"></a>Estados de objeto

A tabela a seguir lista os estados possíveis para objetos de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] .

|Estado|Descrição|
|-----------|-----------------|
|`Untracked`|Um objeto não controlado por [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Os exemplos incluem o seguinte:<br /><br /> -Um objeto não consultado por meio do atual <xref:System.Data.Linq.DataContext> (como um objeto recém-criado).<br />-Um objeto criado por meio de desserialização<br />-Um objeto consultado por um diferente <xref:System.Data.Linq.DataContext> .|
|`Unchanged`|Um objeto retornado usando <xref:System.Data.Linq.DataContext> atual e não conhecido para ter sido alterado desde que ele foi criado.|
|`PossiblyModified`|Um objeto que é *anexado* a um <xref:System.Data.Linq.DataContext> . Para obter mais informações, consulte [operações de recuperação de dados e cud em aplicativos de N camadas (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md).|
|`ToBeInserted`|Um objeto não recuperado usando <xref:System.Data.Linq.DataContext>atual. Isso faz com que um base de dados `INSERT` durante <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.|
|`ToBeUpdated`|Um objeto conhecido para ter sido alterado desde que ele foi recuperado. Isso faz com que um base de dados `UPDATE` durante <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.|
|`ToBeDeleted`|Um objeto marcado para exclusão, causando um base de dados `DELETE` durante <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.|
|`Deleted`|Um objeto que é excluído na base de dados. Esse estado é final e não permite transições adicionais.|

## <a name="inserting-objects"></a>Inserindo objetos

Você pode solicitar `Inserts` explicitamente usando <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>. Como alternativa, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] é possível inferir `Inserts` localizando objetos conectados a um dos objetos conhecidos que devem ser atualizados. Por exemplo, se você adicionar um `Untracked` objeto a um <xref:System.Data.Linq.EntitySet%601> ou definir um <xref:System.Data.Linq.EntityRef%601> para um `Untracked` objeto, tornará o `Untracked` objeto acessível por meio de objetos rastreados no grafo. Durante <xref:System.Data.Linq.DataContext.SubmitChanges%2A> o processamento, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o percorre os objetos rastreados e descobre quaisquer objetos persistentes acessíveis que não são rastreados. Esses objetos são candidatos para inserção na base de dados.

Para classes em uma hierarquia de herança, <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> ( `o` ) também define o valor do membro designado como *discriminador* para corresponder ao tipo do objeto `o` . No caso de um tipo que corresponde ao valor padrão de discriminador, esta ação faz com que o valor de discriminador a ser substituído com o valor padrão. Para obter mais informações, consulte [suporte à herança](inheritance-support.md).

> [!IMPORTANT]
> Um objeto adicionado a `Table` não estiver no cache de identidade. O cache de identidade reflete somente o que é recuperado de base de dados. Após uma chamada a <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>, a entidade adicionada não aparece em consultas na base de dados até que <xref:System.Data.Linq.DataContext.SubmitChanges%2A> está concluída com êxito.

## <a name="deleting-objects"></a>Excluindo objetos

Você marca um objeto acompanhado `o` para exclusão chamando <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>() no <xref:System.Data.Linq.Table%601>apropriado. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] considera a remoção de um objeto de uma <xref:System.Data.Linq.EntitySet%601> operação de atualização e o valor de chave estrangeira correspondente é definido como nulo. O destino da operação (`o`) não é excluído da tabela. Por exemplo, `cust.Orders.DeleteOnSubmit(ord)` indica uma atualização onde a relação entre `cust` e `ord` está separada definindo a chave estrangeira `ord.CustomerID` para nulo. Não faz com que a exclusão da linha que corresponde a `ord`.

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] executa o seguinte processamento quando um objeto é excluído ( <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> ) de sua tabela:

- Quando <xref:System.Data.Linq.DataContext.SubmitChanges%2A> é chamado, uma operação de `DELETE` é executada para esse objeto.

- Remoção não é propagada a objetos relacionados independentemente se eles são carregados. Especificamente, os objetos relacionados não são carregados atualizar a propriedade de relacionamento.

- Após a execução bem-sucedida de <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, os objetos são definidos no estado de `Deleted` . Como resultado, você não pode usar o objeto ou seu `id` nesse <xref:System.Data.Linq.DataContext>. O cache interno mantido por uma instância de <xref:System.Data.Linq.DataContext> não elimina os objetos que são recuperados ou adicionados como novas, mesmo após os objetos foram excluídos na base de dados.

Você pode chamar <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> somente em um objeto controlado por <xref:System.Data.Linq.DataContext>. Para um objeto de `Untracked` , você deve chamar <xref:System.Data.Linq.Table%601.Attach%2A> antes de chamar <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>. A chamada <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> em um objeto de `Untracked` gerencie uma exceção.

> [!NOTE]
> A remoção de um objeto de uma tabela diz [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para gerar um `DELETE` comando SQL correspondente no momento do <xref:System.Data.Linq.DataContext.SubmitChanges%2A> . Esta ação não remove o objeto de cache ou não propaga a exclusão a objetos relacionados.
>
> Para recuperar `id` de um objeto excluído, use uma nova instância de <xref:System.Data.Linq.DataContext> . Para a limpeza de objetos relacionados, você pode usar o recurso de *exclusão em cascata* do banco de dados ou excluir manualmente os objetos relacionados.
>
> Os objetos relacionados não precisam ser excluídos em qualquer encomenda especial (em oposição na base de dados).

## <a name="updating-objects"></a>Atualizando objetos

Você pode detectar `Updates` observando notificações de alterações. As notificações são fornecidas com o evento de <xref:System.ComponentModel.INotifyPropertyChanging.PropertyChanging> em definidores de propriedade. Quando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] é notificado da primeira alteração em um objeto, cria uma cópia do objeto e considera o objeto um candidato para gerar uma instrução de `Update` .

Para objetos que não são implementados <xref:System.ComponentModel.INotifyPropertyChanging> , [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o mantém uma cópia dos valores que os objetos tinham quando foram materializados pela primeira vez. Quando você chama <xref:System.Data.Linq.DataContext.SubmitChanges%2A> , [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o compara os valores atual e original para decidir se o objeto foi alterado.

Para atualizações para relações, a referência de filho ao pai (ou seja, a referência que corresponde à chave estrangeira) é considerada a autoridade. A referência na direção invertida (isto é, pai para o filho) é opcional. As classes de relacionamento (<xref:System.Data.Linq.EntitySet%601> e <xref:System.Data.Linq.EntityRef%601>) garantem que as referências bidirecionais são consistentes para para muitos e relacionamento um-para-um. Se o modelo de objeto não usa <xref:System.Data.Linq.EntitySet%601> ou <xref:System.Data.Linq.EntityRef%601>, e se a referência invertido estiver presente, é de sua responsabilidade mantê-la consistente com a referência direta ao relacionamento é atualizada.

Se você atualizar a referência ambos necessário e a chave estrangeira correspondente, você deve certificar-se que concordam. Uma exceção de <xref:System.InvalidOperationException> é lançada se os dois não são sincronizados momento em que você chamar <xref:System.Data.Linq.DataContext.SubmitChanges%2A>. Embora as alterações de valor de chave estrangeira são suficientes para afetar uma atualização de linha base, você deve alterar a referência para manter a conectividade do grafo de objeto e consistência bidirecional relações.

## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
- [Operações de inserção, atualização e exclusão](insert-update-and-delete-operations.md)
