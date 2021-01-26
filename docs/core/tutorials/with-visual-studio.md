---
title: Criar um aplicativo de console .NET usando o Visual Studio
description: Saiba como criar um aplicativo de console .NET com C# ou Visual Basic usando o Visual Studio.
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: a3a27c1baaab135108ef475d77c35d607c45fa82
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794795"
---
# <a name="tutorial-create-a-net-console-application-using-visual-studio"></a>Tutorial: criar um aplicativo de console .NET usando o Visual Studio

Este tutorial mostra como criar e executar um aplicativo de console .NET no Visual Studio 2019.

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2019 versão 16,8 ou uma versão posterior](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) com a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** instalada. O SDK do .NET 5,0 é instalado automaticamente quando você seleciona essa carga de trabalho.

  Para obter mais informações, consulte [instalar o SDK do .NET com o Visual Studio](../install/windows.md#install-with-visual-studio).

## <a name="create-the-app"></a>Criar o aplicativo

Crie um projeto de aplicativo de console .NET chamado "HelloWorld".

1. Inicie o Visual Studio 2019.

1. Selecione **ferramentas**  >  **Opções**  >    >  **recursos de visualização** de ambiente e, em seguida, selecione **Mostrar todos os modelos do .NET Core no novo projeto (requer reinicialização)**.

   :::image type="content" source="media/with-visual-studio/dotnet-options.png" alt-text="Opção Mostrar todos os modelos do .NET":::

1. Feche e reabra o Visual Studio.

1. Na página inicial, escolha **criar um novo projeto**.

   :::image type="content" source="./media/with-visual-studio/start-window.png" alt-text="Criar um novo botão de projeto selecionado na página inicial do Visual Studio":::

1. Na página **criar um novo projeto** , insira **console** na caixa de pesquisa. Em seguida, escolha **C#** ou **Visual Basic** na lista idioma e, em seguida, escolha **todas as plataformas** na lista plataforma. Escolha o modelo de **aplicativo de console** e, em seguida, escolha **Avançar**.

   :::image type="content" source="./media/with-visual-studio/create-new-project.png" alt-text="Criar uma nova janela de projeto com filtros selecionados":::

   > [!TIP]
   > Se você não vir os modelos .NET, provavelmente está faltando a carga de trabalho necessária. Na mensagem **não localizando o que você está procurando?** , escolha o link **instalar mais ferramentas e recursos** . O Instalador do Visual Studio é aberto. Verifique se você tem a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** instalada.

1. No diálogo **configurar seu novo projeto** , digite **HelloWorld** na caixa **nome do projeto** . Em seguida, escolha **Criar**.

   :::image type="content" source="./media/with-visual-studio/configure-new-project.png" alt-text="Configurar sua nova janela de projeto com os campos nome do projeto, local e nome da solução":::

1. Na caixa de diálogo **informações adicionais** , selecione **.NET 5,0 (atual)** e, em seguida, selecione **criar**.

   :::image type="content" source="media/with-visual-studio/additional-info.png" alt-text="Caixa de diálogo Informações adicionais":::

O modelo cria um simples aplicativo “Olá, Mundo”. Ele chama o <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> método para exibir "Olá, mundo!" na janela do console.

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

```vb
Imports System

Module Program
    Sub Main(args As String())
        Console.WriteLine("Hello World!")
    End Sub
End Module
```

`Main` é o ponto de entrada do aplicativo, o método que é chamado automaticamente pelo runtime quando ele inicia o aplicativo. Quaisquer argumentos de linha de comando fornecidos quando o aplicativo for iniciado estão disponíveis na matriz *args*.

Se o idioma que você deseja usar não for mostrado, altere o seletor de idioma na parte superior da página.

## <a name="run-the-app"></a>Execute o aplicativo

1. Pressione <kbd>Ctrl</kbd> + <kbd>F5</kbd> para executar o programa sem depuração.

   Uma janela de console é aberta com o texto "Olá, Mundo!" impresso na tela.

   :::image type="content" source="./media/with-visual-studio/hello-world-console.png" alt-text="Janela de console mostrando Hello World Press any key to continue":::

1. Pressione qualquer tecla para fechar a janela do console.

## <a name="enhance-the-app"></a>Aprimorar o aplicativo

Aprimore o aplicativo para solicitar ao usuário seu nome e exibi-lo junto com a data e hora.

1. Em *Program.cs* ou *Program. vb*, substitua o conteúdo do `Main` método, que é a linha que chama `Console.WriteLine` , com o seguinte código:

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::
   :::code language="vb" source="./snippets/with-visual-studio/vb/Program.vb" id="MainMethod":::

   Esse código exibe um prompt na janela do console e aguarda até que o usuário insira uma cadeia de caracteres seguida pela tecla <kbd>Enter</kbd> . Ele armazena essa cadeia de caracteres em uma variável chamada `name` . Ele também recupera o valor da <xref:System.DateTime.Now?displayProperty=nameWithType> propriedade, que contém a hora local atual e a atribui a uma variável chamada `date` ( `currentDate` em Visual Basic). E ele exibe esses valores na janela do console. Por fim, ele exibe um prompt na janela do console e chama o <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> método para aguardar a entrada do usuário.

   O `\n` (ou `vbCrLf` no código de Visual Basic) representa um caractere de nova linha.

   O cifrão ( `$` ) na frente de uma cadeia de caracteres permite que você coloque expressões como nomes de variáveis entre chaves na cadeia de caracteres. O valor da expressão é inserido na cadeia de caracteres no lugar da expressão. Essa sintaxe é conhecida como [cadeias de caracteres interpoladas](../../csharp/language-reference/tokens/interpolated.md).

1. Pressione <kbd>Ctrl</kbd> + <kbd>F5</kbd> para executar o programa sem depuração.

1. Responda ao prompt digitando um nome e pressionando a tecla <kbd>Enter</kbd> .

   :::image type="content" source="./media/with-visual-studio/hello-world-update.png" alt-text="Janela de console com saída de programa modificada":::

1. Pressione qualquer tecla para fechar a janela do console.

## <a name="additional-resources"></a>Recursos adicionais

- [Versões atuais e versões de suporte a longo prazo](../releases-and-support.md#net-core-and-net-5-version-lifecycles)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um aplicativo de console .NET. No próximo tutorial, você depurará o aplicativo.

> [!div class="nextstepaction"]
> [Depurar um aplicativo de console .NET usando o Visual Studio](debugging-with-visual-studio.md)
