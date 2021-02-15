---
title: Referência de F# Interativo (dotnet)
description: 'Saiba como F# Interativo (dotNet FSI) é usado para executar o código F # interativamente no console ou para executar scripts em F #.'
ms.date: 11/29/2020
f1_keywords:
- VS.ToolsOptionsPages.F#_Tools.F#_Interactive
ms.openlocfilehash: fe48d4d7de92eea800a489b12342e3ae181e8cb1
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99426964"
---
# <a name="interactive-programming-with-f"></a>Programação interativa com F\#

F# Interativo (dotNet FSI) é usado para executar o código F # interativamente no console ou para executar scripts em F #. Em outras palavras, o F# interativo executa um REPL (Ler, Avaliar, Imprimir Loop) para a linguagem F#.

Para executar o F# Interativo no console do, execute `dotnet fsi` . Você encontrará `dotnet fsi` em qualquer SDK do .net.

Para obter informações sobre opções de linha de comando disponíveis, consulte [Opções de F# interativo](../../language-reference/fsharp-interactive-options.md).

## <a name="executing-code-directly-in-f-interactive"></a>Executando o código diretamente no F# Interativo

Como F# Interativo é uma REPL (loop Read-eval-Print), você pode executar o código interativamente nele. Aqui está um exemplo de uma sessão interativa após `dotnet fsi` a execução na linha de comando:

```console
Microsoft (R) F# Interactive version 11.0.0.0 for F# 5.0
Copyright (c) Microsoft Corporation. All Rights Reserved.

For help type #help;;

> let square x = x *  x;;
val square : x:int -> int

> square 12;;
val it : int = 144

> printfn "Hello, FSI!"
- ;;
Hello, FSI!
val it : unit = ()
```

Você observará duas coisas principais:

1. Todo o código deve ser encerrado com um ponto-e-vírgula duplo ( `;;` ) a ser avaliado
2. O código é avaliado e armazenado em um `it` valor. Você pode fazer referência `it` interativamente.

F# Interativo também dá suporte à entrada de várias linhas. Você só precisa encerrar o envio com um ponto-e-vírgula duplo ( `;;` ). Considere o trecho a seguir que foi colado e avaliado por F# Interativo:

```console
> let getOddSquares xs =
-     xs
-     |> List.filter (fun x -> x % 2 <> 0)
-     |> List.map (fun x -> x * x)
-
- printfn "%A" (getOddSquares [1..10]);;
[1; 9; 25; 49; 81]
val getOddSquares : xs:int list -> int list
val it : unit = ()

>
```

A formatação do código é preservada e há um ponto-e-vírgula duplo ( `;;` ) encerrando a entrada. F# Interativo, em seguida, avaliou o código e imprimiu os resultados!

## <a name="scripting-with-f"></a>Criando scripts com o F\#

Avaliar o código interativamente no F# Interativo pode ser uma excelente ferramenta de aprendizado, mas você descobrirá rapidamente que não é tão produtivo quanto escrever código em um editor normal. Para dar suporte à edição de código normal, você pode escrever scripts em F #.

Os scripts usam a extensão de arquivo **. fsx**. Em vez de compilar o código-fonte e, posteriormente, executar o assembly compilado, você pode apenas executar **dotnet FSI** e especificar o nome de arquivo do script do código-fonte f # e o f # Interactive lê o código e o executa em tempo real. Por exemplo, considere o script a seguir chamado `Script.fsx` :

```fsharp
let getOddSquares xs =
    xs
    |> List.filter (fun x -> x % 2 <> 0)
    |> List.map (fun x -> x * x)

printfn "%A" (getOddSquares [1..10])
```

Quando esse arquivo é criado em seu computador, você pode executá-lo com `dotnet fsi` e ver a saída diretamente na janela do seu terminal:

```console
dotnet fsi Script.fsx
[1; 9; 25; 49; 81]
```

O script F # tem suporte nativo no [Visual Studio](../../get-started/get-started-visual-studio.md), [Visual Studio Code](../../get-started/get-started-vscode.md)e [Visual Studio para Mac](../../get-started/get-started-with-visual-studio-for-mac.md).

## <a name="referencing-packages-in-f-interactive"></a>Referenciando pacotes no F# Interativo

> [!NOTE]
> O sistema de gerenciamento de pacotes é extensível, leia mais [sobre outras extensões](https://fsharp.github.io/FSharp.Compiler.Service/reference/Microsoft.DotNet.DependencyManager.html).

O F# Interativo dá suporte à referência de pacotes NuGet com a `#r "nuget:"` sintaxe e uma versão opcional:

```fsharp
#r "nuget: Newtonsoft.Json"
open Newtonsoft.Json

let data = {| Name = "Don Syme"; Occupation = "F# Creator" |}
JsonConvert.SerializeObject(data)
```

Se uma versão não for especificada, o pacote de não visualização mais alto disponível será obtido. Para fazer referência a uma versão específica, introduza a versão por vírgula. Isso pode ser útil ao fazer referência a uma versão de visualização de um pacote. Por exemplo, considere este script usando uma versão de visualização do [DiffSharp](https://diffsharp.github.io/):

```fsharp
#r "nuget: DiffSharp-lite, 1.0.0-preview-328097867"
open DiffSharp

// A 1D tensor
let t1 = dsharp.tensor [ 0.0 .. 0.2 .. 1.0 ]

// A 2x2 tensor
let t2 = dsharp.tensor [ [ 0; 1 ]; [ 2; 2 ] ]

// Define a scalar-to-scalar function
let f (x: Tensor) = sin (sqrt x)

printfn $"{f (dsharp.tensor 1.2)}"
```

### <a name="specifying-a-package-source"></a>Especificando uma origem de pacote

Você também pode especificar uma origem de pacote com o `#i` comando. O exemplo a seguir especifica uma fonte remota e local:

```fsharp
#i "nuget:https://my-remote-package-source/index.json"
#i @"path-to-my-local-source"
```

Isso fará com que o mecanismo de resolução nos bastidores também leve em consideração as fontes remotas e/ou locais adicionadas a um script.

Você pode especificar quantas referências de pacote desejar em um script.

> [!NOTE]
> Atualmente, há uma limitação para scripts que usam referências de estrutura (por exemplo, `Microsoft.NET.Sdk.Web` ou  `Microsoft.NET.Sdk.WindowsDesktop` ). Pacotes como Saturn, Giraffe, WinForms não estão disponíveis. Isso está sendo acompanhado em questão [#9417](https://github.com/dotnet/fsharp/issues/9417).

Para obter mais informações, consulte [extensibilidade de gerenciamento de pacotes e outras extensões](https://github.com/dotnet/fsharp/tree/main/src/fsharp/Microsoft.DotNet.DependencyManager).

## <a name="referencing-assemblies-on-disk-with-f-interactive"></a>Referenciando assemblies em disco com F # interativo

Como alternativa, se você tiver um assembly em disco e desejar fazer referência a ele em um script, você poderá usar a `#r` sintaxe para especificar um assembly. Considere o seguinte código em um projeto compilado em `MyAssembly.dll` :

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

Um compilado, você pode fazer referência a ele em um arquivo chamado da `Script.fsx` seguinte maneira:

```fsharp
#r "path/to/MyAssembly.dll"

printfn $"{MyAssembly.myFunction 10 40}"
```

A saída é da seguinte maneira:

```console
dotnet fsi Script.fsx
90
```

Você pode especificar quantas referências de assembly desejar em um script.

## <a name="loading-other-scripts"></a>Carregando outros scripts

Ao criar scripts, muitas vezes pode ser útil usar scripts diferentes para tarefas diferentes. Às vezes, talvez você queira reutilizar o código de um script em outro. Em vez de copiar e colar seu conteúdo em seu arquivo, você pode simplesmente carregá-lo e avaliá-lo com o `#load` .

Considere o seguinte `Script1.fsx` :

```fsharp
let square x = x * x
```

E o arquivo de consumo, `Script2.fsx` :

```fsharp
#load "Script1.fsx"
open Script1

printfn $"%d{square 12}"
```

Observe que a `open Script1` declaração é necessária. Isso ocorre porque as construções em um script F # são compiladas em um módulo de nível superior que é o nome do arquivo de script em que se encontra.

Você pode avaliar da `Script2.fsx` seguinte forma:

```console
dotnet fsi Script2.fsx
144
```

Você pode especificar quantas `#load` diretivas desejar em um script.

## <a name="using-the-fsi-object-in-f-code"></a>Usando o `fsi` objeto no código F #

Os scripts F # têm acesso a um `fsi` objeto personalizado que representa a sessão de F# interativo. Ele permite que você personalize coisas como formatação de saída. Também é como você pode acessar argumentos de linha de comando.

O exemplo a seguir mostra como obter e usar argumentos de linha de comando:

```fsharp
let args = fsi.CommandLineArgs

for arg in args do
    printfn $"{arg}"
```

Quando avaliado, ele imprime todos os argumentos. O primeiro argumento é sempre o nome do script que é avaliado:

```dotnet
dotnet fsi Script1.fsx hello world from fsi
Script1.fsx
hello
world
from
fsi
```

Você também pode usar `System.Environment.GetCommandLineArgs()` o para acessar os mesmos argumentos.

## <a name="f-interactive-directive-reference"></a>Referência de diretiva de F# Interativo

As `#r` `#load` diretivas e vistas anteriormente só estão disponíveis no F# interativo. Há várias diretivas disponíveis somente no F# Interativo:

|Diretiva|Descrição|
|---------|-----------|
|`#r "nuget:..."`|Referencia um pacote do NuGet|
|`#r "assembly-name.dll"`|Faz referência a um assembly no disco|
|`#load "file-name.fsx"`|Lê um arquivo de origem, compila e o executa.|
|`#help`|Exibe informações sobre as diretivas disponíveis.|
|`#I`|Especifica um caminho de pesquisa de assembly entre aspas.|
|`#quit`|Finaliza uma sessão do F# interativo.|
|`#time "on"` ou `#time "off"`|Por si só, `#time` alterna se as informações de desempenho devem ser exibidas. Quando é `"on"` , F# interativo mede as informações em tempo real, tempo de CPU e coleta de lixo para cada seção de código que é interpretada e executada.|

Quando você especificar arquivos ou caminhos em F# interativo, uma sequência literal é esperada. Portanto, arquivos e caminhos devem estar entre aspas e os caracteres de escape comuns se aplicam. Você pode usar o `@` caractere para fazer com que F# interativo interprete uma cadeia de caracteres que contém um caminho como uma cadeia de caracteres textual. Isso faz com que o F# interativo ignore quaisquer caracteres de escape.

## <a name="interactive-and-compiled-preprocessor-directives"></a>Diretivas de pré-processador interativo e compilado

Quando você compila o código no F# Interativo, quer você esteja executando interativamente ou executando um script, o símbolo **interativo** é definido. Quando você compila o código no compilador, o símbolo **compilado** é definido. Portanto, se o código precisar ser diferente em modos compilados e interativos, você poderá usar essas diretivas de pré-processador para compilação condicional para determinar qual delas usar. Por exemplo:

```fsharp
#if INTERACTIVE
// Some code that executes only in FSI
// ...
#endif
```

## <a name="using-f-interactive-in-visual-studio"></a>Usando F# Interativo no Visual Studio

Para executar o F# Interativo por meio do Visual Studio, você pode clicar no botão de barra de ferramentas apropriado rotulado como **F# Interativo** ou usar as teclas **Ctrl+Alt+F**. Isso abrirá a janela interativa, uma janela da ferramenta que executa uma sessão de F# interativo. Você também pode selecionar um código que deseja executar na janela interativa e pressionar a combinação de teclas **ALT + Enter**. O F# interativo é iniciado em uma janela da ferramenta rotulada como **F# Interativo**. Quando você usar essa combinação de teclas, certifique-se de que a janela do editor tenha o foco.

Se você estiver usando o console ou o Visual Studio, será exibido um prompt de comando e o interpretador aguardará a entrada. Você pode inserir o código como faria em um arquivo de código. Para compilar e executar o código, insira dois sinais de ponto e vírgula (**;;**) para terminar uma linha ou várias linhas de entrada.

O F# interativo tenta compilar o código e, se tiver êxito, executará o código e imprimirá a assinatura dos tipos e valores que ele compilou. Se ocorrerem erros, o interpretador imprime as mensagens de erro.

O código digitado na mesma sessão tem acesso a quaisquer construções inseridas anteriormente, para poder criar os programas. Um buffer extensivo na janela da ferramenta permite que você copie o código para um arquivo, se necessário.

Quando executado no Visual Studio, o F# interativo é executado independentemente do seu projeto, então, por exemplo, não é possível usar construções definidas em seu projeto em F# interativo, a menos que você copie o código para a função na janela interativa.

Você pode controlar a F# Interativo argumentos de linha de comando (opções) ajustando as configurações. No menu **Ferramentas**, selecione **Opções...** e expanda **Ferramentas do F#**. As duas configurações que podem ser alteradas são as opções do F# interativo e a configuração do **F# Interativo de 64 bits**, que é relevante apenas se você estiver executando o F# interativo em uma máquina de 64 bits. Essa configuração determina se você deseja executar a versão dedicada de 64 bits do **fsi.exe** ou **fsianycpu.exe**, que usa a arquitetura do computador para determinar se deve ser executado como um processo de 32 ou 64 bits.

## <a name="related-articles"></a>Artigos relacionados

|Título|Descrição|
|-----|-----------|
|[Opções do F# Interativo](../../language-reference/fsharp-interactive-options.md)|Descreve a sintaxe de linha de comando e as opções para o F# Interativo, fsi.exe.|
