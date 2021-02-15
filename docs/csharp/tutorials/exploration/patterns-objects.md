---
title: Usar padrões em objetos – tutorial em C#
description: Este tutorial ensina técnicas para usar a correspondência de padrões em membros de classe para criar modelos melhores para comportamento de objeto
ms.date: 11/05/2020
ms.openlocfilehash: 072f6f57696504c2d691473e3a43c1cda53f227f
ms.sourcegitcommit: 6bef8abde346c59771a35f4f76bf037ff61c5ba3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2020
ms.locfileid: "94332184"
---
# <a name="use-pattern-matching-to-build-your-class-behavior-for-better-code"></a>Use a correspondência de padrões para criar seu comportamento de classe para um código melhor

Os recursos de correspondência de padrões no C# fornecem sintaxe para expressar seus algoritmos. Você pode usar essas técnicas para implementar o comportamento em suas classes. Você pode combinar o design de classe orientado a objeto com uma implementação orientada a dados para fornecer código conciso ao modelar objetos do mundo real.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
>
> - Expresse suas classes orientadas a objeto usando padrões de dados.
> - Implemente esses padrões usando os recursos de correspondência de padrões do C#.
> - Aproveite o diagnóstico do compilador para validar sua implementação.

## <a name="prerequisites"></a>Pré-requisitos

Você precisará configurar seu computador para executar o .NET 5, incluindo o compilador C# 9,0. O compilador C# 9,0 está disponível a partir do [Visual Studio 2019 versão 16,8 Preview](https://visualstudio.microsoft.com/vs/preview/) ou da [visualização do SDK do .NET 5,0](https://dotnet.microsoft.com/download/dotnet/5.0).

## <a name="build-a-simulation-of-a-canal-lock"></a>Criar uma simulação de um bloqueio canal

Neste tutorial, você criará uma classe C# que simula um [bloqueio canal](https://en.wikipedia.org/wiki/Lock_(water_navigation)). Resumidamente, um bloqueio canal é um dispositivo que gera e reduz o Boats à medida que eles viajam entre dois esticamentos de água em diferentes níveis. Um bloqueio tem duas Gates e algum mecanismo para alterar o nível de água.

Em sua operação normal, um barco entra em uma das Gates, enquanto o nível de água no bloqueio corresponde ao nível de água no lado em que o barco entra. Uma vez no bloqueio, o nível de água será alterado para corresponder ao nível de água onde o barco deixará o bloqueio. Quando o nível de água corresponde ao lado, o portão no lado de saída é aberto. As medidas de segurança garantem que um operador não possa criar uma situação perigosa no canal. O nível de água só pode ser alterado quando ambos os Gates são fechados. No máximo uma porta pode ser aberta. Para abrir um portão, o nível de água no bloqueio deve corresponder ao nível de água fora do portão que está sendo aberto.

Você pode criar uma classe C# para modelar esse comportamento. Uma `CanalLock` classe ofereceria suporte a comandos para abrir ou fechar qualquer portão. Ele teria outros comandos para aumentar ou diminuir a água. A classe também deve dar suporte a propriedades para ler o estado atual de Gates e o nível de água. Seus métodos implementam as medidas de segurança.

## <a name="define-a-class"></a>Definir um classe

Você criará um aplicativo de console para testar sua `CanalLock` classe. Crie um novo projeto de console para o .NET 5 usando o Visual Studio ou a CLI do .NET. Em seguida, adicione uma nova classe e nomeie-a `CanalLock` . Em seguida, projete sua API pública, mas deixe os métodos não implementados:

:::code language="csharp" source="snippets/pattern-objects/InterimSteps.cs" ID="APIDesign":::

O código anterior Inicializa o objeto para que ambos os Gates sejam fechados e o nível de água é baixo. Em seguida, escreva o código de teste a seguir em seu `Main` método para orientá-lo enquanto cria uma primeira implementação da classe:

:::code language="csharp" source="snippets/pattern-objects/Program.cs" ID="HappyTests":::

Em seguida, adicione uma primeira implementação de cada método na `CanalLock` classe. O código a seguir implementa os métodos da classe sem preocupação com as regras de segurança. Você adicionará testes de segurança mais tarde:

:::code language="csharp" source="snippets/pattern-objects/InterimSteps.cs" ID="FirstImplementation":::

Os testes que você escreveu até agora são aprovados. Você implementou os conceitos básicos. Agora, grave um teste para a primeira condição de falha. No final dos testes anteriores, ambos os Gates são fechados e o nível de água é definido como baixo. Adicione um teste para tentar abrir o portão superior:

:::code language="csharp" source="snippets/pattern-objects/Program.cs" ID="HighGateSafetyTest":::

Esse teste falha porque a porta é aberta. Como uma primeira implementação, você pode corrigi-lo com o código a seguir:

:::code language="csharp" source="snippets/pattern-objects/InterimSteps.cs" ID="SecondImplementation":::

Seus testes são aprovados. Mas, à medida que você adiciona mais testes, você adicionará mais `if` cláusulas e testará propriedades diferentes. Em breve, esses métodos ficarão muito complicados à medida que você adicionar mais condicionais.

## <a name="implement-the-commands-with-patterns"></a>Implementar os comandos com padrões

Uma maneira melhor é usar *padrões* para determinar se o objeto está em um estado válido para executar um comando. Você pode expressar se um comando é permitido como uma função de três variáveis: o estado da porta, o nível da água e a nova configuração:

| Nova configuração | Estado da porta | Nível de água | Resultado             |
| ----------- | ---------- | ----------- | ------------------ |
| Fechado      | Fechado     | Alta        | Fechado             |
| Fechado      | Fechado     | Baixo         | Fechado             |
| Fechado      | Aberto       | Alta        | Aberto               |
| ~~Fechadas~~  | ~~Abrir~~   | ~~Baixa~~     | ~~Fechadas~~         |
| Aberto        | Fechadas     | Alta        | Aberto               |
| Aberto        | Fechadas     | Baixo         | Fechado (erro)     |
| Aberto        | Aberto       | Alta        | Aberto               |
| ~~Abrir~~    | ~~Abrir~~   | ~~Baixa~~     | ~~Fechado (erro)~~ |

A quarta e última linhas na tabela têm texto tachado porque são inválidas. O código que você está adicionando agora deve garantir que a porta de água alta nunca seja aberta quando a água estiver baixa.  Esses Estados podem ser codificados como uma única expressão de comutador (Lembre-se de que `false` indica "closed"):

:::code language="csharp" source="snippets/pattern-objects/InterimSteps.cs" ID="ThirdImplementation":::

Experimente esta versão. Seus testes são aprovados, validando o código. A tabela completa mostra as possíveis combinações de entradas e resultados. Isso significa que você e outros desenvolvedores podem examinar rapidamente a tabela e ver que você abordou todas as entradas possíveis. Ainda mais fácil, o compilador também pode ajudar. Depois de adicionar o código anterior, você pode ver que o compilador gera um aviso: *CS8524* indica que a expressão switch não cobre todas as entradas possíveis. O motivo para esse aviso é que uma das entradas é um `enum` tipo. O compilador interpreta "todas as entradas possíveis" como todas as entradas do tipo subjacente, normalmente um `int` . Esta `switch` expressão verifica apenas os valores declarados no `enum` . Para remover o aviso, você pode adicionar um padrão de descarte catch-all para o último ARM da expressão. Essa condição gera uma exceção, porque ela indica entrada inválida:

```csharp
_  => throw new InvalidOperationException("Invalid internal state"),
```

O braço de comutador anterior deve ser o último em sua `switch` expressão, pois ele corresponde a todas as entradas. Experimente movê-lo anteriormente na ordem. Isso causa um erro do compilador *CS8510* para código inacessível em um padrão.  A estrutura natural de expressões switch permite que o compilador gere erros e avisos para possíveis erros. O compilador "rede de segurança" facilita a criação de código correto em menos iterações e a liberdade de combinar os braços de switch com caracteres curinga. O compilador emitirá erros se sua combinação resultar em braços inacessíveis que você não esperava e avisos se você remover um ARM necessário.

A primeira alteração é combinar todos os braços em que o comando é para fechar a porta; Isso é sempre permitido. Adicione o seguinte código como o primeiro ARM em sua expressão de comutador:

```csharp
(false, _, _) => false,
```

Depois de adicionar o braço de comutador anterior, você obterá quatro erros de compilador, um em cada um dos braços em que o comando é `false` . Esses braços já estão cobertos pelo ARM recém-adicionado. Você pode remover essas quatro linhas com segurança. Você pretendia esse novo braço de comutador para substituir essas condições.

Em seguida, você pode simplificar os quatro braços em que o comando é para abrir o portão. Em ambos os casos em que o nível de água é alto, o portão pode ser aberto. (Em um, ele já está aberto.) Um caso em que o nível de água está baixo gera uma exceção e o outro não deve acontecer. Deve ser seguro lançar a mesma exceção se o bloqueio de água já estiver em um estado inválido. Você pode fazer as seguintes simplificações para esses braços:

```csharp
(true, _, WaterLevel.High) => true,
(true, false, WaterLevel.Low) => throw new InvalidOperationException("Cannot open high gate when the water is low"),
_ => throw new InvalidOperationException("Invalid internal state"),
```

Execute os testes novamente e eles passam. Esta é a versão final do `SetHighGate` método:

:::code language="csharp" source="snippets/pattern-objects/CanalLock.cs" ID="FinalImplementaton":::

## <a name="implement-patterns-yourself"></a>Implementar padrões por conta própria

Agora que você já viu a técnica, preencha os `SetLowGate` métodos e por `SetWaterLevel` conta própria.  Comece adicionando o código a seguir para testar operações inválidas nesses métodos:

:::code language="csharp" source="snippets/pattern-objects/Program.cs" ID="FinalTestCode":::

Execute o aplicativo novamente. Você pode ver que os novos testes falham e o bloqueio canal entra em um estado inválido. Tente implementar os métodos restantes por conta própria. O método para definir o portão inferior deve ser semelhante ao método para definir o portão superior. O método que altera o nível de água tem verificações diferentes, mas deve seguir uma estrutura semelhante. Talvez você ache útil usar o mesmo processo para o método que define o nível de água. Comece com todas as quatro entradas: o estado de ambos os Gates, o estado atual do nível de água e o novo nível de água solicitado. A expressão switch deve começar com:

```csharp
CanalLockWaterLevel = (newLevel, CanalLockWaterLevel, LowWaterGateOpen, HighWaterGateOpen) switch
{
    // elided
};
```

Você terá 16 braços de comutação total para preencher. Em seguida, teste e simplifique.

Você fez métodos como este?

:::code language="csharp" source="snippets/pattern-objects/CanalLock.cs" ID="FinalExercise":::

Seus testes devem passar e o bloqueio canal deve funcionar com segurança.

## <a name="summary"></a>Resumo

Neste tutorial, você aprendeu a usar a correspondência de padrões para verificar o estado interno de um objeto antes de aplicar qualquer alteração a esse estado. Você pode verificar combinações de propriedades. Depois de criar tabelas para qualquer uma dessas transições, você testará seu código e, em seguida, simplificará a legibilidade e a capacidade de manutenção. Essas refatoridades iniciais podem sugerir refatoração adicional que validam o estado interno ou gerenciam outras alterações de API. Este tutorial combinou classes e objetos com uma abordagem mais orientada a dados, baseada em padrões, para implementar essas classes.
