---
title: Introdução ao F# no Visual Studio Code
description: 'Saiba como usar F # com Visual Studio Code e o pacote de plug-in Ionide.'
ms.date: 12/23/2018
ms.openlocfilehash: 11fb0d443fb7c2b3f270d45bfeaa91102ba28efd
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739796"
---
# <a name="get-started-with-f-in-visual-studio-code"></a>Introdução ao F# no Visual Studio Code

Você pode escrever F # em [Visual Studio Code](https://code.visualstudio.com) com o [plug-in Ionide](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp) para obter uma experiência excelente de plataforma cruzada, ambiente de desenvolvimento integrado leve (IDE) com IntelliSense e refatoração de código. Visite [Ionide.Io](https://ionide.io) para saber mais sobre o plug-in.

Para começar, verifique se você tem [F # e o plug-in Ionide instalado corretamente](install-fsharp.md#install-f-with-visual-studio-code).

## <a name="create-your-first-project-with-ionide"></a>Criar seu primeiro projeto com o Ionide

Para criar um novo projeto F #, abra uma linha de comando e crie um novo projeto com o CLI do .NET Core:

```dotnetcli
dotnet new console -lang "F#" -o FirstIonideProject
```

Após a conclusão, altere o diretório para o projeto e abra Visual Studio Code:

```console
cd FirstIonideProject
code .
```

Depois que o projeto for carregado no Visual Studio Code, você deverá ver o painel de Gerenciador de Soluções de F # no lado esquerdo da janela aberta. Isso significa que o Ionide carregou com êxito o projeto que você acabou de criar. Você pode escrever código no editor antes desse ponto no tempo, mas assim que isso acontecer, tudo concluiu o carregamento.

## <a name="configure-f-interactive"></a>Configurar o F # interativo

Primeiro, verifique se o script do .NET Core é o seu ambiente de script padrão:

1. Abra as configurações de Visual Studio Code (configurações de preferências de **código**  >  **Preferences**  >  **Settings**).
1. Procure o termo **script F #**.
1. Clique na caixa de seleção que diz **FSharp: usar scripts do SDK**.

Isso é necessário no momento devido a alguns comportamentos herdados em scripts baseados em .NET Framework que não funcionam com o script do .NET Core e o Ionide está se empenhando atualmente para a compatibilidade com versões anteriores. No futuro, o script do .NET Core se tornará o padrão.

### <a name="write-your-first-script"></a>Escrever seu primeiro script

Depois de configurar Visual Studio Code para usar o script do .NET Core, navegue até o modo de exibição do Explorer em Visual Studio Code e crie um novo arquivo. Nomeie-o como *MyFirstScript. fsx*.

Agora, adicione o seguinte código a ele:

[!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx)]

Essa função converte uma palavra em uma forma de [Pig Latin](https://en.wikipedia.org/wiki/Pig_Latin). A próxima etapa é avaliá-lo usando o F# Interativo (FSI).

Realce a função inteira (deve ter 11 linhas). Depois de realçar, mantenha pressionada a tecla **ALT** e pressione **Enter**. Você notará uma janela de terminal exibida na parte inferior da tela e ela deverá ser semelhante a esta:

![Exemplo de saída de F# Interativo com Ionide](./media/getting-started-vscode/vscode-fsi.png)

Isso fazia três coisas:

1. Ele iniciou o processo FSI.
2. Ele enviou o código realçado sobre o processo FSI.
3. O processo do FSI avaliou o código que você enviou.

Como o que você enviou foi uma [função](../language-reference/functions/index.md), agora você pode chamar essa função com o FSI! Na janela interativa, digite o seguinte:

```fsharp
toPigLatin "banana";;
```

Você deverá ver o resultado a seguir:

```fsharp
val it : string = "ananabay"
```

Agora, vamos tentar com uma vogal como a primeira letra. Insira o seguinte:

```fsharp
toPigLatin "apple";;
```

Você deverá ver o resultado a seguir:

```fsharp
val it : string = "appleyay"
```

A função parece estar funcionando conforme o esperado. Parabéns, você acabou de escrever sua primeira função F # em Visual Studio Code e a avaliou com o FSI!

> [!NOTE]
> Como você deve ter notado, as linhas no FSI são encerradas com `;;` . Isso ocorre porque o FSI permite que você insira várias linhas. O `;;` no final permite que o FSI saiba quando o código é concluído.

## <a name="explaining-the-code"></a>Explicando o código

Se você não tiver certeza sobre o que o código está realmente fazendo, aqui está um passo a passo.

Como você pode ver, `toPigLatin` é uma função que usa uma palavra como sua entrada e a converte em uma Pig-Latin representação dessa palavra. As regras para isso são as seguintes:

Se o primeiro caractere em uma palavra começar com uma vogal, adicione "Sim" ao final da palavra. Se não começar com uma vogal, mova o primeiro caractere para o final da palavra e adicione "o".

Você pode ter notado o seguinte no FSI:

```fsharp
val toPigLatin : word:string -> string
```

Isso declara que `toPigLatin` é uma função que usa `string` como entrada (chamada `word` ) e retorna outra `string` . Isso é conhecido como a [assinatura de tipo da função](https://fsharpforfunandprofit.com/posts/function-signatures/), uma parte fundamental do F # que é a chave para entender o código f #. Você também observará isso se passar o mouse sobre a função em Visual Studio Code.

No corpo da função, você observará duas partes distintas:

1. Uma função interna, chamada `isVowel` , que determina se um determinado caractere ( `c` ) é uma vogal verificando se ele corresponde a um dos padrões fornecidos por meio de [correspondência de padrões](../language-reference/pattern-matching.md):

   [!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L2-L6)]

2. Uma [`if..then..else`](../language-reference/conditional-expressions-if-then-else.md) expressão que verifica se o primeiro caractere é uma vogal e constrói um valor de retorno dos caracteres de entrada com base em se o primeiro caractere era uma vogal ou não:

   [!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L8-L11)]

O fluxo de `toPigLatin` é assim:

Verifique se o primeiro caractere da palavra de entrada é uma vogal. Se for, anexe "Sim" ao final da palavra. Caso contrário, mova esse primeiro caractere para o final da palavra e adicione "

Há uma coisa final a ser observada sobre isso: em F #, não há nenhuma instrução explícita para retornar da função. Isso ocorre porque F # é baseado em expressão e a última expressão avaliada no corpo de uma função determina o valor de retorno dessa função. Como `if..then..else` o próprio é uma expressão, a avaliação do corpo do `then` bloco ou o corpo do `else` bloco determina o valor retornado pela `toPigLatin` função.

## <a name="turn-the-console-app-into-a-pig-latin-generator"></a>Transforme o aplicativo de console em um gerador de Pig Latin

As seções anteriores neste artigo demonstraram uma primeira etapa comum na escrita do código F #: escrever uma função inicial e executá-la interativamente com o FSI. Isso é conhecido como desenvolvimento controlado por REPL, em que [repl](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) significa "Read-Evaluate-Print loop". É uma ótima maneira de experimentar a funcionalidade até que você tenha algo funcionando.

A próxima etapa no desenvolvimento controlado por REPL é mover o código funcional para um arquivo de implementação em F #. Em seguida, ele pode ser compilado pelo compilador F # em um assembly que pode ser executado.

Para começar, abra o arquivo *Program. FS* criado anteriormente com o CLI do .NET Core. Você observará que algum código já está lá.

Em seguida, crie um novo [`module`](../language-reference/modules.md) chamado `PigLatin` e copie a `toPigLatin` função que você criou anteriormente como tal:

[!code-fsharp[ToPigLatin](~/samples/snippets/fsharp/getting-started/pig-latin.fs#L3-L14)]

Esse módulo deve estar acima da `main` função e abaixo da `open System` declaração. A ordem das declarações é importante em F #, portanto, você precisará definir a função antes de chamá-la em um arquivo.

Agora, na `main` função, chame sua função de gerador de Pig Latin nos argumentos:

```fsharp
[<EntryPoint>]
let main argv =
    for name in argv do
        let newName = PigLatin.toPigLatin name
        printfn %"{name} in Pig Latin is: {newName}"

    0
```

Agora você pode executar o aplicativo de console na linha de comando:

```dotnetcli
dotnet run apple banana
```

E você verá que ele gera o mesmo resultado que o arquivo de script, mas desta vez como um programa em execução!

## <a name="troubleshooting-ionide"></a>Solução de problemas do Ionide

Aqui estão algumas maneiras de solucionar alguns problemas que você pode encontrar:

1. Para obter os recursos de edição de código do Ionide, os arquivos F # precisam ser salvos em disco e dentro de uma pasta que está aberta no espaço de trabalho Visual Studio Code.
1. Se você fez alterações no seu sistema ou instalou os pré-requisitos do Ionide com Visual Studio Code abrir, reinicie o Visual Studio Code.
1. Se você tiver caracteres inválidos em seus diretórios de projeto, o Ionide poderá não funcionar.  Renomeie os diretórios do projeto se esse for o caso.
1. Se nenhum dos comandos Ionide estiver funcionando, verifique suas [associações de chave de Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings#_advanced-customization) para ver se você está substituindo-os por acidente.
1. Se o Ionide for interrompido em seu computador e nenhuma das opções acima tiver corrigido o problema, tente remover o `ionide-fsharp` diretório em seu computador e reinstalar o pacote de plug-in.
1. Se um projeto não for carregado (o Gerenciador de Soluções F # mostrará isso), clique com o botão direito do mouse no projeto e clique em **Ver detalhes** para obter mais informações de diagnóstico.

Ionide é um projeto de software livre criado e mantido por membros da Comunidade do F #. Informe os problemas e fique à vontade para contribuir no [repositório GitHub ionide-vscode-FSharp](https://github.com/ionide/ionide-vscode-fsharp).

Você também pode pedir mais ajuda da comunidade de desenvolvedores do Ionide e do F # no [canal Ionide Gitter](https://gitter.im/ionide/ionide-project).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o F # e os recursos do idioma, confira o [Tour do f #](../tour.md).
