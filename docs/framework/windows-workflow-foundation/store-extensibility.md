---
description: 'Saiba mais sobre: armazenar extensibilidade'
title: Extensibilidade de Store
ms.date: 03/30/2017
ms.assetid: 7c3f4a46-4bac-4138-ae6a-a7c7ee0d28f5
ms.openlocfilehash: f04c466224aacd1c8f755e7aa60b18846d0c7180
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755220"
---
# <a name="store-extensibility"></a>Extensibilidade de Store

<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> permite que os usuários elevem o personalizado, as propriedades específicas do aplicativo que podem ser usadas para consultar instâncias na base de dados de persistência. O ato de elevar uma propriedade faz com que o valor esteja disponível em uma exibição especial na base de dados. Essas propriedades elevadas (propriedades que podem ser usadas em consultas de usuário) podem ser de tipos simples como Int64, GUID, cadeia de caracteres, e DateTime ou tipo binário serializado (byte []).

A classe de <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> tem o método de <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.Promote%2A> que você pode usar para elevar uma propriedade como uma propriedade que pode ser usada em consultas. O exemplo a seguir é um exemplo de ponta a ponta de extensibilidade de armazenamento.

1. Neste cenário exemplo, um aplicativo de (DP) de processamento de documento tem fluxos de trabalho, cada um deless use atividades personalizadas para processamento de documento. Esses fluxos de trabalho têm um conjunto de variáveis de estado que precisam ser feitos visíveis para o usuário final. Para obter isso, o aplicativo de DP fornece uma extensão da instância do tipo <xref:System.Activities.Persistence.PersistenceParticipant>, que é usado por atividades para fornecer variáveis de estado.

    ```csharp
    class DocumentStatusExtension : PersistenceParticipant
    {
        public string DocumentId;
        public string ApprovalStatus;
        public string UserName;
        public DateTime LastUpdateTime;
    }
    ```

2. A nova extensão é adicionada para o host.

    ```csharp
    static Activity workflow = CreateWorkflow();
    WorkflowApplication application = new WorkflowApplication(workflow);
    DocumentStatusExtension documentStatusExtension = new DocumentStatusExtension ();
    application.Extensions.Add(documentStatusExtension);
    ```

     Para obter mais detalhes sobre como adicionar um participante de persistência personalizado, consulte o exemplo [participantes de persistência](persistence-participants.md) .

3. As atividades personalizadas no aplicativo DP populam vários campos de status no método **Execute** .

    ```csharp
    public override void Execute(CodeActivityContext context)
    {
        // ...
        context.GetExtension<DocumentStatusExtension>().DocumentId = Guid.NewGuid();
        context.GetExtension<DocumentStatusExtension>().UserName = "John Smith";
        context.GetExtension<DocumentStatusExtension>().ApprovalStatus = "Approved";
        context.GetExtension<DocumentStatusExtension>().LastUpdateTime = DateTime.Now();
        // ...
    }
    ```

4. Quando uma instância de fluxo de trabalho atinge um ponto de persistência, o método **CollectValues** do participante de persistência **DocumentStatusExtension** salva essas propriedades na coleção de dados de persistência.

    ```csharp
    class DocumentStatusExtension : PersistenceParticipant
    {
        const XNamespace xNS = XNamespace.Get("http://contoso.com/DocumentStatus");

        protected override void CollectValues(out IDictionary<XName, object> readWriteValues, out IDictionary<XName, object> writeOnlyValues)
        {
            readWriteValues = new Dictionary<XName, object>();
            readWriteValues.Add(xNS.GetName("UserName"), this.UserName);
            readWriteValues.Add(xNS.GetName("ApprovalStatus"), this.ApprovalStatus);
            readWriteValues.Add(xNS.GetName("DocumentId"), this.DocumentId);
            readWriteValues.Add(xNS.GetName("LastModifiedTime"), this.LastUpdateTime);

            writeOnlyValues = null;
        }
        // ...
    }
    ```

    > [!NOTE]
    > Todas essas propriedades são passadas para **SqlWorkflowInstanceStore** pela estrutura de persistência por meio da coleção **SaveWorkflowCommand. InstanceData** .

5. O aplicativo de DP Inicializa o repositório da instância do fluxo de trabalho SQL e invoca o método **Promote** para promover esses dados.

    ```csharp
    SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore(connectionString);

    List<XName> variantProperties = new List<XName>()
    {
        xNS.GetName("UserName"),
        xNS.GetName("ApprovalStatus"),
        xNS.GetName("DocumentId"),
        xNS.GetName("LastModifiedTime")
    };

    store.Promote("DocumentStatus", variantProperties, null);
    ```

    Com base nessas informações de promoção, **SqlWorkflowInstanceStore** coloca as propriedades de dados nas colunas da exibição [InstancePromotedProperties](#InstancePromotedProperties) .

6. Para ver um subconjunto dos dados da tabela da promoção, o aplicativo de DP adiciona um modo de exibição personalizado no modo da promoção.

    ```sql
    create view [dbo].[DocumentStatus] with schemabinding
    as
        select  P.[InstanceId] as [InstanceId],
            P.Value1 as [UserName],
            P.Value2 as [ApprovalStatus],
            P.Value3 as [DocumentId],
            P.Value4 as [LastUpdatedTime]
    from [System.Activities.DurableInstancing].[InstancePromotedProperties] as P
    where P.PromotionName = N'DocumentStatus'
    go
    ```

## <a name="systemactivitiesdurableinstancinginstancepromotedproperties-view"></a><a name="InstancePromotedProperties"></a> [System. Activities. DurableInstancing. InstancePromotedProperties] exibição

|Nome da coluna|Tipo de coluna|Descrição|
|-----------------|-----------------|-----------------|
|InstanceId|GUID|A instância de fluxo de trabalho que essa promoção pertence.|
|PromotionName|nvarchar (400)|O nome da promoção próprio.|
|Valor1, valor2, Value3. , Value32|sql_variant|O valor da propriedade promovida próprio. A maioria dos tipos de dados primitivos SQL exceto gotas binários e cadeias de caracteres sobre 8000 bytes de comprimento podem caber em sql_variant.|
|Value33, Value34, Value35,…, Value64|varbinary(max)|O valor das propriedades elevadas que são explicitamente declaradas como varbinary (máximo).|
