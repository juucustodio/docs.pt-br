---
description: 'Saiba mais sobre: suporte para novos recursos do Workflow Foundation 4,5 no Designer de Fluxo de Trabalho rehospedado'
title: Suporte para novos recursos do Workflow Foundation 4.5 no Designer de Fluxo de Trabalho hospedado novamente
ms.date: 03/30/2017
ms.assetid: 1a4a4038-d8e6-41dd-99ea-93bd76286772
ms.openlocfilehash: 948519265383e9fd3850c44304f7c02283b3f579
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754999"
---
# <a name="support-for-new-workflow-foundation-45-features-in-the-rehosted-workflow-designer"></a>Suporte para novos recursos do Workflow Foundation 4.5 no Designer de Fluxo de Trabalho hospedado novamente

O Windows Workflow Foundation (WF) no .NET Framework 4,5 introduziu muitos recursos novos, incluindo vários aprimoramentos na experiência do designer de fluxo de trabalho. Este tópico detalha quais desses recursos têm suporte no designer hospedado novamente e que não têm suporte no momento.

> [!NOTE]
> Para obter uma lista de todos os novos recursos do Windows Workflow Foundation (WF) introduzidos no .NET Framework 4,5, incluindo aqueles que não estão relacionados à hospedagem do designer, consulte [novidades do Windows Workflow Foundation no .NET Framework 4,5](whats-new-in-wf-in-dotnet.md).

## <a name="activities"></a>Atividades

 A biblioteca de atividades embutida contém novas atividades e novos recursos para atividades existentes. Todas essas novas atividades têm suporte no designer hospedado novamente. Para obter mais informações sobre essas novas atividades, consulte a seção [atividades](whats-new-in-wf-in-dotnet.md#BKMK_NewActivities) do [que há de novo no Windows Workflow Foundation no .NET Framework 4,5](whats-new-in-wf-in-dotnet.md).

## <a name="c-expressions"></a>Expressões C#

 Antes do .NET Framework 4,5, todas as expressões em fluxos de trabalho só podiam ser gravadas em Visual Basic. No .NET Framework 4,5, Visual Basic expressões são usadas somente para projetos criados usando Visual Basic. Os projetos do Visual C# agora usam o C# para expressões. Ao criar fluxos de trabalho no Visual Studio 2012, um editor de expressão C# totalmente funcional fornece os recursos como realce de gramática e IntelliSense. Os projetos do fluxo de trabalho C# criados em versões anteriores que usam expressões do Visual Basic continuarão funcionando.

> [!WARNING]
> As expressões C# não têm suporte no designer hospedado novamente.

## <a name="new-designer-capabilities"></a>Novos recursos do designer

### <a name="designer-search"></a>Pesquisa do designer

 Os recursos [localização rápida](whats-new-in-wf-in-dotnet.md#BKMK_QuickFind) e [localizar nos arquivos](whats-new-in-wf-in-dotnet.md#BKMK_FindInFiles) introduzidos com o .NET Framework 4,5 não têm suporte no designer rehospedado. A pesquisa de `Toolbox` tem suporte no designer hospedado novamente. Para obter mais informações sobre esses recursos, consulte [pesquisa de designer](whats-new-in-wf-in-dotnet.md#BKMK_DesignerSearch).

> [!WARNING]
> Não há suporte para [localização rápida](whats-new-in-wf-in-dotnet.md#BKMK_QuickFind) e [localização em arquivos](whats-new-in-wf-in-dotnet.md#BKMK_FindInFiles) no designer rehospedado.

### <a name="delete-context-menu-item-in-variable-and-argument-designer"></a>Excluir item de menu de contexto no designer de argumento e variável

 No .NET Framework 4, variáveis e argumentos só podem ser excluídos no designer usando o teclado. A partir do .NET Framework 4,5, variáveis e argumentos podem ser excluídos usando o menu de contexto. Esse recurso tem suporte no designer hospedado novamente.

 A captura de tela a seguir mostra o menu de contexto do designer de variável e argumento.

 ![Menu de contexto do designer de argumento e variável](./media/wf-features-in-the-rehosted-workflow-designer/designer-context-menu.png)

### <a name="auto-surround-with-sequence"></a>Envolvimento automático com sequência

 Como um fluxo de trabalho ou algumas atividades do contêiner (como <xref:System.Activities.Statements.NoPersistScope>) só podem conter uma única atividade do corpo, adicionar uma segunda atividade exigia que o desenvolvedor excluísse a primeira atividade, adicionasse uma atividade <xref:System.Activities.Statements.Sequence> e, em seguida, adicionasse as duas atividades para a atividade de sequência. A partir do .NET Framework 4,5, ao adicionar uma segunda atividade à superfície do designer, uma `Sequence` atividade será criada automaticamente para encapsular as duas atividades. Esse recurso tem suporte no designer hospedado novamente.

 A captura de tela a seguir mostra uma atividade de `WriteLine` no `Body` de um `NoPersistScope`.

 ![Uma atividade WriteLine no corpo de uma atividade NoPersistScope.](./media/wf-features-in-the-rehosted-workflow-designer/auto-surround-write-line-activity.png)

 A captura de tela a seguir mostra a atividade de `Sequence` criada automaticamente no `Body` quando um segundo `WriteLine` é solto abaixo do primeiro.

 ![Uma sequência criada automaticamente no corpo de um NoPersistScope.](./media/wf-features-in-the-rehosted-workflow-designer/auto-surround-sequence-activity.png)

### <a name="pan-mode"></a>Modo panorâmico

 Para navegar mais facilmente um grande fluxo de trabalho no designer, o modo panorâmico pode ser habilitado, permitindo que o desenvolvedor clique e arraste para mover a parte visível do fluxo de trabalho, em vez de precisar usar as barras de rolagem. O botão para ativar o modo de superfície está no canto inferior direito do designer. Esse recurso tem suporte no designer hospedado novamente.

 A captura de tela a seguir mostra o botão de panorâmica qual está localizado no canto inferior direito do designer de fluxo de trabalho.

 ![O botão de panorâmica realçado no designer de fluxo de trabalho.](./media/wf-features-in-the-rehosted-workflow-designer/pan-button-workflow-designer.png)

 O botão do meio do mouse ou a barra de espaço também podem ser usados para executar uma panorâmica do designer de fluxo de trabalho.

### <a name="multi-select"></a>Seleção múltipla

 Várias atividades podem ser selecionadas ao mesmo tempo, arrastando um retângulo ao redor delas (quando o modo panorâmico não está habilitado), ou mantendo pressionada a tecla CTRL e clicando nas atividades desejadas. Esse recurso tem suporte no designer hospedado novamente.

 Várias seleções de atividade também podem ser arrastadas e soltadas dentro do designer, e também podem ser interagidas usando o menu de contexto.

### <a name="outline-view-of-workflow-items"></a>Exibição de destaque de itens de fluxo de trabalho

 Para facilitar a navegação de fluxos de trabalho hierárquicos, os componentes de um fluxo de trabalho são mostrados em uma exibição de destaque em estilo de árvore. O modo de exibição de estrutura de tópicos é exibido na exibição de **estrutura de tópicos do documento** . Para abrir essa exibição no Visual Studio, no menu superior, selecione **exibição**, **outras janelas**, **estrutura de tópicos do documento** ou pressione CTRL +, U. Clicar em um nó na exibição de destaque navegará para a atividade correspondente no designer de fluxo de trabalho, e a exibição da estrutura será atualizada para mostrar as atividades que estão selecionadas no designer. Esse recurso tem suporte no designer hospedado novamente.

 A seguinte captura de tela do fluxo de trabalho concluído do [tutorial de introdução](getting-started-tutorial.md) mostra o modo de exibição de estrutura de tópicos com um fluxo de trabalho Sequencial.

 ![Captura de tela da exibição de estrutura de tópicos com um fluxo de trabalho Sequencial no Visual Studio](./media/wf-features-in-the-rehosted-workflow-designer/outline-view-in-workflow-designer.jpg)

### <a name="more-control-of-visibility-of-shell-bar-and-header-items"></a>Mais controle da visibilidade da barra de shell e dos itens de cabeçalho

 Em um designer hospedado novamente, alguns dos controles padrão de interface do usuário não podem ter o significado de um fluxo de trabalho específico, e podem ser desativados. No .NET Framework 4, essa personalização só é suportada pela barra de Shell na parte inferior do designer. No .NET Framework 4,5, a visibilidade dos itens de cabeçalho do Shell na parte superior do designer pode ser ajustada Configurando <xref:System.Activities.Presentation.View.DesignerView.WorkflowShellHeaderItemsVisibility%2A> com o <xref:System.Activities.Presentation.View.ShellHeaderItemsVisibility> valor apropriado.

### <a name="auto-connect-and-auto-insert-in-flowchart-and-state-machine-workflows"></a>Conexão automática e inserção automática em fluxograma e fluxos de trabalho de máquina de estado

 No .NET Framework 4, as conexões entre os nós em um fluxo de trabalho de fluxograma tinham que ser adicionadas manualmente. No .NET Framework 4,5, os nós de máquina de estado e fluxograma têm pontos de conexão automática que se tornam visíveis quando uma atividade é arrastada da caixa de ferramentas para a superfície do designer. Soltar uma atividade em um destes pontos adiciona automaticamente a atividade junto com a conexão necessária.

 A captura de tela a seguir mostra os pontos de anexação que ficam visíveis quando uma atividade é arrastada da caixa de ferramentas.

 ![Nó de início do fluxograma mostrando pontos de conexão automática](./media/wf-features-in-the-rehosted-workflow-designer/auto-connect-points-start-node.png)

 As atividades também podem ser arrastadas em conexões entre nós de fluxograma e estados para inserção automática do nó entre dois outros nós. A captura de tela a seguir mostra a linha de conexão realçada em que as atividades podem ser arrastadas da caixa de ferramentas e soltas.

 ![Identificador de inserção automática para soltar atividades](./media/wf-features-in-the-rehosted-workflow-designer/auto-insert-connecting-line.png)

 A conexão automática e a inserção automática têm suporte no designer hospedado novamente.

### <a name="designer-annotations"></a>Anotações do designer

 Para facilitar o desenvolvimento de fluxos de trabalho maiores, o designer agora permite adicionar anotações para ajudar a controlar o processo de design. A anotação pode ser adicionada a atividades, estados, nós de fluxograma, variáveis e argumentos. A captura de tela a seguir mostra o menu de contexto usado para adicionar anotações para o designer.

 ![Captura de tela que mostra o menu para adicionar notações.](./media/wf-features-in-the-rehosted-workflow-designer/designer-annotations-context-menu.png)

 As anotações do designer não têm suporte no designer hospedado novamente.

### <a name="define-and-consume-activitydelegate-objects-in-the-designer"></a>Definir e consumir objetos ActivityDelegate no designer

 As atividades em .NET Framework 4 <xref:System.Activities.ActivityDelegate> objetos usados para expor pontos de execução em que outras partes do fluxo de trabalho poderiam interagir com a execução de um fluxo de trabalho, mas usar esses pontos de execução geralmente exigia uma quantidade razoável de código. Nesta versão, os desenvolvedores podem definir e consumir representantes de atividade usando o designer de fluxo de trabalho. Para obter mais informações, consulte [como: definir e consumir delegados de atividade no designer de fluxo de trabalho](/visualstudio/workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer).

 Os delegados de atividade não têm suporte no designer hospedado novamente.

### <a name="build-time-validation"></a>Validação de tempo de compilação

 No .NET Framework 4, os erros de validação de fluxo de trabalho não foram contados como erros de compilação durante a compilação de um projeto de fluxo de trabalho. Isso significava que criar um projeto de fluxo de trabalho poderia ter êxito mesmo se houvesse erros de validação do fluxo de trabalho. No .NET Framework 4,5, os erros de validação do fluxo de trabalho fazem com que a compilação falhe.

> [!WARNING]
> A validação de tempo de compilação não tem suporte no designer hospedado novamente.

### <a name="design-time-background-validation"></a>Validação em segundo plano do tempo de design

 No .NET Framework 4, os fluxos de trabalho foram validados como um processo em primeiro plano, o que poderia bloquear a interface do usuário durante processos de validação complexos ou demorados. A validação do fluxo de trabalho agora ocorre em um thread em segundo plano, de modo que a interface do usuário não seja bloqueada.

 A validação em segundo plano do tempo de design não tem suporte no designer hospedado novamente.

### <a name="view-state-located-in-a-separate-location-in-xaml-files"></a>Estado de exibição localizado em um local separado em arquivos XAML

 No .NET Framework 4, as informações de estado de exibição de um fluxo de trabalho são armazenadas em todo o arquivo XAML em vários locais diferentes. Isso é inconveniente para os desenvolvedores que desejam ler XAML diretamente, ou gravar código para remover informações de estado de exibição. No .NET Framework 4,5, as informações de estado de exibição no arquivo XAML são serializadas como um elemento separado no arquivo XAML.  Os desenvolvedores podem facilmente localizar e editar as informações de estado de exibição de uma atividade ou remover completamente o estado de exibição.

 Esse recurso tem suporte no designer de fluxo de trabalho hospedado novamente.

### <a name="opt-in-for-workflow-45-features-in-rehosted-designer"></a>Aceitação dos recursos do Workflow 4.5 no designer hospedado novamente

 Para preservar a compatibilidade com versões anteriores, alguns recursos novos incluídos no .NET Framework 4,5 não são habilitados por padrão no designer rehospedado. Este é para garantir que aplicativos existentes que usam o designer hospedado novamente não sejam interrompidos ao atualizar para a versão mais recente. Para habilitar novos recursos no designer hospedado novamente, defina <xref:System.Activities.Presentation.DesignerConfigurationService.TargetFrameworkName%2A> como ".NET Framework 4.5" ou defina membros individuais do conjunto de <xref:System.Activities.Presentation.DesignerConfigurationService> para habilitar recursos individuais.

## <a name="new-workflow-development-models"></a>Novos modelos de desenvolvimento de fluxo de trabalho

 Além do fluxograma e de modelos sequenciais de desenvolvimento de fluxo de trabalho, esta versão inclui fluxos de trabalho da Máquina de Estado e serviços de fluxo de trabalho de primeiro contrato.

### <a name="state-machine-workflows"></a>Fluxo de trabalho de máquina de estado

 Os fluxos de trabalho de máquina de estado foram introduzidos como parte do .NET Framework 4.0.1 na [atualização 1 da plataforma Microsoft .NET Framework 4](/archive/blogs/endpoint/microsoft-net-framework-4-platform-update-1). Essa atualização incluiu várias novas classes e atividades que permitiram que os desenvolvedores criassem fluxos de trabalho de máquina do estado. Essas classes e atividades foram atualizadas para o .NET Framework 4,5. As atualizações incluem:

1. A capacidade de definir pontos de interrupção em estados

2. A capacidade de copiar e colar transições no designer de fluxo de trabalho

3. Suporte de designer para criação de transição do disparador compartilhado

4. Atividades usadas para criar fluxos de trabalho da máquina de estado, incluindo: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State> e <xref:System.Activities.Statements.Transition>.

 A captura de tela a seguir mostra o fluxo de trabalho de máquina de estado concluído da etapa [introdução tutorial](getting-started-tutorial.md) [como criar um fluxo de trabalho de máquina de estado](how-to-create-a-state-machine-workflow.md).

 ![Ilustração que mostra o fluxo de trabalho da máquina de estado concluído.](./media/wf-features-in-the-rehosted-workflow-designer/complete-state-machine-workflow.jpg)

 Para saber mais sobre como criar fluxos de trabalho de máquina de estado, confira [fluxos de trabalho de máquina de estado](state-machine-workflows.md). Os fluxos de trabalho da máquina de estado têm suporte no designer hospedado novamente.

### <a name="contract-first-workflow-development"></a>Desenvolvimento de fluxo de trabalho de primeiro contrato

 A ferramenta de desenvolvimento de fluxo de trabalho de primeiro contrato permite que o desenvolvedor projete um contrato no código primeiro e, com alguns cliques no Visual Studio, gere automaticamente um modelo de atividade na caixa de ferramentas que representa cada operação. Essas atividades são então usadas para criar um fluxo de trabalho que implementa as operações definidas pelo contrato. O designer de fluxo de trabalho validará o serviço de fluxo de trabalho para assegurar que essas operações sejam implementadas e a assinatura do fluxo de trabalho corresponda à assinatura do contrato. O desenvolvedor também pode associar um serviço de fluxo de trabalho a uma coleção de contratos implementados. Para obter mais informações sobre o desenvolvimento do serviço de fluxo de trabalho do primeiro contrato, consulte [como: criar um serviço de fluxo de trabalho que consome um contrato de serviço existente](how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md).

> [!WARNING]
> O desenvolvimento de fluxo de trabalho de primeiro contrato não tem suporte no designer de fluxo de trabalho.
