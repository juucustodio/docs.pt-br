---
title: Depurar um aplicativo de console do .NET Core com o Visual Studio Code
description: Saiba como depurar um aplicativo de console do .NET Core com o Visual Studio Code.
ms.date: 05/26/2020
ms.openlocfilehash: eaeb97f54442006d2f0e29483a68dc3de89b5778
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202585"
---
# <a name="tutorial-debug-a-net-core-console-application-using-visual-studio-code"></a><span data-ttu-id="57204-103">Tutorial: Depurar um aplicativo de console do .NET Core usando Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="57204-103">Tutorial: Debug a .NET Core console application using Visual Studio Code</span></span>

<span data-ttu-id="57204-104">Este tutorial apresenta as ferramentas de depuração disponíveis no Visual Studio Code para trabalhar com aplicativos .NET Core.</span><span class="sxs-lookup"><span data-stu-id="57204-104">This tutorial introduces the debugging tools available in Visual Studio Code for working with .NET Core apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57204-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="57204-105">Prerequisites</span></span>

- <span data-ttu-id="57204-106">Este tutorial funciona com o aplicativo de console que você cria em [criar um aplicativo de console do .NET Core no Visual Studio Code](with-visual-studio-code.md).</span><span class="sxs-lookup"><span data-stu-id="57204-106">This tutorial works with the console app that you create in [Create a .NET Core console application in Visual Studio Code](with-visual-studio-code.md).</span></span>

## <a name="use-debug-build-configuration"></a><span data-ttu-id="57204-107">Usar configuração de compilação de depuração</span><span class="sxs-lookup"><span data-stu-id="57204-107">Use Debug build configuration</span></span>

<span data-ttu-id="57204-108">*Depuração* e *versão* são duas das configurações de compilação do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="57204-108">*Debug* and *release* are two of .NET Core's build configurations.</span></span> <span data-ttu-id="57204-109">Você usa a configuração de compilação de depuração para depuração e a configuração de versão para a distribuição de versão final.</span><span class="sxs-lookup"><span data-stu-id="57204-109">You use the Debug build configuration for debugging and the Release configuration for the final release distribution.</span></span>

<span data-ttu-id="57204-110">Na configuração de depuração, um programa é compilado com informações de depuração simbólicas completas e sem otimização.</span><span class="sxs-lookup"><span data-stu-id="57204-110">In the Debug configuration, a program compiles with full symbolic debug information and no optimization.</span></span> <span data-ttu-id="57204-111">A otimização complica a depuração, porque a relação entre o código fonte e as instruções geradas é mais complexa.</span><span class="sxs-lookup"><span data-stu-id="57204-111">Optimization complicates debugging, because the relationship between source code and generated instructions is more complex.</span></span> <span data-ttu-id="57204-112">A configuração de versão de um programa não tem informações de depuração simbólicas e é totalmente otimizada.</span><span class="sxs-lookup"><span data-stu-id="57204-112">The release configuration of a program has no symbolic debug information and is fully optimized.</span></span>

 <span data-ttu-id="57204-113">Por padrão, Visual Studio Code usa a configuração de compilação de depuração, portanto, você não precisa alterá-la antes da depuração.</span><span class="sxs-lookup"><span data-stu-id="57204-113">By default, Visual Studio Code uses the Debug build configuration, so you don't need to change it before debugging.</span></span>

## <a name="set-a-breakpoint"></a><span data-ttu-id="57204-114">Definir um ponto de interrupção</span><span class="sxs-lookup"><span data-stu-id="57204-114">Set a breakpoint</span></span>

<span data-ttu-id="57204-115">Um ponto de interrupção interrompe temporariamente a execução do aplicativo *antes* de a linha com o ponto de interrupção ser executada.</span><span class="sxs-lookup"><span data-stu-id="57204-115">A breakpoint temporarily interrupts the execution of the application *before* the line with the breakpoint is executed.</span></span>

1. <span data-ttu-id="57204-116">No *Program.cs*, defina um *ponto de interrupção* na linha que exibe o nome, a data e a hora clicando na margem esquerda da janela de código.</span><span class="sxs-lookup"><span data-stu-id="57204-116">In *Program.cs*, set a *breakpoint* on the line that displays the name, date, and time, by clicking in the left margin of the code window.</span></span> <span data-ttu-id="57204-117">A margem esquerda está à esquerda dos números de linha.</span><span class="sxs-lookup"><span data-stu-id="57204-117">The left margin is to the left of the line numbers.</span></span> <span data-ttu-id="57204-118">Outra maneira de definir um ponto de interrupção é colocando o cursor na linha de código e, em seguida, pressionando <kbd>F9</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-118">Another way to set a breakpoint is by placing the cursor in the line of code and then pressing <kbd>F9</kbd>.</span></span>

   <span data-ttu-id="57204-119">Como mostra a imagem a seguir, Visual Studio Code indica a linha na qual o ponto de interrupção é definido, exibindo um ponto vermelho na margem esquerda.</span><span class="sxs-lookup"><span data-stu-id="57204-119">As the following image shows, Visual Studio Code indicates the line on which the breakpoint is set by displaying a red dot in the left margin.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-set.png" alt-text="Conjunto de pontos de interrupção":::

## <a name="set-up-for-terminal-input"></a><span data-ttu-id="57204-121">Configurar para entrada de terminal</span><span class="sxs-lookup"><span data-stu-id="57204-121">Set up for terminal input</span></span>

<span data-ttu-id="57204-122">O ponto de interrupção está localizado após uma `Console.ReadLine` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="57204-122">The breakpoint is located after a `Console.ReadLine` method call.</span></span> <span data-ttu-id="57204-123">O **console de depuração** não aceita a entrada de terminal para um programa em execução.</span><span class="sxs-lookup"><span data-stu-id="57204-123">The **Debug Console** doesn't accept terminal input for a running program.</span></span> <span data-ttu-id="57204-124">Para lidar com a entrada de terminal durante a depuração, você pode usar o terminal integrado (um dos Visual Studio Code Windows) ou um terminal externo.</span><span class="sxs-lookup"><span data-stu-id="57204-124">To handle terminal input while debugging, you can use the integrated terminal (one of the Visual Studio Code windows) or an external terminal.</span></span> <span data-ttu-id="57204-125">Para este tutorial, você usa o terminal integrado.</span><span class="sxs-lookup"><span data-stu-id="57204-125">For this tutorial, you use the integrated terminal.</span></span>

1. <span data-ttu-id="57204-126">Abra *. vscode/Launch. JSON*.</span><span class="sxs-lookup"><span data-stu-id="57204-126">Open *.vscode/launch.json*.</span></span>

1. <span data-ttu-id="57204-127">Altere a `console` configuração para `integratedTerminal` .</span><span class="sxs-lookup"><span data-stu-id="57204-127">Change the `console` setting to `integratedTerminal`.</span></span>

   <span data-ttu-id="57204-128">De:</span><span class="sxs-lookup"><span data-stu-id="57204-128">From:</span></span>

   ```
   "console": "internalConsole",
   ```

   <span data-ttu-id="57204-129">Para:</span><span class="sxs-lookup"><span data-stu-id="57204-129">To:</span></span>

   ```
   "console": "integratedTerminal",
   ```

1. <span data-ttu-id="57204-130">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="57204-130">Save your changes.</span></span>

## <a name="start-debugging"></a><span data-ttu-id="57204-131">Iniciar a depuração</span><span class="sxs-lookup"><span data-stu-id="57204-131">Start debugging</span></span>

1. <span data-ttu-id="57204-132">Abra a exibição de depuração selecionando o ícone de depuração no menu do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="57204-132">Open the Debug view by selecting the Debugging icon on the left side menu.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/select-debug-pane.png" alt-text="Abrir a guia Depurar no Visual Studio Code":::

1. <span data-ttu-id="57204-134">Inicie a depuração selecionando a seta verde na parte superior do painel, ao lado de **inicialização do .NET Core (console)**.</span><span class="sxs-lookup"><span data-stu-id="57204-134">Start debugging by selecting the green arrow at the top of the pane, next to **.NET Core Launch (console)**.</span></span>  <span data-ttu-id="57204-135">Outra maneira de iniciar a depuração é pressionar <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-135">Another way to start debugging is by pressing <kbd>F5</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/start-debugging.png" alt-text="Iniciar Depuração":::

1. <span data-ttu-id="57204-137">Selecione a guia **terminal** para ver o "Qual é seu nome?"</span><span class="sxs-lookup"><span data-stu-id="57204-137">Select the **Terminal** tab to see the "What is your name?"</span></span> <span data-ttu-id="57204-138">avisar que o programa é exibido antes de aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="57204-138">prompt that the program displays before waiting for a response.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/select-terminal.png" alt-text="Selecione a guia terminal":::

1. <span data-ttu-id="57204-140">Insira uma cadeia de caracteres na janela do **terminal** em resposta à solicitação de um nome e pressione <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-140">Enter a string in the **Terminal** window in response to the prompt for a name, and then press <kbd>Enter</kbd>.</span></span>

   <span data-ttu-id="57204-141">A execução do programa para quando ele atinge o ponto de interrupção e antes de o método `Console.WriteLine` ser executado.</span><span class="sxs-lookup"><span data-stu-id="57204-141">Program execution stops when it reaches the breakpoint and before the `Console.WriteLine` method executes.</span></span> <span data-ttu-id="57204-142">A seção **locais** da janela **variáveis** exibe os valores das variáveis que são definidas no método em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="57204-142">The **Locals** section of the **Variables** window displays the values of variables that are defined in the currently executing method.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-hit.png" alt-text="Impacto de ponto de interrupção, mostrando locais":::

## <a name="change-variable-values"></a><span data-ttu-id="57204-144">Alterar valores de variáveis</span><span class="sxs-lookup"><span data-stu-id="57204-144">Change variable values</span></span>

<span data-ttu-id="57204-145">A janela do **console de depuração** permite interagir com o aplicativo que você está depurando.</span><span class="sxs-lookup"><span data-stu-id="57204-145">The **Debug Console** window lets you interact with the application you're debugging.</span></span> <span data-ttu-id="57204-146">Você pode alterar o valor de variáveis para ver como ele afeta seu programa.</span><span class="sxs-lookup"><span data-stu-id="57204-146">You can change the value of variables to see how it affects your program.</span></span>

1. <span data-ttu-id="57204-147">Selecione a guia **console de depuração** .</span><span class="sxs-lookup"><span data-stu-id="57204-147">Select the **Debug Console** tab.</span></span>

1. <span data-ttu-id="57204-148">Digite `name = "Gracie"` no prompt na parte inferior da janela do **console de depuração** e pressione a tecla <kbd>Enter</kbd> .</span><span class="sxs-lookup"><span data-stu-id="57204-148">Enter `name = "Gracie"` at the prompt at the bottom of the **Debug Console** window and press the <kbd>Enter</kbd> key.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/change-variable-values.png" alt-text="Alterar valores de variáveis":::

1. <span data-ttu-id="57204-150">Digite `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` na parte inferior da janela do **console de depuração** e pressione a tecla <kbd>Enter</kbd> .</span><span class="sxs-lookup"><span data-stu-id="57204-150">Enter `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` at the bottom of the **Debug Console** window and press the <kbd>Enter</kbd> key.</span></span>

   <span data-ttu-id="57204-151">A janela **variáveis** exibe os novos valores das `name` variáveis e `date` .</span><span class="sxs-lookup"><span data-stu-id="57204-151">The **Variables** window displays the new values of the `name` and `date` variables.</span></span>

1. <span data-ttu-id="57204-152">Continue a execução do programa selecionando o botão **continuar** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="57204-152">Continue program execution by selecting the **Continue** button in the toolbar.</span></span> <span data-ttu-id="57204-153">Outra maneira de continuar é pressionando <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-153">Another way to continue is by pressing <kbd>F5</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/continue-debugging.png" alt-text="Continuar a depuração":::

1. <span data-ttu-id="57204-155">Selecione a guia **terminal** novamente.</span><span class="sxs-lookup"><span data-stu-id="57204-155">Select the **Terminal** tab again.</span></span>

   <span data-ttu-id="57204-156">Os valores exibidos na janela do console correspondem às alterações feitas no **console de depuração**.</span><span class="sxs-lookup"><span data-stu-id="57204-156">The values displayed in the console window correspond to the changes you made in the **Debug Console**.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/changed-variable-values.png" alt-text="Terminal mostrando os valores inseridos":::

1. <span data-ttu-id="57204-158">Pressione qualquer tecla para sair do aplicativo e parar a depuração.</span><span class="sxs-lookup"><span data-stu-id="57204-158">Press any key to exit the application and stop debugging.</span></span>

## <a name="set-a-conditional-breakpoint"></a><span data-ttu-id="57204-159">Definir um ponto de interrupção condicional</span><span class="sxs-lookup"><span data-stu-id="57204-159">Set a conditional breakpoint</span></span>

<span data-ttu-id="57204-160">O programa exibe a cadeia de caracteres que o usuário insere.</span><span class="sxs-lookup"><span data-stu-id="57204-160">The program displays the string that the user enters.</span></span> <span data-ttu-id="57204-161">O que acontecerá se o usuário não inserir nada?</span><span class="sxs-lookup"><span data-stu-id="57204-161">What happens if the user doesn't enter anything?</span></span> <span data-ttu-id="57204-162">Você pode testá-lo com um recurso de depuração útil chamado de *ponto de interrupção condicional*.</span><span class="sxs-lookup"><span data-stu-id="57204-162">You can test this with a useful debugging feature called a *conditional breakpoint*.</span></span>

1. <span data-ttu-id="57204-163">Clique com o botão direito do mouse (<kbd>Ctrl</kbd>+ clique em MacOS) no ponto vermelho que representa o pontos de interrupção.</span><span class="sxs-lookup"><span data-stu-id="57204-163">Right-click (<kbd>Ctrl</kbd>+click on macOS) on the red dot that represents the breakpoint.</span></span> <span data-ttu-id="57204-164">No menu de contexto, selecione **Editar ponto de interrupção** para abrir uma caixa de diálogo que permite inserir uma expressão condicional.</span><span class="sxs-lookup"><span data-stu-id="57204-164">In the context menu, select **Edit Breakpoint** to open a dialog that lets you enter a conditional expression.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/breakpoint-context-menu.png" alt-text="Menu de contexto do ponto de interrupção":::

1. <span data-ttu-id="57204-166">Selecione `Expression` na lista suspensa, insira a seguinte expressão condicional e pressione <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-166">Select `Expression` in the drop-down, enter the following conditional expression, and press <kbd>Enter</kbd>.</span></span>

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/conditional-expression.png" alt-text="Inserir uma expressão condicional":::

   <span data-ttu-id="57204-168">Cada vez que o ponto de interrupção for atingido, o depurador chamará o `String.IsNullOrEmpty(name)` método e interromperá essa linha somente se a chamada do método retornar `true` .</span><span class="sxs-lookup"><span data-stu-id="57204-168">Each time the breakpoint is hit, the debugger calls the `String.IsNullOrEmpty(name)` method, and it breaks on this line only if the method call returns `true`.</span></span>

   <span data-ttu-id="57204-169">Em vez de uma expressão condicional, você pode especificar uma *contagem de ocorrências*, que interrompe a execução do programa antes que uma instrução seja executada um número especificado de vezes ou uma *condição de filtro*, que interrompe a execução do programa com base nesses atributos como um identificador de thread, um nome de processo ou um nome de thread.</span><span class="sxs-lookup"><span data-stu-id="57204-169">Instead of a conditional expression, you can specify a *hit count*, which interrupts program execution before a statement is executed a specified number of times, or a *filter condition*, which interrupts program execution based on such attributes as a thread identifier, process name, or thread name.</span></span>

1. <span data-ttu-id="57204-170">Inicie o programa com a depuração pressionando <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-170">Start the program with debugging by pressing <kbd>F5</kbd>.</span></span>

1. <span data-ttu-id="57204-171">Na guia **terminal** , pressione a tecla <kbd>Enter</kbd> quando for solicitado a inserir seu nome.</span><span class="sxs-lookup"><span data-stu-id="57204-171">In the **Terminal** tab, press the <kbd>Enter</kbd> key when prompted to enter your name.</span></span>

   <span data-ttu-id="57204-172">Como a condição especificada ( `name` is `null` ou <xref:System.String.Empty?displayProperty=nameWithType> ) foi satisfeita, a execução do programa é interrompida quando atinge o ponto de interrupção e antes da execução do `Console.WriteLine` método.</span><span class="sxs-lookup"><span data-stu-id="57204-172">Because the condition you specified (`name` is `null` or <xref:System.String.Empty?displayProperty=nameWithType>) has been satisfied, program execution stops when it reaches the breakpoint and before the `Console.WriteLine` method executes.</span></span>

   <span data-ttu-id="57204-173">A janela **variáveis** mostra que o valor da `name` variável é `""` , ou <xref:System.String.Empty?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="57204-173">The **Variables** window shows that the value of the `name` variable is `""`, or <xref:System.String.Empty?displayProperty=nameWithType>.</span></span>

1. <span data-ttu-id="57204-174">Confirme se o valor é uma cadeia de caracteres vazia digitando a seguinte instrução no prompt do **console de depuração** e pressionando <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-174">Confirm the value is an empty string by entering the following statement at the **Debug Console** prompt and pressing <kbd>Enter</kbd>.</span></span> <span data-ttu-id="57204-175">O resultado é `true`.</span><span class="sxs-lookup"><span data-stu-id="57204-175">The result is `true`.</span></span>

   ```csharp
   name == String.Empty
   ```

   :::image type="content" source="media/debugging-with-visual-studio-code/expression-in-debug-console.png" alt-text="Console de depuração retornando um valor true após a execução da instrução":::

1. <span data-ttu-id="57204-177">Selecione o botão **Continuar** na barra de ferramentas para continuar a execução do programa.</span><span class="sxs-lookup"><span data-stu-id="57204-177">Select the **Continue** button on the toolbar to continue program execution.</span></span>

1. <span data-ttu-id="57204-178">Selecione a guia **terminal** e pressione qualquer tecla para sair do programa e parar a depuração.</span><span class="sxs-lookup"><span data-stu-id="57204-178">Select the **Terminal** tab, and press any key to exit the program and stop debugging.</span></span>

1. <span data-ttu-id="57204-179">Desmarque o ponto de interrupção clicando no pontos na margem esquerda da janela de código.</span><span class="sxs-lookup"><span data-stu-id="57204-179">Clear the breakpoint by clicking on the dot in the left margin of the code window.</span></span> <span data-ttu-id="57204-180">Outra maneira de limpar um ponto de interrupção é pressionando <kbd>F9</kbd> enquanto a linha de código é selecionada.</span><span class="sxs-lookup"><span data-stu-id="57204-180">Another way to clear a breakpoint is by pressing <kbd>F9</kbd> while the line of code is selected.</span></span>

1. <span data-ttu-id="57204-181">Se você receber um aviso de que a condição de ponto de interrupção será perdida, selecione **remover ponto de interrupção**.</span><span class="sxs-lookup"><span data-stu-id="57204-181">If you get a warning that the breakpoint condition will be lost, select **Remove Breakpoint**.</span></span>

## <a name="step-through-a-program"></a><span data-ttu-id="57204-182">Percorrer um programa</span><span class="sxs-lookup"><span data-stu-id="57204-182">Step through a program</span></span>

<span data-ttu-id="57204-183">Visual Studio Code também permite que você percorra linha por linha por meio de um programa e monitore sua execução.</span><span class="sxs-lookup"><span data-stu-id="57204-183">Visual Studio Code also allows you to step line by line through a program and monitor its execution.</span></span> <span data-ttu-id="57204-184">Normalmente, você definiria um ponto de interrupção e seguirá o fluxo do programa por meio de uma pequena parte do código do programa.</span><span class="sxs-lookup"><span data-stu-id="57204-184">Ordinarily, you'd set a breakpoint and follow program flow through a small part of your program code.</span></span> <span data-ttu-id="57204-185">Como esse programa é pequeno, você pode percorrer todo o programa.</span><span class="sxs-lookup"><span data-stu-id="57204-185">Since this program is small, you can step through the entire program.</span></span>

1. <span data-ttu-id="57204-186">Defina um ponto de interrupção na chave de abertura do `Main` método.</span><span class="sxs-lookup"><span data-stu-id="57204-186">Set a breakpoint on the opening curly brace of the `Main` method.</span></span>

1. <span data-ttu-id="57204-187">Pressione <kbd>F5</kbd> para iniciar a depuração.</span><span class="sxs-lookup"><span data-stu-id="57204-187">Press <kbd>F5</kbd> to start debugging.</span></span>

   <span data-ttu-id="57204-188">Visual Studio Code realça a linha do ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="57204-188">Visual Studio Code highlights the breakpoint line.</span></span>

   <span data-ttu-id="57204-189">Neste ponto, a janela **variáveis** mostra que a `args` matriz está vazia e `name` `date` tem valores padrão.</span><span class="sxs-lookup"><span data-stu-id="57204-189">At this point, the **Variables** window shows that the `args` array is empty, and `name` and `date` have default values.</span></span>

1. <span data-ttu-id="57204-190">Selecione **a etapa into** ou pressione <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-190">Select **Step Into** or press <kbd>F11</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/step-into.png" alt-text="Botão de depuração":::

   <span data-ttu-id="57204-192">Visual Studio Code realça a próxima linha.</span><span class="sxs-lookup"><span data-stu-id="57204-192">Visual Studio Code highlights the next line.</span></span>

1. <span data-ttu-id="57204-193">Selecione **a etapa into** ou pressione <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-193">Select **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="57204-194">Visual Studio Code executa o `Console.WriteLine` para o prompt de nome e realça a próxima linha de execução.</span><span class="sxs-lookup"><span data-stu-id="57204-194">Visual Studio Code executes the `Console.WriteLine` for the name prompt and highlights the next line of execution.</span></span> <span data-ttu-id="57204-195">A próxima linha é o `Console.ReadLine` para o `name` .</span><span class="sxs-lookup"><span data-stu-id="57204-195">The next line is the `Console.ReadLine` for the `name`.</span></span> <span data-ttu-id="57204-196">A janela **variáveis** é inalterada e a guia **terminal** mostra o "Qual é seu nome?"</span><span class="sxs-lookup"><span data-stu-id="57204-196">The **Variables** window is unchanged, and the **Terminal** tab shows the "What is your name?"</span></span> <span data-ttu-id="57204-197">aviso.</span><span class="sxs-lookup"><span data-stu-id="57204-197">prompt.</span></span>

1. <span data-ttu-id="57204-198">Selecione **a etapa into** ou pressione <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-198">Select **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="57204-199">O Visual Studio realça a `name` atribuição de variável.</span><span class="sxs-lookup"><span data-stu-id="57204-199">Visual Studio highlights the `name` variable assignment.</span></span> <span data-ttu-id="57204-200">A janela **variáveis** mostra que `name` ainda é `null` .</span><span class="sxs-lookup"><span data-stu-id="57204-200">The **Variables** window shows that `name` is still `null`.</span></span>

1. <span data-ttu-id="57204-201">Responda ao prompt inserindo uma cadeia de caracteres na guia terminal e pressionando <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-201">Respond to the prompt by entering a string in the Terminal tab and pressing <kbd>Enter</kbd>.</span></span>

   <span data-ttu-id="57204-202">A guia **terminal** pode não exibir a cadeia de caracteres que você inserir enquanto estiver inserindo, mas o <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> método capturará sua entrada.</span><span class="sxs-lookup"><span data-stu-id="57204-202">The **Terminal** tab might not display the string you enter while you're entering it, but the <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> method will capture your input.</span></span>

1. <span data-ttu-id="57204-203">Selecione **a etapa into** ou pressione <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-203">Select **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="57204-204">Visual Studio Code realça a `date` atribuição de variável.</span><span class="sxs-lookup"><span data-stu-id="57204-204">Visual Studio Code highlights the `date` variable assignment.</span></span> <span data-ttu-id="57204-205">A janela **variáveis** mostra o valor retornado pela chamada para o <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> método.</span><span class="sxs-lookup"><span data-stu-id="57204-205">The **Variables** window shows the value returned by the call to the <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="57204-206">A guia **terminal** exibe a cadeia de caracteres que você inseriu no prompt.</span><span class="sxs-lookup"><span data-stu-id="57204-206">The **Terminal** tab displays the string you entered at the prompt.</span></span>

1. <span data-ttu-id="57204-207">Selecione **a etapa into** ou pressione <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-207">Select **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="57204-208">A janela **variáveis** mostra o valor da `date` variável após a atribuição da <xref:System.DateTime.Now?displayProperty=nameWithType> propriedade.</span><span class="sxs-lookup"><span data-stu-id="57204-208">The **Variables** window shows the value of the `date` variable after the assignment from the <xref:System.DateTime.Now?displayProperty=nameWithType> property.</span></span>

1. <span data-ttu-id="57204-209">Selecione **a etapa into** ou pressione <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-209">Select **Step Into** or press <kbd>F11</kbd>.</span></span>

   <span data-ttu-id="57204-210">Visual Studio Code chama o <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> método.</span><span class="sxs-lookup"><span data-stu-id="57204-210">Visual Studio Code calls the <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="57204-211">A janela do console exibe a cadeia de caracteres formatada.</span><span class="sxs-lookup"><span data-stu-id="57204-211">The console window displays the formatted string.</span></span>

1. <span data-ttu-id="57204-212">Selecione **sair** ou pressione <kbd>Shift</kbd> + <kbd>F11</kbd>.</span><span class="sxs-lookup"><span data-stu-id="57204-212">Select **Step Out** or press <kbd>Shift</kbd>+<kbd>F11</kbd>.</span></span>

   :::image type="content" source="media/debugging-with-visual-studio-code/step-out.png" alt-text="Botão de depuração":::

1. <span data-ttu-id="57204-214">Selecione a guia **terminal** .</span><span class="sxs-lookup"><span data-stu-id="57204-214">Select the **Terminal** tab.</span></span>

   <span data-ttu-id="57204-215">O terminal exibe "Pressione qualquer tecla para sair..."</span><span class="sxs-lookup"><span data-stu-id="57204-215">The terminal displays "Press any key to exit..."</span></span>

1. <span data-ttu-id="57204-216">Pressione qualquer tecla para sair do programa.</span><span class="sxs-lookup"><span data-stu-id="57204-216">Press any key to exit the program.</span></span>

## <a name="select-release-build-configuration"></a><span data-ttu-id="57204-217">Selecionar configuração da compilação de versão</span><span class="sxs-lookup"><span data-stu-id="57204-217">Select Release build configuration</span></span>

<span data-ttu-id="57204-218">Depois de testar a versão de depuração do seu aplicativo, você também deve compilar e testar a versão de lançamento.</span><span class="sxs-lookup"><span data-stu-id="57204-218">Once you've tested the Debug version of your application, you should also compile and test the Release version.</span></span> <span data-ttu-id="57204-219">A versão de lançamento incorpora otimizações de compilador que podem afetar o comportamento de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57204-219">The Release version incorporates compiler optimizations that can affect the behavior of an application.</span></span> <span data-ttu-id="57204-220">Por exemplo, as otimizações do compilador que são projetadas para melhorar o desempenho podem criar condições de corrida em aplicativos multissegmentados.</span><span class="sxs-lookup"><span data-stu-id="57204-220">For example, compiler optimizations that are designed to improve performance can create race conditions in multithreaded applications.</span></span>

<span data-ttu-id="57204-221">Para compilar e testar a versão de lançamento do seu aplicativo de console, abra o **terminal** e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="57204-221">To build and test the Release version of your console application, open the **Terminal** and run the following command:</span></span>

```dotnetcli
dotnet run --configuration Release
```

## <a name="additional-resources"></a><span data-ttu-id="57204-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="57204-222">Additional resources</span></span>

* [<span data-ttu-id="57204-223">Depurar no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="57204-223">Debugging in Visual Studio Code</span></span>](https://code.visualstudio.com/docs/editor/debugging)

## <a name="next-steps"></a><span data-ttu-id="57204-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57204-224">Next steps</span></span>

<span data-ttu-id="57204-225">Neste tutorial, você usou Visual Studio Code ferramentas de depuração.</span><span class="sxs-lookup"><span data-stu-id="57204-225">In this tutorial, you used Visual Studio Code debugging tools.</span></span> <span data-ttu-id="57204-226">Para saber como publicar uma versão implantável do aplicativo, consulte [publicar seu aplicativo](cli-create-console-app.md#publish-your-app).</span><span class="sxs-lookup"><span data-stu-id="57204-226">To learn how to publish a deployable version of the app, see [Publish your app](cli-create-console-app.md#publish-your-app).</span></span>

<!--In the next tutorial, you publish a deployable version of the app.

> [!div class="nextstepaction"]
> [Publish a .NET Core console application with Visual Studio Code](publishing-with-visual-studio-code.md)
-->