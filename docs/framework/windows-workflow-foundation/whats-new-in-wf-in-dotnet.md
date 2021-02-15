---
title: O que há de novo na Windows Workflow Foundation no .NET Framework 4,5
description: Windows Workflow Foundation no .NET Framework 4,5 apresenta muitos recursos novos, como novas atividades, recursos de designer e modelos de desenvolvimento de fluxo de trabalho.
ms.date: 03/30/2017
ms.assetid: 195c43a8-e0a8-43d9-aead-d65a9e6751ec
ms.openlocfilehash: 0d7086fd5ff9bfa410568a74092be3e29f732e23
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95697903"
---
# <a name="whats-new-in-windows-workflow-foundation-in-net-framework-45"></a>O que há de novo na Windows Workflow Foundation no .NET Framework 4,5

O Windows Workflow Foundation (WF) no .NET Framework 4,5 apresenta muitos recursos novos, como novas atividades, recursos de designer e modelos de desenvolvimento de fluxo de trabalho. Muitos, mas nem todos, dos novos recursos de fluxo de trabalho introduzidos no .NET Framework 4,5 têm suporte no designer de fluxo de trabalho hospedado novamente. Para obter mais informações sobre os novos recursos com suporte, consulte [suporte para novos recursos do Workflow Foundation 4,5 no designer de fluxo de trabalho rehospedado](wf-features-in-the-rehosted-workflow-designer.md). Para obter mais informações sobre como migrar .NET Framework 3,0 e .NET Framework aplicativos de fluxo de trabalho 3,5 para usar a versão mais recente, consulte [diretrizes de migração](migration-guidance.md). Este artigo fornece uma visão geral dos novos recursos de fluxo de trabalho introduzidos no .NET Framework 4,5.

> [!WARNING]
> Os novos recursos do Windows Workflow Foundation introduzidos no .NET Framework 4,5 não estão disponíveis para projetos destinados a versões anteriores do Framework. Se um projeto que tem como alvo .NET Framework 4,5 for Redirecionado para uma versão anterior do Framework, vários problemas poderão ocorrer.
>
> - As expressões C# serão substituídas no designer com o **valor Message definido em XAML**.
> - Muitos erros de compilação ocorrerão, incluindo o seguinte.
>
> **O formato de arquivo não é compatível com a estrutura de destino atual. Para converter o formato de arquivo, salve explicitamente o arquivo. Essa mensagem de erro desaparecerá depois que você salvar o arquivo e reabrir o designer.**

## <a name="workflow-versioning"></a><a name="BKMK_Versioning"></a> Controle de versão do fluxo de trabalho

O .NET Framework 4,5 introduziu vários novos recursos de controle de versão com base na nova <xref:System.Activities.WorkflowIdentity> classe. O <xref:System.Activities.WorkflowIdentity> fornece a autores de aplicativo de fluxo de trabalho um mecanismo para mapear uma instância de fluxo de trabalho persistida com sua definição.

- Os desenvolvedores que usam a hospedagem do <xref:System.Activities.WorkflowApplication> podem usar o <xref:System.Activities.WorkflowIdentity> para habilitar hospedagem de várias versões de um fluxo de trabalho lado a lado. As instâncias de fluxo de trabalho persistidas podem ser carregadas usando a nova classe <xref:System.Activities.WorkflowApplicationInstance> e, em seguida, o <xref:System.Activities.WorkflowApplicationInstance.DefinitionIdentity%2A> pode ser usado pelo host para fornecer a versão correta da definição de fluxo de trabalho ao criar uma instância do <xref:System.Activities.WorkflowApplication>. Para obter mais informações, consulte [usando a WorkflowIdentity e o controle de versão](using-workflowidentity-and-versioning.md) e [como hospedar várias versões de um fluxo de trabalho lado a lado](how-to-host-multiple-versions-of-a-workflow-side-by-side.md).

- O <xref:System.ServiceModel.WorkflowServiceHost> agora é um host de várias versões. Quando uma nova versão de um serviço de fluxo de trabalho é implantada, as novas instâncias são criadas usando o novo serviço, mas as instâncias existentes continuam usando a versão anterior. Para obter mais informações, consulte [controle de versão lado a lado no WorkflowServiceHost](../wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md).

- A atualização dinâmica é introduzida, o que fornece um mecanismo para atualizar a definição de uma instância de fluxo de trabalho persistida. Para obter mais informações, consulte [atualização dinâmica](dynamic-update.md) e [como: atualizar a definição de uma instância de fluxo de trabalho em execução](how-to-update-the-definition-of-a-running-workflow-instance.md).

- Um script de banco de dados SqlWorkflowInstanceStoreSchemaUpgrade. SQL é fornecido para atualizar bancos de dados de persistência criados usando os .NET Framework 4 scripts de banco de dados. Esse script atualiza .NET Framework 4 bancos de dados de persistência para dar suporte aos novos recursos de controle de versão introduzidos no .NET Framework 4,5. As instâncias de fluxo de trabalho persistidas no banco de dados recebem valores padrão do controle de versão e podem participar da execução lado a lado e da atualização dinâmica. Para obter mais informações, consulte [Upgrading .NET Framework 4 bancos de dados de persistência para dar suporte ao controle de versão de fluxo de trabalho](using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases).

## <a name="activities"></a><a name="BKMK_NewActivities"></a> As

A biblioteca de atividades embutida contém novas atividades e novos recursos para atividades existentes.

### <a name="nopersist-scope"></a><a name="BKMK_NoPersistScope"></a> Escopo de nopersist

<xref:System.Activities.Statements.NoPersistScope> é uma nova atividade do contêiner que impede que um fluxo de trabalho seja persistido quando as atividades filhos do NoPersistScope estiverem em execução. Isso é útil em cenários onde não é apropriado para o fluxo de trabalho ser persistido, como quando o fluxo de trabalho estiver usando recursos específicos de computadores como os identificadores de arquivos ou durante as transações de banco de dados. Anteriormente, para impedir que a persistência ocorresse durante a execução de uma atividade, um <xref:System.Activities.NativeActivity> personalizado que usava <xref:System.Activities.NoPersistHandle> era necessário.

### <a name="new-flowchart-capabilities"></a><a name="BKMK_NewFlowchartCapabilities"></a> Novos recursos de fluxograma

Os fluxogramas são atualizados para o .NET Framework 4,5 e têm os seguintes novos recursos:

- A propriedade `DisplayName` de uma atividade <xref:System.Activities.Statements.FlowSwitch%601> ou <xref:System.Activities.Statements.FlowDecision> é editável. Isso permitirá que o designer de atividade mostre mais informações sobre a finalidade da atividade.

- Os fluxogramas têm uma nova propriedade chamada <xref:System.Activities.Statements.Flowchart.ValidateUnconnectedNodes%2A>; o padrão para essa propriedade é `False`. Se essa propriedade for definida como `True`, os nós de fluxograma desconectados gerarão erros de validação.

## <a name="support-for-partial-trust"></a>Suporte para confiança parcial

Os fluxos de trabalho no .NET Framework 4 exigiam um domínio de aplicativo totalmente confiável. No .NET Framework 4,5, os fluxos de trabalho podem operar em um ambiente de confiança parcial. Em um ambiente de confiança parcial, os componentes de terceiros podem ser usados sem conceder a eles acesso completo aos recursos do host. Algumas preocupações sobre fluxos de trabalho em execução em confiança parcial são as seguintes:

1. Usar os componentes legados (incluindo regras) contidos na atividade <xref:System.Activities.Statements.Interop> não tem suporte em confiança parcial.

2. Fluxos de trabalho em execução em confiança parcial no <xref:System.ServiceModel.WorkflowServiceHost> não têm suporte.

3. Manter exceções em um cenário de confiança parcial é uma ameaça potencial de segurança. Para desabilitar a persistência de exceções, uma extensão do tipo <xref:System.Activities.ExceptionPersistenceExtension> deve ser adicionada ao projeto para deixar de persistir exceções. O exemplo de código a seguir demonstra como implementar esse tipo.

    ```csharp
    public class ExceptionPersistenceExtension
    {
        public ExceptionPersistenceExtension()
        {
            this.PersistExceptions = false;
        }
        public bool PersistExceptions { get; set; }
    }
    ```

     Se as exceções não tiverem que ser serializadas, verifique se as exceções são usadas dentro de um <xref:System.Activities.Statements.NoPersistScope>.

4. Os autores de atividade devem substituir <xref:System.Activities.Activity.CacheMetadata%2A> para evitar que o runtime de fluxo de trabalho execute automaticamente a reflexão em relação ao tipo. Os argumentos e as atividades filho devem ser não null e <xref:System.Activities.ActivityMetadata.Bind%2A> deve ser chamado explicitamente. Para obter mais informações sobre substituição <xref:System.Activities.Activity.CacheMetadata%2A> , consulte [expondo dados com CacheMetadata](exposing-data-with-cachemetadata.md). Além disso, as instâncias de argumentos que são de um tipo que é `internal` ou **privado** devem ser explicitamente criadas no  <xref:System.Activities.Activity.CacheMetadata%2A> para evitar que sejam criadas pela reflexão.

5. Os tipos não usarão <xref:System.Runtime.Serialization.ISerializable> ou <xref:System.SerializableAttribute> para serialização; os tipos que tiverem que ser serializados devem oferecer suporte a <xref:System.Runtime.Serialization.DataContractSerializer>.

6. Expressões que usam <xref:System.Activities.Expressions.LambdaValue%601> exigem <xref:System.Security.Permissions.ReflectionPermissionAttribute.RestrictedMemberAccess%2A> e, dessa forma, não funcionarão em confiança parcial. Os fluxos de trabalho que usam <xref:System.Activities.Expressions.LambdaValue%601> devem substituir essas expressões pelas atividades que derivam de <xref:System.Activities.CodeActivity%601>. .

7. As expressões não podem ser criadas com <xref:System.Activities.XamlIntegration.TextExpressionCompiler> ou o compilador hospedado do Visual Basic em confiança parcial, mas as expressões criadas anteriormente podem ser executadas.

8. Um único assembly que usa a [transparência de nível 2](../misc/security-transparent-code-level-2.md) não pode ser usado no .NET Framework 4, [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] em confiança total e [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] em confiança parcial.

## <a name="new-designer-capabilities"></a><a name="BKMK_NewDesignerCapabilites"></a> Novos recursos do designer

### <a name="designer-search"></a><a name="BKMK_DesignerSearch"></a> Pesquisa de designer

Para tornar os fluxos de trabalho maiores mais gerenciáveis, os fluxos de trabalho podem agora ser pesquisados por palavra-chave. Este recurso só está disponível no Visual Studio; Esse recurso não está disponível em um designer rehospedado. Há dois tipos de pesquisas disponível:

- Localização rápida, iniciada com **Ctrl + F** ou **Editar**, **Localizar e substituir**, **localização rápida**.

- Localizar em arquivos, iniciados com **Ctrl + Shift + F** ou **Editar**, **Localizar e substituir**, **Localizar em arquivos**.

Observe que Substituir não tem suporte.

#### <a name="quick-find"></a><a name="BKMK_QuickFind"></a> Localização rápida

As palavras-chave pesquisadas em fluxos de trabalho corresponderão aos seguintes itens do designer:

- Propriedades de objetos <xref:System.Activities.Activity>, <xref:System.Activities.Statements.FlowNode>, <xref:System.Activities.Statements.State>, <xref:System.Activities.Statements.Transition> e outros itens de controle de fluxo personalizado.

- Variáveis

- Argumentos

- Expressões

A Localização Rápida é executada na árvore do <xref:System.Activities.Presentation.Model.ModelItem> do designer. A Localização Rápida não localizará namespaces importados na definição de fluxo de trabalho.

#### <a name="find-in-files"></a><a name="BKMK_FindInFiles"></a> Localizar nos arquivos

As palavras-chave pesquisadas em fluxos de trabalho coincidirão com o conteúdo real dos arquivos de fluxo de trabalho. Os resultados da pesquisa serão mostrados no painel de exibição Localizar Resultados do Visual Studio. Clicar duas vezes no item de resultado navegará até a atividade que contém a correspondência no designer de fluxo de trabalho.

### <a name="delete-context-menu-item-in-variable-and-argument-designer"></a><a name="BKMK_VariableDeleteContextMenu"></a> Excluir item de menu de contexto em Designer de argumento e de variável

No .NET Framework 4, variáveis e argumentos só podem ser excluídos no designer usando o teclado. A partir do .NET Framework 4,5, variáveis e argumentos podem ser excluídos usando o menu de contexto.

A captura de tela a seguir mostra o menu de contexto do designer de variável e argumento.

![Menu de contexto do designer de argumento e variável](./media/whats-new-in-wf-in-dotnet/designer-context-menu.png)

### <a name="auto-surround-with-sequence"></a><a name="BKMK_AutoSurround"></a> Surround automático com sequência

Como um fluxo de trabalho ou algumas atividades do contêiner (como <xref:System.Activities.Statements.NoPersistScope>) só podem conter uma única atividade do corpo, adicionar uma segunda atividade exigia que o desenvolvedor excluísse a primeira atividade, adicionasse uma atividade <xref:System.Activities.Statements.Sequence> e, em seguida, adicionasse as duas atividades para a atividade de sequência. A partir do .NET Framework 4,5, ao adicionar uma segunda atividade à superfície do designer, uma `Sequence` atividade será criada automaticamente para encapsular as duas atividades.

A captura de tela a seguir mostra uma atividade de `WriteLine` no `Body` de um `NoPersistScope`.

![Uma atividade WriteLine no corpo de uma atividade NoPersistScope.](./media/whats-new-in-wf-in-dotnet/auto-surround-write-line-activity.png)

A captura de tela a seguir mostra a atividade de `Sequence` criada automaticamente no `Body` quando um segundo `WriteLine` é solto abaixo do primeiro.

![Uma sequência criada automaticamente no corpo de um NoPersistScope.](./media/whats-new-in-wf-in-dotnet/auto-surround-sequence-activity.png)

### <a name="pan-mode"></a><a name="BKMK_PanMode"></a> Modo panorâmico

Para navegar mais facilmente um grande fluxo de trabalho no designer, o modo panorâmico pode ser habilitado, permitindo que o desenvolvedor clique e arraste para mover a parte visível do fluxo de trabalho, em vez de precisar usar as barras de rolagem. O botão para ativar o modo de superfície está no canto inferior direito do designer.

A captura de tela a seguir mostra o botão de panorâmica qual está localizado no canto inferior direito do designer de fluxo de trabalho.

![O botão de panorâmica realçado no designer de fluxo de trabalho.](./media/whats-new-in-wf-in-dotnet/pan-button-workflow-designer.png)

O botão do meio do mouse ou a barra de espaço também podem ser usados para executar uma panorâmica do designer de fluxo de trabalho.

### <a name="multi-select"></a><a name="BKMK_MultiSelect"></a> Seleção múltipla

Várias atividades podem ser selecionadas ao mesmo tempo, arrastando um retângulo ao redor delas (quando o modo panorâmico não está habilitado), ou mantendo pressionada a tecla CTRL e clicando nas atividades desejadas.

Várias seleções de atividade também podem ser arrastadas e soltadas dentro do designer, e também podem ser interagidas usando o menu de contexto.

### <a name="outline-view-of-workflow-items"></a><a name="BKMK_DocumentOutline"></a> modo de exibição da Estrutura do Código de itens de fluxo de trabalho

Para facilitar a navegação de fluxos de trabalho hierárquicos, os componentes de um fluxo de trabalho são mostrados em uma exibição de destaque em estilo de árvore. O modo de exibição de estrutura de tópicos é exibido na exibição de **estrutura de tópicos do documento** . Para abrir essa exibição, no menu superior, selecione **exibição**, **outras janelas**, **estrutura de tópicos do documento** ou pressione CTRL +, U. Clicar em um nó na exibição de destaque navegará para a atividade correspondente no designer de fluxo de trabalho, e a exibição da estrutura será atualizada para mostrar as atividades que estão selecionadas no designer.

A seguinte captura de tela do fluxo de trabalho concluído do [tutorial de introdução](getting-started-tutorial.md) mostra o modo de exibição de estrutura de tópicos com um fluxo de trabalho Sequencial.

![Captura de tela da exibição de estrutura de tópicos com um fluxo de trabalho Sequencial no Visual Studio.](./media/whats-new-in-wf-in-dotnet/outline-view-in-workflow-designer.jpg)

### <a name="c-expressions"></a><a name="BKMK_CSharpExpressions"></a> Expressões C#

Antes do .NET Framework 4,5, todas as expressões em fluxos de trabalho só podiam ser gravadas em Visual Basic. No .NET Framework 4,5, Visual Basic expressões são usadas somente para projetos criados usando Visual Basic. Os projetos do Visual C# agora usam o C# para expressões. Um editor de expressão C# completamente funcional é fornecido com recursos como realce de gramática e intellisense. Os projetos do fluxo de trabalho C# criados em versões anteriores que usam expressões do Visual Basic continuarão funcionando.

As expressões C# são validadas em tempo de design. Os erros em expressões C# serão marcados com um sublinhado vermelho ondulado.

Para obter mais informações sobre expressões C#, consulte [expressões c#](csharp-expressions.md).

### <a name="more-control-of-visibility-of-shell-bar-and-header-items"></a><a name="BKMK_Visibility"></a> Mais controle da visibilidade de itens de cabeçalho e barra do Shell

Em um designer hospedado novamente, alguns dos controles padrão de interface do usuário não podem ter o significado de um fluxo de trabalho específico, e podem ser desativados. No .NET Framework 4, essa personalização só é suportada pela barra de Shell na parte inferior do designer. No .NET Framework 4,5, a visibilidade dos itens de cabeçalho do Shell na parte superior do designer pode ser ajustada Configurando <xref:System.Activities.Presentation.View.DesignerView.WorkflowShellHeaderItemsVisibility%2A> com o <xref:System.Activities.Presentation.View.ShellHeaderItemsVisibility> valor apropriado.

### <a name="auto-connect-and-auto-insert-in-flowchart-and-state-machine-workflows"></a><a name="BKMK_AutoConnect"></a> Conexão automática e inserção automática em fluxos de trabalho do fluxograma e da máquina de estado

No .NET Framework 4, as conexões entre os nós em um fluxo de trabalho de fluxograma tinham que ser adicionadas manualmente. No .NET Framework 4,5, os nós de máquina de estado e fluxograma têm pontos de conexão automática que se tornam visíveis quando uma atividade é arrastada da caixa de ferramentas para a superfície do designer. Soltar uma atividade em um destes pontos adiciona automaticamente a atividade junto com a conexão necessária.

A captura de tela a seguir mostra os pontos de anexação que ficam visíveis quando uma atividade é arrastada da caixa de ferramentas.

![Nó de início do fluxograma mostrando pontos de conexão automática](./media/whats-new-in-wf-in-dotnet/auto-connect-points-start-node.png)

As atividades também podem ser arrastadas em conexões entre nós de fluxograma e estados para inserção automática do nó entre dois outros nós. A captura de tela a seguir mostra a linha de conexão realçada em que as atividades podem ser arrastadas da caixa de ferramentas e soltas.

![Identificador de inserção automática para soltar atividades](./media/whats-new-in-wf-in-dotnet/auto-insert-connecting-line.png)

### <a name="designer-annotations"></a><a name="BKMK_Annotations"></a> Anotações do designer

Para facilitar o desenvolvimento de fluxos de trabalho maiores, o designer agora permite adicionar anotações para ajudar a controlar o processo de design. A anotação pode ser adicionada a atividades, estados, nós de fluxograma, variáveis e argumentos. A captura de tela a seguir mostra o menu de contexto usado para adicionar anotações para o designer.

![Captura de tela mostrando um menu para adicionar anotações.](./media/whats-new-in-wf-in-dotnet/designer-annotations-context-menu.png)

### <a name="debugging-states"></a>Estados de depuração

No .NET Framework 4, os elementos que não são de atividade não podiam dar suporte a pontos de interrupção de depuração, pois não eram unidades de execução. Esta versão fornece um mecanismo para adicionar pontos de interrupção a objetos <xref:System.Activities.Statements.State>. Quando um ponto de interrupção for definido em um <xref:System.Activities.Statements.State>, a execução será interrompida quando ocorrer a transição do estado antes que suas atividades de entrada ou gatilhos sejam agendados.

### <a name="define-and-consume-activitydelegate-objects-in-the-designer"></a><a name="BKMK_ActivityDelegates"></a> Definir e consumir objetos ActivityDelegate no designer

As atividades em .NET Framework 4 <xref:System.Activities.ActivityDelegate> objetos usados para expor pontos de execução em que outras partes do fluxo de trabalho poderiam interagir com a execução de um fluxo de trabalho, mas usar esses pontos de execução geralmente exigia uma quantidade razoável de código. Nesta versão, os desenvolvedores podem definir e consumir representantes de atividade usando o designer de fluxo de trabalho. Para obter mais informações, consulte [como: definir e consumir delegados de atividade no designer de fluxo de trabalho](/visualstudio/workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer).

### <a name="build-time-validation"></a><a name="BKMK_BuildTimeValidation"></a> Validação de tempo de compilação

No .NET Framework 4, os erros de validação de fluxo de trabalho não foram contados como erros de compilação durante a compilação de um projeto de fluxo de trabalho. Isso significava que criar um projeto de fluxo de trabalho poderia ter êxito mesmo se houvesse erros de validação do fluxo de trabalho. No .NET Framework 4,5, os erros de validação do fluxo de trabalho fazem com que a compilação falhe.

### <a name="design-time-background-validation"></a><a name="BKMK_DesignTimeValidation"></a> Validação de segundo plano em tempo de design

No .NET Framework 4, os fluxos de trabalho foram validados como um processo em primeiro plano, o que poderia bloquear a interface do usuário durante processos de validação complexos ou demorados. A validação do fluxo de trabalho agora ocorre em um thread em segundo plano, de modo que a interface do usuário não seja bloqueada.

### <a name="view-state-located-in-a-separate-location-in-xaml-files"></a><a name="BKMK_ViewState"></a> Estado de exibição localizado em um local separado em arquivos XAML

No .NET Framework 4, as informações de estado de exibição de um fluxo de trabalho são armazenadas em todo o arquivo XAML em vários locais diferentes. Isso é inconveniente para os desenvolvedores que desejam ler XAML diretamente, ou gravar código para remover informações de estado de exibição. No .NET Framework 4,5, as informações de estado de exibição no arquivo XAML são serializadas como um elemento separado no arquivo XAML. Os desenvolvedores podem facilmente localizar e editar as informações de estado de exibição de uma atividade ou remover completamente o estado de exibição.

### <a name="expression-extensibility"></a><a name="BKMK_ExpressionExtensibility"></a> Extensibilidade de expressão

No .NET Framework 4,5, fornecemos uma maneira para os desenvolvedores criarem suas próprias expressões e a experiência de criação de expressão que pode ser conectada ao designer de fluxo de trabalho.

### <a name="opt-in-for-workflow-45-features-in-rehosted-designer"></a><a name="BKMK_BackwardCompatRehostedDesigner"></a> Aceitar recursos do Workflow 4,5 no designer rehospedado

Para preservar a compatibilidade com versões anteriores, alguns recursos novos incluídos no .NET Framework 4,5 não são habilitados por padrão no designer rehospedado. Este é para garantir que aplicativos existentes que usam o designer hospedado novamente não sejam interrompidos ao atualizar para a versão mais recente. Para habilitar novos recursos no designer hospedado novamente, defina <xref:System.Activities.Presentation.DesignerConfigurationService.TargetFrameworkName%2A> como ".NET Framework 4.5" ou defina membros individuais do conjunto de <xref:System.Activities.Presentation.DesignerConfigurationService> para habilitar recursos individuais.

## <a name="new-workflow-development-models"></a><a name="BKMK_NewWFModels"></a> Novos modelos de desenvolvimento de fluxo de trabalho

Além do fluxograma e de modelos sequenciais de desenvolvimento de fluxo de trabalho, esta versão inclui fluxos de trabalho da Máquina de Estado e serviços de fluxo de trabalho de primeiro contrato.

### <a name="state-machine-workflows"></a><a name="BKMK_StateMachine"></a> Fluxos de trabalho de máquina de estado

Os fluxos de trabalho de máquina de estado foram introduzidos como parte do .NET Framework 4, versão 4.0.1 na [atualização 1 da plataforma Microsoft .NET Framework 4](/archive/blogs/endpoint/microsoft-net-framework-4-platform-update-1). Essa atualização incluiu várias novas classes e atividades que permitiram que os desenvolvedores criassem fluxos de trabalho de máquina do estado. Essas classes e atividades foram atualizadas para o .NET Framework 4,5. As atualizações incluem:

1. A capacidade de definir pontos de interrupção em estados

2. A capacidade de copiar e colar transições no designer de fluxo de trabalho

3. Suporte de designer para criação de transição do disparador compartilhado

4. Atividades usadas para criar fluxos de trabalho da máquina de estado, incluindo: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State> e <xref:System.Activities.Statements.Transition>.

A captura de tela a seguir mostra o fluxo de trabalho de máquina de estado concluído da etapa [introdução tutorial](getting-started-tutorial.md) [como criar um fluxo de trabalho de máquina de estado](how-to-create-a-state-machine-workflow.md).

![Ilustração que mostra o fluxo de trabalho da máquina de estado concluído.](./media/whats-new-in-wf-in-dotnet/complete-state-machine-workflow.jpg)

Para saber mais sobre como criar fluxos de trabalho de máquina de estado, confira [fluxos de trabalho de máquina de estado](state-machine-workflows.md).

### <a name="contract-first-workflow-development"></a><a name="BKMK_ContractFirst"></a> Contrato-primeiro desenvolvimento de fluxo de trabalho

A ferramenta de desenvolvimento de fluxo de trabalho de primeiro contrato permite que o desenvolvedor projete um contrato no código primeiro e, com alguns cliques no Visual Studio, gere automaticamente um modelo de atividade na caixa de ferramentas que representa cada operação. Essas atividades são então usadas para criar um fluxo de trabalho que implementa as operações definidas pelo contrato. O designer de fluxo de trabalho validará o serviço de fluxo de trabalho para assegurar que essas operações sejam implementadas e a assinatura do fluxo de trabalho corresponda à assinatura do contrato. O desenvolvedor também pode associar um serviço de fluxo de trabalho a uma coleção de contratos implementados. Para obter mais informações sobre o desenvolvimento do serviço de fluxo de trabalho do primeiro contrato, consulte [como: criar um serviço de fluxo de trabalho que consome um contrato de serviço existente](how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md).
