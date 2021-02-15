---
title: Depurar um aplicativo de console .NET usando o Visual Studio
description: Saiba como depurar um aplicativo de console do .NET usando o Visual Studio.
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: 8a914dc6cf069c011ea5b077ada514bf8cec331d
ms.sourcegitcommit: 5114e7847e0ff8ddb8c266802d47af78567949cf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94916178"
---
# <a name="tutorial-debug-a-net-console-application-using-visual-studio"></a>Tutorial: Depurar um aplicativo de console .NET usando o Visual Studio

Este tutorial apresenta as ferramentas de depuração disponíveis no Visual Studio.

## <a name="prerequisites"></a>Pré-requisitos

- Este tutorial funciona com o aplicativo de console que você cria em [criar um aplicativo de console .NET usando o Visual Studio](with-visual-studio.md).

## <a name="use-debug-build-configuration"></a>Usar configuração de compilação de depuração

*Debug* e *Release* são as configurações de compilação internas do Visual Studio. Você usa a configuração de compilação de depuração para depuração e a configuração de versão para a distribuição de versão final.

Na configuração de depuração, um programa é compilado com informações de depuração simbólicas completas e sem otimização. A otimização complica a depuração, porque a relação entre o código fonte e as instruções geradas é mais complexa. A configuração de versão de um programa não tem informações de depuração simbólicas e é totalmente otimizada.

 Por padrão, o Visual Studio usa a configuração de compilação de depuração, portanto, você não precisa alterá-la antes da depuração.

1. Inicie o Visual Studio.

1. Abra o projeto que você criou em [criar um aplicativo de console .NET usando o Visual Studio](with-visual-studio.md).

   A configuração de build atual é mostrada na barra de ferramentas. A imagem da barra de ferramentas a seguir mostra que o Visual Studio está configurado para compilar a versão de depuração do aplicativo:

   :::image type="content" source="./media/debugging-with-visual-studio/visual-studio-toolbar-debug.png" alt-text="Barra de ferramentas do Visual Studio com depuração realçada":::

## <a name="set-a-breakpoint"></a>Definir um ponto de interrupção

Um *ponto de interrupção* interrompe temporariamente a execução do aplicativo antes de a linha com o ponto de interrupção ser executada.

1. Defina um *ponto de interrupção* na linha que exibe o nome, a data e a hora clicando na margem esquerda da janela de código nessa linha. A margem esquerda está à esquerda dos números de linha.  Outras maneiras de definir um ponto de interrupção são colocando o cursor na linha de código e, em seguida, pressionando <kbd>F9</kbd> ou escolhendo **depurar**  >  **alternância de ponto de interrupção** na barra de menus.

   Como mostra a imagem a seguir, o Visual Studio indica a linha na qual o ponto de interrupção é definido, destacando-o e exibindo um ponto vermelho na margem esquerda.

   :::image type="content" source="./media/debugging-with-visual-studio/set-breakpoint-in-editor.png" alt-text="Janela Programa do Visual Studio com o ponto de interrupção definido":::

1. Pressione <kbd>F5</kbd> para executar o programa no modo de depuração. Outra maneira de iniciar a depuração é escolhendo **depurar**  >  **Iniciar Depuração** no menu.

1. Insira uma cadeia de caracteres na janela do console quando o programa solicitar um nome e pressione <kbd>Enter</kbd>.

1. A execução do programa para quando ele atinge o ponto de interrupção e antes de o método `Console.WriteLine` ser executado. A janela **Locais** exibe os valores das variáveis que são definidas no método que está sendo executado no momento.

   :::image type="content" source="./media/debugging-with-visual-studio/breakpoint-hit.png" alt-text="Captura de tela de um ponto de interrupção no Visual Studio":::

## <a name="use-the-immediate-window"></a>Usar a janela imediata

A janela **imediata** permite interagir com o aplicativo que você está depurando. Você pode alterar o valor de variáveis interativamente para ver como ele afeta seu programa.

1. Se a janela **imediata** não estiver visível, exiba-a escolhendo **depurar**  >  **janelas**  >  **imediatamente**.

1. Insira `name = "Gracie"` na janela **imediata** e pressione a tecla <kbd>Enter</kbd> .

1. Insira `date = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime()` na janela **imediata** e pressione a tecla <kbd>Enter</kbd> .

   A janela **imediato** exibe o valor da variável de cadeia de caracteres e as propriedades do <xref:System.DateTime> valor. Além disso, os valores das variáveis são atualizados na janela **locais** .

   :::image type="content" source="./media/debugging-with-visual-studio/locals-immediate-window.png" alt-text="Locais e janelas imediatas no Visual Studio 2019":::

1. Pressione <kbd>F5</kbd> para continuar a execução do programa. Outra maneira de continuar é escolhendo **depurar**  >  **continuar** no menu.

   Os valores exibidos na janela do console correspondem às alterações feitas na janela **imediata** .

   :::image type="content" source="./media/debugging-with-visual-studio/console-window.png" alt-text="Janela do console mostrando os valores inseridos":::

1. Pressione qualquer tecla para sair do aplicativo e parar a depuração.

## <a name="set-a-conditional-breakpoint"></a>Definir um ponto de interrupção condicional

O programa exibe a cadeia de caracteres que o usuário insere. O que acontecerá se o usuário não inserir nada? Você pode testá-lo com um recurso de depuração útil chamado de *ponto de interrupção condicional*.

1. Clique com o botão direito do mouse no ponto vermelho que representa o ponto de interrupção. No menu de contexto, selecione **condições** para abrir a caixa de diálogo **configurações de ponto de interrupção** . Marque a caixa para **condições** se ela ainda não estiver selecionada.

   :::image type="content" source="./media/debugging-with-visual-studio/breakpoint-settings.png" alt-text="Editor mostrando o painel de configurações do ponto de interrupção – C#":::

1. Para a **expressão condicional**, insira o código a seguir no campo que mostra o código de exemplo que testa se `x` é 5. Se o idioma que você deseja usar não for mostrado, altere o seletor de idioma na parte superior da página.

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   ```vb
   String.IsNullOrEmpty(name)
   ```

   Cada vez que o ponto de interrupção for atingido, o depurador chamará o `String.IsNullOrEmpty(name)` método e interromperá essa linha somente se a chamada do método retornar `true` .

   Em vez de uma expressão condicional, você pode especificar uma *contagem de ocorrências*, que interrompe a execução do programa antes que uma instrução seja executada um número especificado de vezes. Outra opção é especificar uma *condição de filtro*, que interrompe a execução do programa com base nesses atributos como um identificador de thread, um nome de processo ou um nome de thread.

1. Selecione **fechar** para fechar a caixa de diálogo.

1. Inicie o programa com a depuração pressionando <kbd>F5</kbd>.

1. Na janela do console, pressione a tecla <kbd>Enter</kbd> quando for solicitado a inserir seu nome.

1. Como a condição que você especificou ( `name` é `null` ou <xref:System.String.Empty?displayProperty=nameWithType> ) foi satisfeita, a execução do programa é interrompida quando atinge o ponto de interrupção e antes da `Console.WriteLine` execução do método.

1. Selecione a janela **locais** , que mostra os valores das variáveis que são locais para o método atualmente em execução. Nesse caso, `Main` é o método atualmente em execução. Observe que o valor da variável `name` é `""` ou <xref:System.String.Empty?displayProperty=nameWithType>.

1. Confirme se o valor é uma cadeia de caracteres vazia inserindo a seguinte instrução na janela **imediata** e pressionando <kbd>Enter</kbd>. O resultado é `true`.

   ```csharp
   ? name == String.Empty
   ```

   ```vb
   ? String.IsNullOrEmpty(name)
   ```

   O ponto de interrogação direciona a janela imediata para [avaliar uma expressão](/visualstudio/ide/reference/immediate-window#enter-commands).

   :::image type="content" source="./media/debugging-with-visual-studio/immediate-window-output.png" alt-text="Janela Imediata retornando um valor igual a true após a execução da instrução – C#":::

1. Pressione <kbd>F5</kbd> para continuar a execução do programa.

1. Pressione qualquer tecla para fechar a janela do console e parar a depuração.

1. Desmarque o ponto de interrupção clicando no pontos na margem esquerda da janela de código. Outras maneiras de limpar um ponto de interrupção são pressionando <kbd>F9</kbd> ou escolhendo **debug > alternar o ponto de interrupção** enquanto a linha de código é selecionada.

## <a name="step-through-a-program"></a>Percorrer um programa

O Visual Studio também permite percorrer linha por linha de um programa e monitorar sua execução. Normalmente, você definiria um ponto de interrupção e seguirá o fluxo do programa por meio de uma pequena parte do código do programa. Como esse programa é pequeno, você pode percorrer todo o programa.

1. Escolha **depurar**  >  **etapa em**. Outra maneira de depurar uma instrução por vez é pressionar <kbd>F11</kbd>.

   O Visual Studio realça e exibe uma seta ao lado da próxima linha de execução.

   C#

   :::image type="content" source="./media/debugging-with-visual-studio/step-into-method.png" alt-text="Método Intervir do Visual Studio – C#":::

   Visual Basic

   :::image type="content" source="./media/debugging-with-visual-studio/vb-step-into-method.png" alt-text="Método Intervir do Visual Studio – Visual Basic":::

   Neste ponto, a janela **locais** mostra que a `args` matriz está vazia e `name` `date` tem valores padrão. Além disso, o Visual Studio abriu uma janela de console em branco.

1. Pressione <kbd>F11</kbd>. O Visual Studio agora destaca a próxima linha de execução. A janela **locais** não é alterada e a janela do console permanece em branco.

   C#

   :::image type="content" source="./media/debugging-with-visual-studio/step-into-source-method.png" alt-text="Origem do método Intervir do Visual Studio – C#":::

   Visual Basic

   :::image type="content" source="./media/debugging-with-visual-studio/vb-step-into-source-method.png" alt-text="Origem do método Intervir do Visual Studio – Visual Basic":::

1. Pressione <kbd>F11</kbd>. O Visual Studio destaca a instrução que inclui a atribuição de variável `name`. A janela **locais** mostra que `name` é `null` , e a janela do console exibe a cadeia de caracteres "Qual é seu nome?".

1. Responda ao prompt inserindo uma cadeia de caracteres na janela do console e pressionando <kbd>Enter</kbd>. O console não está respondendo, e a cadeia de caracteres inserida não é exibida na janela do console, mas o método, no <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> entanto, captura sua entrada.

1. Pressione <kbd>F11</kbd>. O Visual Studio realça a instrução que inclui a `date` atribuição de variável ( `currentDate` em Visual Basic). A janela **locais** mostra o valor retornado pela chamada para o <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> método. A janela do console também exibe a cadeia de caracteres que você inseriu no prompt.

1. Pressione <kbd>F11</kbd>. A janela **locais** mostra o valor da `date` variável após a atribuição da <xref:System.DateTime.Now?displayProperty=nameWithType> propriedade. A janela do console não é alterada.

1. Pressione <kbd>F11</kbd>. O Visual Studio chama o método <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType>. A janela do console exibe a cadeia de caracteres formatada.

1. Escolha **depurar depuração**  >  **fora**. Outra maneira de parar a execução passo a passo é pressionar <kbd>Shift</kbd> + <kbd>F11</kbd>.

   A janela do console exibe uma mensagem e aguarda até que uma tecla seja pressionada.

1. Pressione qualquer tecla para fechar a janela do console e parar a depuração.

## <a name="use-release-build-configuration"></a>Usar a configuração de Build de versão

Depois de testar a versão de depuração do seu aplicativo, você também deve compilar e testar a versão de lançamento. A versão de lançamento incorpora otimizações do compilador que, às vezes, podem afetar negativamente o comportamento de um aplicativo. Por exemplo, as otimizações do compilador que são projetadas para melhorar o desempenho podem criar condições de corrida em aplicativos multissegmentados.

Para compilar e testar a versão de lançamento do seu aplicativo de console, altere a configuração de build na barra de ferramentas de **Depuração** para **Lançamento**.

:::image type="content" source="./media/debugging-with-visual-studio/visual-studio-toolbar-release.png" alt-text="barra de ferramentas do Visual Studio padrão com a versão realçada":::

Quando você pressiona <kbd>F5</kbd> ou escolhe **Compilar solução** no menu **Compilar** , o Visual Studio compila a versão de lançamento do aplicativo. Você pode testá-lo como fez a versão de depuração.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você usou as ferramentas de depuração do Visual Studio. No próximo tutorial, você publica uma versão implantável do aplicativo.

> [!div class="nextstepaction"]
> [Publicar um aplicativo de console .NET usando o Visual Studio](publishing-with-visual-studio.md)
