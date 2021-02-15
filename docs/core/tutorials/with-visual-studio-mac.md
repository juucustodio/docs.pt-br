---
title: Criar um aplicativo de console .NET usando Visual Studio para Mac
description: Saiba como criar um aplicativo de console .NET usando Visual Studio para Mac.
ms.date: 11/30/2020
ms.openlocfilehash: 1351b06eec32cd8d3d9d44926655405fe2246f58
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599480"
---
# <a name="tutorial-create-a-net-console-application-using-visual-studio-for-mac"></a>Tutorial: criar um aplicativo de console .NET usando o Visual Studio para Mac

Este tutorial mostra como criar e executar um aplicativo de console .NET usando Visual Studio para Mac.

> [!NOTE]
> Seus comentários são muito importantes. Há duas maneiras de enviar comentários à equipe de desenvolvimento no Visual Studio para Mac:
>
> * Em Visual Studio para Mac, selecione **ajuda** para  >  **relatar um problema** no menu ou **relatar um problema** na tela de boas-vindas, que abrirá uma janela para o arquivamento de um relatório de bug. Você pode acompanhar seus comentários no portal [Developer Community (Comunidade do Desenvolvedor)](https://aka.ms/feedback/report?space=41).
> * Para fazer uma sugestão, selecione **ajuda**  >  **fornecer uma sugestão** no menu ou **forneça uma sugestão** na tela de boas-vindas, que levará você para a [página da Web do Visual Studio para Mac Developer Community](https://aka.ms/feedback/suggest?space=41).

## <a name="prerequisites"></a>Pré-requisitos

* [Visual Studio para Mac versão 8,8 ou posterior](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link). Selecione a opção para instalar o .NET Core. A instalação do Xamarin é opcional para o desenvolvimento do .NET. Para obter mais informações, consulte os seguintes recursos:

  * [Tutorial: instalar o Visual Studio para Mac](/visualstudio/mac/installation).
  * [Versões do MacOS com suporte](../install/windows.md).
  * [Versões do .NET com suporte pelo Visual Studio para Mac](/visualstudio/mac/net-core-support).

## <a name="create-the-app"></a>Crie o aplicativo

1. Iniciar Visual Studio para Mac.

1. Selecione **novo** na janela iniciar.

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="O botão Novo na tela de Boas-vindas do Visual Studio para Mac":::

1. Na caixa de diálogo **novo projeto** , selecione **aplicativo** no nó **Web e console** . Selecione o modelo de **aplicativo de console** e selecione **Avançar**.

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-dialog.png" alt-text="Lista de modelos de novo projeto":::

1. Na lista suspensa **estrutura de destino** da caixa de diálogo **configurar seu novo aplicativo de console** , selecione **.NET 5,0** e selecione **Avançar**.

1. Digite "HelloWorld" para o **nome do projeto** e selecione **criar**.

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-options.png" alt-text="Configurar a caixa de diálogo Novo Aplicativo de Console":::

O modelo cria um simples aplicativo “Olá, Mundo”. Ele chama o <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> método para exibir "Olá, mundo!" na janela do terminal.

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

`Main` é o ponto de entrada do aplicativo, o método que é chamado automaticamente pelo runtime quando ele inicia o aplicativo. Todos os argumentos de linha de comando fornecidos quando o aplicativo é iniciado estão disponíveis na `args` matriz.

## <a name="run-the-app"></a>Execute o aplicativo

1. Pressione <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd> + <kbd>comando</kbd>Option + <kbd>Enter</kbd>) para executar o aplicativo sem depuração.

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-output.png" alt-text="O terminal mostra Olá, Mundo!":::

1. Feche a janela do **terminal** .

## <a name="enhance-the-app"></a>Aprimorar o aplicativo

Aprimore o aplicativo para solicitar ao usuário seu nome e exibi-lo junto com a data e hora.

1. No *Program.cs*, substitua o conteúdo do `Main` método, que é a linha que chama `Console.WriteLine` , com o seguinte código:

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::

   Esse código exibe um prompt na janela do console e aguarda até que o usuário insira uma cadeia de caracteres seguida pela tecla <kbd>Enter</kbd> . Ele armazena essa cadeia de caracteres em uma variável chamada `name` . Ele também recupera o valor da propriedade <xref:System.DateTime.Now?displayProperty=nameWithType>, que contém a hora local atual e o atribui a uma variável chamada `date`. E ele exibe esses valores na janela do console. Por fim, ele exibe um prompt na janela do console e chama o <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> método para aguardar a entrada do usuário.

   O `\n` representa um caractere de nova linha.

   O cifrão ( `$` ) na frente de uma cadeia de caracteres permite que você coloque expressões como nomes de variáveis entre chaves na cadeia de caracteres. O valor da expressão é inserido na cadeia de caracteres no lugar da expressão. Essa sintaxe é conhecida como [cadeias de caracteres interpoladas](../../csharp/language-reference/tokens/interpolated.md).

1. Pressione <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd> + <kbd>comando</kbd>Option + <kbd>Enter</kbd>) para executar o aplicativo.

1. Responda ao prompt digitando um nome e pressionando <kbd>Enter</kbd>.

   :::image type="content" source="media/with-visual-studio-mac/hello-world-update.png" alt-text="Terminal mostra a saída de programa modificada":::

1. Feche o terminal.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um aplicativo de console .NET. No próximo tutorial, você depurará o aplicativo.

> [!div class="nextstepaction"]
> [Depurar um aplicativo de console .NET usando Visual Studio para Mac](debugging-with-visual-studio-mac.md)
