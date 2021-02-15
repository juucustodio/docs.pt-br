---
title: Organizando e testando projetos com a CLI do .NET
description: Este tutorial explica como organizar e testar projetos .NET na linha de comando.
author: cartermp
ms.date: 09/10/2018
ms.openlocfilehash: 263eaf15beac008de8bb353a385b8f3588a7fefc
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633631"
---
# <a name="organizing-and-testing-projects-with-the-net-cli"></a>Organizando e testando projetos com a CLI do .NET

Este tutorial segue o [tutorial: criar um aplicativo de console com o .NET usando Visual Studio Code](with-visual-studio-code.md), levando você além da criação de um aplicativo de console simples para desenvolver aplicativos avançados e bem organizados. Depois de mostrar como usar pastas para organizar seu código, este tutorial mostra como estender um aplicativo de console com a estrutura de teste [xUnit](https://xunit.net/).

## <a name="using-folders-to-organize-code"></a>Usar pastas para organizar o código

Se você quiser introduzir novos tipos em um aplicativo de console, poderá fazer isso adicionando arquivos que contêm os tipos para o aplicativo. Por exemplo, se você adicionar arquivos contendo os tipos `AccountInformation` e `MonthlyReportRecords` ao seu projeto, a estrutura do arquivo de projeto será simples e fácil de navegar:

```
/MyProject
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

No entanto, isso funciona bem apenas quando o projeto é relativamente pequeno. Você pode imaginar o que acontecerá se adicionar 20 tipos ao projeto? O projeto definitivamente não será fácil navegar e manter com tantos arquivos dividindo o diretório raiz do projeto.

Para organizar o projeto, crie uma nova pasta e nomeie-a como *Modelos* para armazenar os arquivos do tipo. Coloque os arquivos de tipo na pasta *Modelos*:

```
/MyProject
|__/Models
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

Projetos que agrupam arquivos em pastas de forma lógica são fáceis de navegar e manter. Na próxima seção, você criará um exemplo mais complexo com pastas e testes de unidade.

## <a name="organizing-and-testing-using-the-newtypes-pets-sample"></a>Organizando e testando usando o Exemplo Pets de NewTypes

### <a name="prerequisites"></a>Pré-requisitos

* [SDK do .net 5,0](https://dotnet.microsoft.com/download) ou uma versão posterior.

### <a name="building-the-sample"></a>Compilando o exemplo

Para as etapas a seguir, você pode acompanhar usando o [NewTypes Pets Sample](https://github.com/dotnet/samples/tree/master/core/console-apps/NewTypesMsBuild) (Exemplo Pets de NewTypes) ou criar seus próprios arquivos e pastas. Os tipos são organizados logicamente em uma estrutura de pastas que permite a adição de mais tipos posteriormente e os testes também são posicionados logicamente nas pastas, permitindo a adição de mais testes posteriormente.

Esse exemplo contém dois tipos, `Dog` e `Cat`, e faz com que eles implementem uma interface comum, `IPet`. Para o projeto `NewTypes`, sua meta é organizar os tipos relacionados a animais de estimação em uma pasta *Pets*. Se outro conjunto de tipos for adicionado posteriormente, *WildAnimals* por exemplo, ele será colocado na pasta *NewTypes* junto com a pasta *Pets*. A pasta *WildAnimals* pode conter tipos de animais que não são animais de estimação, como os tipos `Squirrel` e `Rabbit`. Dessa forma, conforme os tipos são adicionados, o projeto continua bem organizado.

Crie a seguinte estrutura de pasta com o conteúdo do arquivo indicado:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
```

*IPet.cs*:

[!code-csharp[IPet interface](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/IPet.cs)]

*Dog.cs*:

[!code-csharp[Dog class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/Dog.cs)]

*Cat.cs*:

[!code-csharp[Cat class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Pets/Cat.cs)]

*Program.cs*:

[!code-csharp[Main](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/Program.cs)]

*NewTypes.csproj*:

[!code-xml[NewTypes csproj](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/src/NewTypes/NewTypes.csproj)]

Execute o seguinte comando:

```dotnetcli
dotnet run
```

Obtenha a seguinte saída:

```console
Woof!
Meow!
```

Exercício opcional: você pode adicionar um novo tipo de animal de estimação, como um `Bird`, estendendo esse projeto. Faça com que o método `TalkToOwner` de pássaro dê um `Tweet!` para o proprietário. Execute o aplicativo novamente. A saída incluirá `Tweet!`

### <a name="testing-the-sample"></a>Testando o exemplo

O projeto `NewTypes` está em funcionamento e você o organizou mantendo os tipos relacionados a animais de estimação em uma pasta. Em seguida, crie seu projeto de teste e comece a escrever testes com a estrutura de teste [xUnit](https://xunit.net/). O teste de unidade permite que você verifique automaticamente o comportamento dos seus tipos de animal de estimação para confirmar se eles estão funcionando corretamente.

Navegue de volta para a pasta *src* e crie uma pasta *test* com uma pasta *NewTypesTests* dentro dela. Em um prompt de comando da pasta *NewTypesTests*, execute `dotnet new xunit`. Isso gera dois arquivos: *NewTypesTests.csproj* e *UnitTest1.cs*.

No momento, o projeto de teste não pode testar os tipos no `NewTypes` e requer uma referência de projeto para o projeto `NewTypes`. Para adicionar uma referência de projeto, use o [`dotnet add reference`](../tools/dotnet-add-reference.md) comando:

```dotnetcli
dotnet add reference ../../src/NewTypes/NewTypes.csproj
```

Se preferir, adicione manualmente a referência de projeto adicionando um nó `<ItemGroup>` ao arquivo *NewTypesTests.csproj*:

```xml
<ItemGroup>
  <ProjectReference Include="../../src/NewTypes/NewTypes.csproj" />
</ItemGroup>
```

*NewTypesTests.csproj*:

[!code-xml[NewTypesTests csproj](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/test/NewTypesTests/NewTypesTests.csproj)]

O arquivo *NewTypesTests.csproj* com o seguinte:

* Referência de pacote para `Microsoft.NET.Test.Sdk`, a infraestrutura de teste do .NET
* Referência de pacote para `xunit`, a estrutura de teste do xUnit
* Referência de pacote para `xunit.runner.visualstudio`, o executor de teste
* Referência de projeto para `NewTypes`, o código a ser testado

Altere o nome de *UnitTest1.cs* para *PetTests.cs* e substitua o código no arquivo pelo seguinte:

```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }

    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }
}
```

Exercício opcional: se você adicionou um tipo `Bird` anteriormente que produz um `Tweet!` para o proprietário, adicione um método de teste ao arquivo *PetTests.cs*, `BirdTalkToOwnerReturnsTweet`, para verificar se o método `TalkToOwner` funciona corretamente para o tipo `Bird`.

> [!NOTE]
> Embora você espere que os valores `expected` e `actual` sejam iguais, uma declaração inicial com a verificação `Assert.NotEqual` especifica que esses valores *não são iguais*. Sempre crie inicialmente os testes para falhar para verificar a lógica do teste. Depois de confirmar que o teste falhou, ajuste a declaração para permitir que o teste seja aprovado.

O código a seguir mostra a estrutura do projeto completo:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```

Inicie no diretório *test/NewTypesTests*. Execute os testes com o [`dotnet test`](../tools/dotnet-test.md) comando. Esse comando inicia o executor de teste especificado no arquivo de projeto.

Conforme o esperado, o teste falha e o console exibe a seguinte saída:

```output
Test run for C:\Source\dotnet\docs\samples\snippets\core\tutorials\testing-with-cli\csharp\test\NewTypesTests\bin\Debug\net5.0\NewTypesTests.dll (.NETCoreApp,Version=v5.0)
Microsoft (R) Test Execution Command Line Tool Version 16.8.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
A total of 1 test files matched the specified pattern.
[xUnit.net 00:00:00.50]     PetTests.DogTalkToOwnerReturnsWoof [FAIL]
  Failed PetTests.DogTalkToOwnerReturnsWoof [6 ms]
  Error Message:
   Assert.NotEqual() Failure
Expected: Not "Woof!"
Actual:   "Woof!"
  Stack Trace:
     at PetTests.DogTalkToOwnerReturnsWoof() in C:\Source\dotnet\docs\samples\snippets\core\tutorials\testing-with-cli\csharp\test\NewTypesTests\PetTests.cs:line 13

Failed!  - Failed:     1, Passed:     1, Skipped:     0, Total:     2, Duration: 8 ms - NewTypesTests.dll (net5.0)
```

Altere as asserções de seus testes de `Assert.NotEqual` para `Assert.Equal`:

[!code-csharp[PetTests class](../../../samples/snippets/core/tutorials/testing-with-cli/csharp/test/NewTypesTests/PetTests.cs)]

Execute novamente os testes com o comando `dotnet test` e obtenha a seguinte saída:

```output
Test run for C:\Source\dotnet\docs\samples\snippets\core\tutorials\testing-with-cli\csharp\test\NewTypesTests\bin\Debug\net5.0\NewTypesTests.dll (.NETCoreApp,Version=v5.0)
Microsoft (R) Test Execution Command Line Tool Version 16.8.1
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
A total of 1 test files matched the specified pattern.

Passed!  - Failed:     0, Passed:     2, Skipped:     0, Total:     2, Duration: 2 ms - NewTypesTests.dll (net5.0)
```

O teste é aprovado. Os métodos dos tipos de animais de estimação retornam os valores corretos ao conversar com o proprietário.

Você aprendeu técnicas para organizar e testar projetos usando xUnit. Prossiga com essas técnicas aplicando-as em seus próprios projetos. *Boa codificação!*
