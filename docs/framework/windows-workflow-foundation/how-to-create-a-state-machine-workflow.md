---
title: 'Como: criar um fluxo de trabalho da máquina de estado'
description: Este artigo cria um fluxo de trabalho que usa atividades internas, como a atividade StateMachine e atividades personalizadas.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3ec60e8f-fad4-493e-a426-e7962d7aee8c
ms.openlocfilehash: 8e977a182d55143f8d877d61a0f0345bbe6bded4
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190462"
---
# <a name="how-to-create-a-state-machine-workflow"></a>Como: criar um fluxo de trabalho da máquina de estado

Os fluxos de trabalho podem ser construídos a partir de atividades internas assim como as atividades personalizadas. Este tópico percorre a criação de um fluxo de trabalho que usa atividades internas, como a <xref:System.Activities.Statements.StateMachine> atividade, e as atividades personalizadas do tópico [como criar uma atividade](how-to-create-an-activity.md) anterior. O fluxo de trabalho modela um jogo de palpite de número.  
  
> [!NOTE]
> Cada tópico do tutorial de Introdução depende dos tópicos anteriores. Para concluir este tópico, você deve primeiro concluir [como: criar uma atividade](how-to-create-an-activity.md).  
  
### <a name="to-create-the-workflow"></a>Para criar o fluxo de trabalho  
  
1. Clique com o botão direito do mouse em **NumberGuessWorkflowActivities** em **Gerenciador de soluções** e selecione **Adicionar**, **novo item**.  
  
2. No nó **itens comuns** **instalados**, selecione fluxo de **trabalho**. Selecione **Atividade** na lista **Fluxo de Trabalho**.  
  
3. Digite `StateMachineNumberGuessWorkflow` na caixa **nome** e clique em **Adicionar**.  
  
4. Arraste uma atividade **StateMachine** da seção **máquina de estado** da caixa de **ferramentas** e solte-a no rótulo **soltar atividade aqui** na superfície de design do fluxo de trabalho.  
  
### <a name="to-create-the-workflow-variables-and-arguments"></a>Para criar as variáveis e os argumentos do fluxo de trabalho  
  
1. Clique duas vezes em **StateMachineNumberGuessWorkflow. XAML** em **Gerenciador de soluções** para exibir o fluxo de trabalho no designer, se ele ainda não estiver sendo exibido.  
  
2. Clique em **argumentos** no lado inferior esquerdo do designer de fluxo de trabalho para exibir o painel **argumentos** .  
  
3. Clique em **Criar Argumento**.  
  
4. Digite na `MaxNumber` caixa **nome** , selecione **em na** lista suspensa **direção** , selecione **Int32** na lista suspensa tipo de **argumento** e pressione ENTER para salvar o argumento...  
  
5. Clique em **Criar Argumento**.  
  
6. Digite `Turns` na caixa de **nome** que está abaixo do argumento recém-adicionado `MaxNumber` , selecione **fora** na lista suspensa **direção** , selecione **Int32** na lista suspensa tipo de **argumento** e, em seguida, pressione Enter.  
  
7. Clique em **Argumentos** no lado inferior esquerdo do designer de atividade para fechar o painel **Argumentos**.  
  
8. Clique em **variáveis** no lado inferior esquerdo do designer de fluxo de trabalho para exibir o painel **variáveis** .  
  
9. Clique em **Criar Variável**.  
  
    > [!TIP]
    > Se nenhuma caixa **criar variável** for exibida, clique na <xref:System.Activities.Statements.StateMachine> atividade na superfície do designer de fluxo de trabalho para selecioná-la.  
  
10. Digite `Guess` na caixa **nome** , selecione **Int32** na lista suspensa **tipo de variável** e pressione ENTER para salvar a variável.  
  
11. Clique em **Criar Variável**.  
  
12. Digite `Target` na caixa **nome** , selecione **Int32** na lista suspensa **tipo de variável** e pressione ENTER para salvar a variável.  
  
13. Clique em **Variáveis** no lado inferior esquerdo do designer de atividade para fechar o painel **Variáveis**.  
  
### <a name="to-add-the-workflow-activities"></a>Para adicionar as atividades de fluxo de trabalho  
  
1. Clique em **State1** para selecioná-lo. Na **janela Propriedades**, altere o **DisplayName** para `Initialize Target` .  
  
    > [!TIP]
    > Se a **janela Propriedades** não for exibida, selecione **janela Propriedades** no menu **Exibir** .  
  
2. Clique duas vezes no estado de destino de **inicialização** renomeado recentemente no designer de fluxo de trabalho para expandi-lo.  
  
3. Arraste uma atividade **atribuir** da seção **primitivas** da caixa de **ferramentas** e solte-a na seção **entrada** do estado. Digite `Target` na caixa **para** e a expressão a seguir na caixa **Inserir uma expressão C#** ou **Inserir uma expressão VB** .  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    > Se a janela da **Caixa de Ferramentas** não abrir, selecione **Caixa de Ferramentas** no menu **Exibir**.  
  
4. Retorne à exibição de máquina de estado geral no designer de fluxo de trabalho clicando em **StateMachine** na exibição de navegação estrutural na parte superior do designer de fluxo de trabalho.  
  
5. Arraste uma atividade de **estado** da seção **máquina de estado** da **caixa de ferramentas** para o designer de fluxo de trabalho e passe o mouse sobre o estado de destino de **inicialização** . Observe que quatro triângulos aparecerão em torno do estado de **inicialização de destino** quando o novo estado estiver sobre ele. Descarte o novo estado no triângulo imediatamente abaixo do estado de **inicialização de destino** . Isso coloca o novo estado no fluxo de trabalho e cria uma transição do estado de **destino de inicialização** para o novo estado.  
  
6. Clique em **State1** para selecioná-lo, altere o **DisplayName** para `Enter Guess` e clique duas vezes no estado no designer de fluxo de trabalho para expandi-lo.  
  
7. Arraste uma atividade **WriteLine** da seção **primitivas** da caixa de **ferramentas** e solte-a na seção **entrada** do estado.  
  
8. Digite a expressão a seguir na caixa de propriedade **texto** de **WriteLine**.  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
9. Arraste uma atividade **assign** da seção **primitivas** da caixa de **ferramentas** e solte na seção **sair** do estado.  
  
10. Digite `Turns` na caixa **para** e `Turns + 1` na caixa **Inserir uma expressão C#** ou **Inserir uma expressão VB** .  
  
11. Retorne à exibição de máquina de estado geral no designer de fluxo de trabalho clicando em **StateMachine** na exibição de navegação estrutural na parte superior do designer de fluxo de trabalho.  
  
12. Arraste uma atividade **FinalState** da seção **máquina de estado** da **caixa de ferramentas**, passe o mouse sobre o estado de **adivinhação Enter** e solte-o no triângulo que aparece à direita do estado de **estimativa Enter** para que uma transição seja criada entre **Enter estimativa** e **FinalState**.  
  
13. O nome padrão da transição é **T2**. Clique na transição no designer de fluxo de trabalho para selecioná-la e defina seu **DisplayName** como **palpite correto**. Em seguida, clique e selecione o **FinalState** e arraste-o para a direita para que haja espaço para que o nome de transição completo seja exibido sem sobreposição de qualquer um dos dois Estados. Isso facilitará a conclusão das etapas restantes no tutorial.  
  
14. Clique duas vezes na transição **correta de adivinhação** renomeada no designer de fluxo de trabalho para expandi-la.  
  
15. Arraste uma atividade **ReadInt** da seção **NumberGuessWorkflowActivities** da caixa de **ferramentas** e solte-a na seção **gatilho** da transição.  
  
16. Na **janela Propriedades** da atividade **ReadInt** , digite `"EnterGuess"` incluindo as aspas na caixa valor da propriedade **BookmarkName** e digite `Guess` na caixa valor da propriedade de **resultado**  
  
17. Digite a expressão a seguir na caixa de valor da propriedade **Condition** da transição **correta** .  
  
    ```vb  
    Guess = Target  
    ```  
  
    ```csharp  
    Guess == Target  
    ```  
  
18. Retorne à exibição de máquina de estado geral no designer de fluxo de trabalho clicando em **StateMachine** na exibição de navegação estrutural na parte superior do designer de fluxo de trabalho.  
  
    > [!NOTE]
    > Uma transição ocorre quando o evento de gatilho é recebido e o <xref:System.Activities.Statements.Transition.Condition%2A>, se houver, é avaliado como `True`. Para essa transição, se o usuário `Guess` corresponder ao gerado aleatoriamente `Target` , o controle passará para o **FinalState** e o fluxo de trabalho será concluído.  
  
19. Dependendo se a estimativa está correta, o fluxo de trabalho deve fazer a transição para o **FinalState** ou de volta para o estado de **adivinhação Enter** para outra tentativa. Ambas as transições compartilham o mesmo gatilho de aguardando que a adivinhação do usuário seja recebida por meio da atividade **ReadInt** . Isso é chamado de uma transição compartilhada. Para criar uma transição compartilhada, clique no círculo que indica o início da transição de **adivinhação correta** e arraste-a para o estado desejado. Nesse caso, a transição é uma transição automática, portanto, arraste o ponto inicial da transição de **adivinhação correta** e solte-a de volta na parte inferior do estado de **adivinhação Enter** . Depois de criar a transição, selecione-a no designer de fluxo de trabalho e defina sua propriedade **DisplayName** como **adivinhar incorreta**.  
  
    > [!NOTE]
    > As transições compartilhadas também podem ser criadas de dentro do designer de transição clicando em **Adicionar transição de gatilho compartilhado** na parte inferior do designer de transição e, em seguida, selecionando o estado de destino desejado na lista suspensa **Estados disponíveis para conexão** .  
    > [!NOTE]
    > Observe que se <xref:System.Activities.Statements.Transition.Condition%2A> de uma transição for avaliada como `false` (ou todas as condições de uma transição do gatilho compartilhada for avaliada como `false`), a transição não ocorrerá e todos os gatilhos para todas as transições de estado serão reprogramados. Neste tutorial, essa situação não pode ocorrer devido à maneira como as condições são configuradas (temos ações específicas para se o palpite está correto ou incorreto).  
  
20. Clique duas vezes em **adivinhar transição incorreta** no designer de fluxo de trabalho para expandi-la. Observe que o **gatilho** já está definido como a mesma atividade **ReadInt** que foi usada pela transição de **adivinhação correta** .  
  
21. Digite a expressão a seguir na caixa valor da propriedade de **condição** .  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
22. Arraste uma atividade **If** da seção **fluxo de controle** da **caixa de ferramentas** e solte-a na seção **ação** da transição.  
  
23. Digite a expressão a seguir na caixa de valor da propriedade **condição** **If** da atividade.  
  
    ```text
    Guess < Target
    ```  
  
24. Arraste duas atividades **WriteLine** da seção **primitivas** da caixa de **ferramentas** e solte-as para que uma esteja na seção **em seguida** da atividade **se** e outra esteja na seção **else** .  
  
25. Clique na atividade **WriteLine** na seção **em seguida** para selecioná-la e digite a expressão a seguir na caixa valor da propriedade de **texto** .  
  
    ```text
    "Your guess is too low."  
    ```  
  
26. Clique na atividade **WriteLine** na seção **else** para selecioná-la e digite a expressão a seguir na caixa valor da propriedade de **texto** .  
  
    ```text
    "Your guess is too high."  
    ```  
  
27. Retorne à exibição de máquina de estado geral no designer de fluxo de trabalho clicando em **StateMachine** na exibição de navegação estrutural na parte superior do designer de fluxo de trabalho.  
  
     O exemplo a seguir ilustra o fluxo de trabalho concluído.  
  
     ![Ilustração que mostra o fluxo de trabalho da máquina de estado concluído.](./media/how-to-create-a-state-machine-workflow/complete-state-machine-workflow.jpg)  
  
### <a name="to-build-the-workflow"></a>Para compilar o fluxo de trabalho  
  
1. Pressione CTRL+SHIFT+B para criar a solução.  
  
     Para obter instruções sobre como executar o fluxo de trabalho, consulte o próximo tópico [como: executar um fluxo de trabalho](how-to-run-a-workflow.md). Se você já tiver concluído a etapa [como executar um fluxo de trabalho](how-to-run-a-workflow.md) com um estilo diferente de fluxo de trabalho e desejar executá-lo usando o fluxo de trabalho da máquina de estado nesta etapa, pule para a seção [para criar e executar o aplicativo](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) de [como executar um fluxo de trabalho](how-to-run-a-workflow.md).  
  
## <a name="see-also"></a>Confira também

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Programação do Windows Workflow Foundation](programming.md)
- [Criando fluxos de trabalho](designing-workflows.md)
- [Guia de introdução ao tutorial](getting-started-tutorial.md)
- [Como: criar uma atividade](how-to-create-an-activity.md)
- [Como: executar um fluxo de trabalho](how-to-run-a-workflow.md)
