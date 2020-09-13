---
title: Criar uma biblioteca de classes de .NET Standard usando Visual Studio Code
description: Saiba como criar uma biblioteca de classes de .NET Standard usando Visual Studio Code.
ms.date: 06/08/2020
ms.openlocfilehash: 966b9b0b48f67809e82d9133c523995cd97b6015
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89495506"
---
# <a name="tutorial-create-a-net-standard-library-using-visual-studio-code"></a>Tutorial: criar uma biblioteca de .NET Standard usando Visual Studio Code

Neste tutorial, você cria uma biblioteca de utilitário simples que contém um único método de manipulação de cadeia de caracteres. Implemente-o como um [método de extensão](../../csharp/programming-guide/classes-and-structs/extension-methods.md) para que você possa chamá-lo como se fosse um membro da <xref:System.String> classe.

Uma *biblioteca de classes* define tipos e métodos que são chamados por um aplicativo. Uma biblioteca de classes que tem como alvo .NET Standard 2,0 permite que sua biblioteca seja chamada por qualquer implementação do .NET que dê suporte a essa versão do .NET Standard. Ao concluir a biblioteca de classes, você pode distribuí-la como um componente de terceiros ou como um componente agrupado com um ou mais aplicativos.

## <a name="prerequisites"></a>Pré-requisitos

1. [Visual Studio Code](https://code.visualstudio.com/) com a [extensão C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) instalada. Para obter informações sobre como instalar extensões em Visual Studio Code, consulte [vs Code Marketplace de extensão](https://code.visualstudio.com/docs/editor/extension-gallery).
2. O [SDK do .NET Core 3,1 ou posterior](https://dotnet.microsoft.com/download)

## <a name="create-a-solution"></a>Criar uma solução

Comece criando uma solução em branco para colocar o projeto de biblioteca de classes no. Uma solução serve como um contêiner para um ou mais projetos. Você adicionará mais projetos relacionados à mesma solução.

1. Iniciar o Visual Studio Code.

1. Selecione **arquivo**  >  **abrir pasta** (**abrir...** no MacOS) no menu principal

1. Na caixa de diálogo **abrir pasta** , crie uma pasta *ClassLibraryProjects* e clique em **Selecionar pasta** (**aberta** no MacOS).

1. Abra o **terminal** no Visual Studio Code selecionando **Exibir**  >  **terminal** no menu principal.

   O **terminal** é aberto com o prompt de comando na pasta *ClassLibraryProjects* .

1. No **terminal**, digite o seguinte comando:

   ```dotnetcli
   dotnet new sln
   ```

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   The template "Solution File" was created successfully.
   ```

## <a name="create-a-class-library-project"></a>Criar um projeto de biblioteca de classes

Adicione um novo projeto de biblioteca de classe .NET Standard chamado "StringLibrary" à solução.

1. No terminal, execute o seguinte comando para criar o projeto de biblioteca:

   ```dotnetcli
   dotnet new classlib -o StringLibrary
   ```

   O `-o` `--output` comando ou especifica o local para posicionar a saída gerada.

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   The template "Class library" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on StringLibrary\StringLibrary.csproj...
     Determining projects to restore...
     Restored C:\Projects\ClassLibraryProjects\StringLibrary\StringLibrary.csproj (in 328 ms).
   Restore succeeded.
   ```

1. Execute o seguinte comando para adicionar o projeto de biblioteca à solução:

   ```dotnetcli
   dotnet sln add StringLibrary/StringLibrary.csproj
   ```

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   Project `StringLibrary\StringLibrary.csproj` added to the solution.
   ```

1. Verifique se a biblioteca tem como destino a versão correta do .NET Standard. No **Explorer**, abra *StringLibrary/StringLibrary. csproj*.

   O `TargetFramework` elemento mostra que o projeto tem como destino .NET Standard 2,0.

   ```xml
   <Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
       <TargetFramework>netstandard2.0</TargetFramework>
     </PropertyGroup>

   </Project>
   ```

1. Abra *Class1.cs* e substitua o código pelo código a seguir.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

   A biblioteca de classes, `UtilityLibraries.StringLibrary` , contém um método chamado `StartsWithUpper` . Esse método retorna um <xref:System.Boolean> valor que indica se a instância atual da cadeia de caracteres começa com um caractere maiúsculo. O padrão Unicode distingue caracteres maiúsculos de caracteres minúsculos. O método <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> retornará `true` se um caractere for maiúsculo.

1. Salve o arquivo.

1. Execute o comando a seguir para compilar a solução e verificar se o projeto é compilado sem erros.

   ```dotnetcli
   dotnet build
   ```

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   Microsoft (R) Build Engine version 16.7.0+b89cb5fde for .NET
   Copyright (C) Microsoft Corporation. All rights reserved.
     Determining projects to restore...
     All projects are up-to-date for restore.
     StringLibrary -> C:\Projects\ClassLibraryProjects\StringLibrary\bin\Debug\netstandard2.0\StringLibrary.dll
   Build succeeded.
       0 Warning(s)
       0 Error(s)
   Time Elapsed 00:00:02.78
   ```

## <a name="add-a-console-app-to-the-solution"></a>Adicionar um aplicativo de console à solução

Adicione um aplicativo de console que usa a biblioteca de classes. O aplicativo solicitará que o usuário insira uma cadeia de caracteres e relate se a cadeia de caracteres começa com um caractere maiúsculo.

1. No terminal, execute o seguinte comando para criar o projeto de aplicativo de console:

   ```dotnetcli
   dotnet new console -o ShowCase
   ```

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   The template "Console Application" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on ShowCase\ShowCase.csproj...  
     Determining projects to restore...
     Restored C:\Projects\ClassLibraryProjects\ShowCase\ShowCase.csproj (in 210 ms).
   Restore succeeded.
   ```

1. Execute o seguinte comando para adicionar o projeto de aplicativo de console à solução:

   ```dotnetcli
   dotnet sln add ShowCase/ShowCase.csproj
   ```

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   Project `ShowCase\ShowCase.csproj` added to the solution.
   ```

1. Abra o *Showcase/Program. cs* e substitua todo o código pelo código a seguir.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   O código usa a variável `row` ​​para manter uma contagem do número de linhas de dados gravadas na janela do console. Sempre que for maior ou igual a 25, o código limpará a janela do console e exibirá uma mensagem para o usuário.

   O programa solicita que o usuário insira uma cadeia de caracteres. Ele indica se a cadeia de caracteres começa com um caractere maiúsculo. Se o usuário pressionar a tecla <kbd>Enter</kbd> sem inserir uma cadeia de caracteres, o aplicativo será encerrado e a janela do console será fechada.

1. Salve suas alterações.

## <a name="add-a-project-reference"></a>Adicionar uma referência ao projeto

Inicialmente, o novo projeto de aplicativo de console não tem acesso à biblioteca de classes. Para permitir que ele chame métodos na biblioteca de classes, crie uma referência de projeto para o projeto de biblioteca de classes.

1. Execute o seguinte comando:

   ```dotnetcli
   dotnet add ShowCase/ShowCase.csproj reference StringLibrary/StringLibrary.csproj
   ```

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   Reference `..\StringLibrary\StringLibrary.csproj` added to the project.
   ```

## <a name="run-the-app"></a>Executar o aplicativo

1. Execute o seguinte comando no terminal:

   ```dotnetcli
   dotnet run --project ShowCase/ShowCase.csproj
   ```

1. Experimente o programa digitando cadeias de caracteres e pressionando <kbd>Enter</kbd>e pressione <kbd>Enter</kbd> para sair.

   A saída do terminal é semelhante ao exemplo a seguir:

   ```output
   Press <Enter> only to exit; otherwise, enter a string and press <Enter>:

   A string that starts with an uppercase letter
   Input: A string that starts with an uppercase letter
   Begins with uppercase? : Yes

   a string that starts with a lowercase letter
   Input: a string that starts with a lowercase letter
   Begins with uppercase? : No
   ```

## <a name="additional-resources"></a>Recursos adicionais

* [Desenvolver bibliotecas com o CLI do .NET Core](libraries.md)
* [.Net Standard versões e plataformas às quais eles dão suporte](../../standard/net-standard.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou uma solução, adicionou um projeto de biblioteca e adicionou um projeto de aplicativo de console que usa a biblioteca do. No próximo tutorial, você adicionará um projeto de teste de unidade à solução.

> [!div class="nextstepaction"]
> [Testar uma biblioteca de .NET Standard com o .NET Core usando Visual Studio Code](testing-library-with-visual-studio-code.md)
