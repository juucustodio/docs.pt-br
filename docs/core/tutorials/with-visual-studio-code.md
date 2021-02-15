---
title: Criar um aplicativo de console .NET usando Visual Studio Code
description: Saiba como criar um aplicativo de console .NET usando Visual Studio Code e a CLI do .NET.
ms.date: 11/17/2020
ms.openlocfilehash: dbbdf88b0c84089249eb7e446c25eddc11543c1a
ms.sourcegitcommit: 5114e7847e0ff8ddb8c266802d47af78567949cf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94915863"
---
# <a name="tutorial-create-a-net-console-application-using-visual-studio-code"></a>Tutorial: criar um aplicativo de console .NET usando o Visual Studio Code

Este tutorial mostra como criar e executar um aplicativo de console .NET usando Visual Studio Code e a CLI do .NET. Tarefas de projeto, como criar, compilar e executar um projeto, são feitas usando a CLI do .NET. Você pode seguir este tutorial com um editor de código diferente e executar comandos em um terminal, se preferir.

## <a name="prerequisites"></a>Pré-requisitos

1. [Visual Studio Code](https://code.visualstudio.com/) com a [extensão C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) instalada. Para obter informações sobre como instalar extensões em Visual Studio Code, consulte [vs Code Marketplace de extensão](https://code.visualstudio.com/docs/editor/extension-gallery).
2. O [SDK do .net 5,0 ou posterior](https://dotnet.microsoft.com/download)

## <a name="create-the-app"></a>Criar o aplicativo

Crie um projeto de aplicativo de console .NET chamado "HelloWorld".

1. Inicie o Visual Studio Code.

1. Selecione **arquivo**  >  **abrir pasta** (**arquivo**  >  **aberto...** no MacOS) no menu principal.

1. Na caixa de diálogo **abrir pasta** , crie uma pasta *HelloWorld* e clique em **Selecionar pasta** (**aberta** no MacOS).

   O nome da pasta torna-se o nome do projeto e o nome do namespace por padrão. Você adicionará código posteriormente no tutorial que assume que o namespace do projeto é `HelloWorld` .

1. Abra o **terminal** no Visual Studio Code selecionando **Exibir**  >  **terminal** no menu principal.

   O **terminal** é aberto com o prompt de comando na pasta *HelloWorld* .

1. No **terminal**, digite o seguinte comando:

   ```dotnetcli
   dotnet new console
   ```

O modelo cria um simples aplicativo “Olá, Mundo”. Ele chama o <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> método para exibir " :::no-loc text="Hello World!"::: " na janela do console.

O código de modelo define uma classe, `Program` , com um único método, `Main` , que usa uma <xref:System.String> matriz como um argumento:

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

`Main` é o ponto de entrada do aplicativo, o método que é chamado automaticamente pelo runtime quando ele inicia o aplicativo. Quaisquer argumentos de linha de comando fornecidos quando o aplicativo for iniciado estão disponíveis na matriz *args*.

## <a name="run-the-app"></a>Executar o aplicativo

Execute o seguinte comando no **terminal**:

```dotnetcli
dotnet run
```

O programa exibe "Olá, Mundo!" e termina.

![O comando de execução dotnet](media/with-visual-studio-code/dotnet-run-command.png)

## <a name="enhance-the-app"></a>Aprimorar o aplicativo

Aprimore o aplicativo para solicitar ao usuário seu nome e exibi-lo junto com a data e hora.

1. Abra *Program.cs* clicando nele.

   Na primeira vez que um arquivo do C# é aberto no Visual Studio Code, o [OmniSharp](https://www.omnisharp.net/) é carregado no editor.

   ![Abra o arquivo Program.cs](media/with-visual-studio-code/open-program-cs.png)

1. Selecione **Sim** quando Visual Studio Code solicitar que você adicione os ativos ausentes para compilar e depurar seu aplicativo.

   ![Prompt para ativos ausentes](media/with-visual-studio-code/missing-assets.png)

1. Substitua o conteúdo do `Main` método em *Program.cs*, que é a linha que chama `Console.WriteLine` , com o seguinte código:

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::

   Esse código exibe um prompt na janela do console e aguarda até que o usuário insira uma cadeia de caracteres seguida pela tecla <kbd>Enter</kbd> . Ele armazena essa cadeia de caracteres em uma variável chamada `name` . Ele também recupera o valor da propriedade <xref:System.DateTime.Now?displayProperty=nameWithType>, que contém a hora local atual e o atribui a uma variável chamada `date`. E ele exibe esses valores na janela do console. Por fim, ele exibe um prompt na janela do console e chama o <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> método para aguardar a entrada do usuário.

   O `\n` representa um caractere de nova linha.

   O cifrão ( `$` ) na frente de uma cadeia de caracteres permite que você coloque expressões como nomes de variáveis entre chaves na cadeia de caracteres. O valor da expressão é inserido na cadeia de caracteres no lugar da expressão. Essa sintaxe é conhecida como [cadeias de caracteres interpoladas](../../csharp/language-reference/tokens/interpolated.md).

1. Salve suas alterações.

   > [!IMPORTANT]
   > No Visual Studio Code, você precisa salvar explicitamente as alterações. Ao contrário do Visual Studio, as alterações de arquivo não são salvas automaticamente quando você compila e executa um aplicativo.

1. Execute o programa novamente:

   ```dotnetcli
   dotnet run
   ```

1. Responda ao prompt digitando um nome e pressionando a tecla <kbd>Enter</kbd> .

   :::image type="content" source="media/debugging-with-visual-studio-code/run-modified-program.png" alt-text="Janela do terminal com saída do programa modificada":::

1. Pressione qualquer tecla para encerrar o programa.

## <a name="additional-resources"></a>Recursos adicionais

- [Configurar o Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um aplicativo de console .NET. No próximo tutorial, você depurará o aplicativo.

> [!div class="nextstepaction"]
> [Depurar um aplicativo de console .NET usando Visual Studio Code](debugging-with-visual-studio-code.md)
