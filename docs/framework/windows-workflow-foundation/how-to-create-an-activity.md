---
title: 'Como: criar uma atividade'
description: 'Este artigo mostra como criar duas atividades no Workflow Foundation: uma que usa o código para implementar sua lógica e outra definida usando outras atividades.'
ms.date: 09/14/2018
dev_langs:
- csharp
- vb
ms.assetid: c09b1e99-21b5-4d96-9c04-ec31db3f4436
ms.openlocfilehash: c7610d8612eb944afa9c23e1bf2abceeb3a6d38b
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190761"
---
# <a name="how-to-create-an-activity"></a>Como: criar uma atividade

As atividades são a unidade principal de comportamento no [!INCLUDE[wf1](../../../includes/wf1-md.md)]. A lógica de execução de uma atividade pode ser implementada em código gerenciado ou pode ser implementada usando outras atividades. Este tópico demonstra como criar duas atividades. A primeira atividade é uma atividade simples que usa o código para implementar a sua lógica de execução. A implementação da segunda atividade é definida usando outras atividades. Essas atividades são usadas nas seguintes etapas no tutorial.

## <a name="create-the-activity-library-project"></a>Criar o projeto de biblioteca de atividades

1. Abra o Visual Studio e escolha **novo**  >  **projeto** no menu **arquivo** .

2. Na caixa de diálogo **novo projeto** , na categoria **instalado** , selecione   >  **fluxo de trabalho** do Visual C# (ou **Visual Basic**  >  **fluxo de trabalho**).

    > [!NOTE]
    > Se você não vir a categoria de modelo de **fluxo de trabalho** , talvez seja necessário instalar o componente **Windows Workflow Foundation** do Visual Studio. Escolha o link **abrir instalador do Visual Studio** no lado esquerdo da caixa de diálogo **novo projeto** . Em Instalador do Visual Studio, selecione a guia **componentes individuais** . Em seguida, na categoria **atividades de desenvolvimento** , selecione o componente **Windows Workflow Foundation** . Escolha **Modificar** para instalar o componente.

3. Selecione o modelo de projeto de **biblioteca de atividades** . Digite `NumberGuessWorkflowActivities` na caixa **Nome** e clique em **OK**.

4. Clique com o botão direito do mouse em **Activity1.xaml** no **Gerenciador de Soluções** e selecione **Excluir**. Clique em **OK** para confirmar.

## <a name="create-the-readint-activity"></a>Criar a atividade ReadInt

1. Escolha **Adicionar novo item** no menu **projeto** .

2. No nó   >  **itens comuns** instalados, selecione **fluxo de trabalho**. Selecione **atividade de código** na lista **fluxo de trabalho** .

3. Digite `ReadInt` na caixa **Nome** e clique em **Adicionar**.

4. Substitua a definição existente de `ReadInt` pela seguinte definição.

     [!code-csharp[CFX_WF_GettingStarted#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/readint.cs#1)]
     [!code-vb[CFX_WF_GettingStarted#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/readint.vb#1)]

    > [!NOTE]
    > A atividade `ReadInt` é derivada de <xref:System.Activities.NativeActivity%601> em vez de <xref:System.Activities.CodeActivity>, que é o padrão para o modelo de atividade de código. <xref:System.Activities.CodeActivity%601> poderá ser usado se a atividade fornecer um único resultado, que é exposto através do argumento <xref:System.Activities.Activity%601.Result%2A>, mas <xref:System.Activities.CodeActivity%601> não oferece suporte ao uso de indicadores, portanto <xref:System.Activities.NativeActivity%601> será usado.

## <a name="create-the-prompt-activity"></a>Criar a atividade de prompt

1. Pressione **Ctrl** + **Shift** + **B** para compilar o projeto. Compilar o projeto permite que a atividade `ReadInt` neste projeto seja usada para criar a atividade personalizada dessa etapa.

2. Escolha **Adicionar novo item** no menu **projeto** .

3. No nó   >  **itens comuns** instalados, selecione **fluxo de trabalho**. Selecione **Atividade** na lista **Fluxo de Trabalho**.

4. Digite `Prompt` na caixa **Nome** e clique em **Adicionar**.

5. Clique duas vezes em **prompt. XAML** em **Gerenciador de soluções** para exibi-lo no designer se ele ainda não estiver sendo exibido.

6. Clique em **Argumentos** no lado inferior esquerdo do designer de atividade para exibir o painel **Argumentos**.

7. Clique em **Criar Argumento**.

8. Digite na `BookmarkName` caixa **nome** , selecione **em na** lista suspensa **direção** , selecione **cadeia de caracteres** na lista suspensa tipo de **argumento** e pressione **Enter** para salvar o argumento.

9. Clique em **Criar Argumento**.

10. Digite `Result` na caixa de **nome** que está abaixo do argumento recém-adicionado `BookmarkName` , selecione **fora** na lista suspensa **direção** , selecione **Int32** na lista suspensa tipo de **argumento** e pressione **Enter** para.

11. Clique em **Criar Argumento**.

12. Digite na `Text` caixa **nome** , selecione **em na** lista suspensa **direção** , selecione **cadeia de caracteres** na lista suspensa tipo de **argumento** e pressione **Enter** para salvar o argumento.

     Esses três argumentos são associados aos argumentos correspondentes das atividades <xref:System.Activities.Statements.WriteLine> e `ReadInt` que são adicionadas à atividade `Prompt` nas seguintes etapas.

13. Clique em **Argumentos** no lado inferior esquerdo do designer de atividade para fechar o painel **Argumentos**.

14. Arraste uma atividade de **sequência** da seção **fluxo de controle** da **caixa de ferramentas** e solte-a no rótulo **descartar atividade aqui** do designer de atividade de **prompt** .

    > [!TIP]
    > Se a janela da **Caixa de Ferramentas** não abrir, selecione **Caixa de Ferramentas** no menu **Exibir**.

15. Arraste uma atividade **WriteLine** da seção **primitivas** da caixa de **ferramentas** e solte-a no rótulo **descartar atividade aqui** da atividade de **sequência** .

16. Vincule o argumento **Text** da atividade **WriteLine** ao argumento Text da atividade **prompt** digitando na caixa de **texto** `Text` **Inserir uma expressão C#** ou **Inserir uma expressão VB** na janela **Propriedades** e, em seguida, pressione a tecla **Tab** duas vezes. Isso fecha a janela dos membros da lista do IntelliSense e salva o valor da propriedade removendo a seleção da propriedade. Essa propriedade também pode ser definida digitando na `Text` caixa **Inserir uma expressão C#** ou **Inserir uma expressão VB** na própria atividade.

    > [!TIP]
    > Se a **janela Propriedades** não for exibida, selecione **janela Propriedades** no menu **Exibir** .

17. Arraste uma atividade **ReadInt** da seção **NumberGuessWorkflowActivities** da caixa de **ferramentas** e solte-a na atividade **Sequence** para que ela siga a atividade **WriteLine** .

18. Associe o argumento **BookmarkName** da atividade **ReadInt** ao argumento **BookmarkName** da atividade **prompt** , digitando `BookmarkName` na caixa **Inserir uma expressão VB** à direita do argumento **BookmarkName** na **janela Propriedades** e pressione a tecla **Tab** duas vezes para fechar a janela membros da lista do IntelliSense e salvar a propriedade.

19. Vincule o argumento **Result** da atividade **ReadInt** ao argumento **Result** da atividade **prompt** , digitando `Result` na caixa **Inserir uma expressão VB** à direita do argumento **resultado** na **janela Propriedades** e pressione a tecla **Tab** duas vezes...

20. Pressione **Ctrl** + **Shift** + **B** para criar a solução.

## <a name="next-steps"></a>Próximas etapas

Para obter instruções sobre como criar um fluxo de trabalho usando essas atividades, consulte a próxima etapa do tutorial [como: criar um fluxo de trabalho](how-to-create-a-workflow.md).

## <a name="see-also"></a>Confira também

- <xref:System.Activities.CodeActivity>
- <xref:System.Activities.NativeActivity%601>
- [Criando e implementando atividades personalizadas](designing-and-implementing-custom-activities.md)
- [Guia de introdução ao tutorial](getting-started-tutorial.md)
- [Como: criar um fluxo de trabalho](how-to-create-a-workflow.md)
- [Usando o ExpressionTextBox em um designer personalizado de atividades](./samples/using-the-expressiontextbox-in-a-custom-activity-designer.md)
