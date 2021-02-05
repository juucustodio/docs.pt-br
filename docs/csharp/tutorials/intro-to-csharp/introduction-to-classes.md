---
title: Tutorial Classes e objetos – introdução ao C#
description: Crie seu primeiro programa em C# e explore os conceitos de orientado a objeto
ms.date: 10/11/2017
ms.custom: mvc
ms.openlocfilehash: a48e5790d2872ca3074bd7ce06c23412086b00f3
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585358"
---
# <a name="explore-object-oriented-programming-with-classes-and-objects"></a>Explorar programação orientada a objeto com classes e objetos

Neste tutorial, você criará um aplicativo de console e verá os recursos básicos orientados a objeto que fazem parte da linguagem C#.

## <a name="prerequisites"></a>Pré-requisitos

O tutorial espera que você tenha uma máquina configurada para desenvolvimento local. No Windows, Linux ou macOS, você pode usar a CLI do .NET para criar, compilar e executar aplicativos. No Windows, você pode usar o Visual Studio 2019. Para obter instruções de instalação, consulte [configurar seu ambiente local](local-environment.md).

## <a name="create-your-application"></a>Criar o aplicativo

Usando uma janela de terminal, crie um diretório chamado *classes*. Você compilará o aplicativo nesse diretório. Altere para esse diretório e digite `dotnet new console` na janela do console. Esse comando cria o aplicativo. Abra *Program.cs*. Ele deverá ser parecido com:

```csharp
using System;

namespace classes
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

Neste tutorial, você criará novos tipos que representam uma conta bancária. Normalmente, os desenvolvedores definem cada classe em um arquivo de texto diferente. Isso facilita o gerenciamento à medida que o tamanho do programa aumenta. Crie um novo arquivo chamado *BankAccount.cs* no diretório *classes*.

Esse arquivo conterá a definição de uma ***conta bancária** _. A programação orientada a objeto organiza o código criando tipos na forma de _ *_classes_* *. Essas classes contêm o código que representa uma entidade específica. A classe `BankAccount` representa uma conta bancária. O código implementa operações específicas por meio de métodos e propriedades. Neste tutorial, a conta bancária dá suporte a este comportamento:

1. Ela tem um número com 10 dígitos que identifica exclusivamente a conta bancária.
1. Ela tem uma cadeia de caracteres que armazena o nome ou os nomes dos proprietários.
1. O saldo pode ser recuperado.
1. Ela aceita depósitos.
1. Ele aceita saques.
1. O saldo inicial deve ser positivo.
1. Os saques não podem resultar em um saldo negativo.

## <a name="define-the-bank-account-type"></a>Definir o tipo de conta bancária

Você pode começar criando as noções básicas de uma classe que define esse comportamento. Crie um novo arquivo usando o comando **file: New** . Nomeie-o como *BankAccount.cs*. Adicione o seguinte código ao arquivo *BankAccount.cs* :

```csharp
using System;

namespace classes
{
    public class BankAccount
    {
        public string Number { get; }
        public string Owner { get; set; }
        public decimal Balance { get; }

        public void MakeDeposit(decimal amount, DateTime date, string note)
        {
        }

        public void MakeWithdrawal(decimal amount, DateTime date, string note)
        {
        }
    }
}
```

Antes de continuar, vamos dar uma olhada no que você compilou.  A declaração `namespace` fornece uma maneira de organizar logicamente seu código. Este tutorial é relativamente pequeno, portanto, você colocará todo o código em um namespace.

`public class BankAccount` define a classe ou o tipo que você está criando. Tudo dentro do `{` e `}` que segue a declaração de classe define o estado e o comportamento da classe. Há cinco ***Membros** _ da `BankAccount` classe. As três primeiras são _*_Propriedades_*_. Propriedades são elementos de dados que podem ter um código que impõe a validação ou outras regras. Os dois últimos são _ *_métodos_* *. Os métodos são blocos de código que executam uma única função. A leitura dos nomes de cada um dos membros deve fornecer informações suficientes para você, ou outro desenvolvedor, entender o que a classe faz.

## <a name="open-a-new-account"></a>Abrir uma nova conta

O primeiro recurso a ser implementado serve para abrir uma conta bancária. Quando um cliente abre uma conta, ele deve fornecer um saldo inicial e informações sobre o proprietário, ou proprietários, dessa conta.

A criação de um novo objeto do `BankAccount` tipo significa definir um **Construtor*** _ que atribui esses valores. Um _ *_Construtor_** é um membro que tem o mesmo nome que a classe. Ele é usado para inicializar objetos desse tipo de classe. Adicione o seguinte construtor ao `BankAccount` tipo. Coloque o seguinte código acima da declaração de `MakeDeposit` :

```csharp
public BankAccount(string name, decimal initialBalance)
{
    this.Owner = name;
    this.Balance = initialBalance;
}
```

Os construtores são chamados quando você cria um objeto usando [`new`](../../language-reference/operators/new-operator.md) . Substitua a linha `Console.WriteLine("Hello World!");` em *Program.cs* pelo código a seguir (substitua `<name>` pelo seu nome):

```csharp
var account = new BankAccount("<name>", 1000);
Console.WriteLine($"Account {account.Number} was created for {account.Owner} with {account.Balance} initial balance.");
```

Vamos executar o que você criou até agora. Se você estiver usando o Visual Studio, selecione **Iniciar sem depuração** no menu **executar** . Se você estiver usando uma linha de comando, digite `dotnet run` o diretório em que você criou o projeto.

Você notou que o número da conta está em branco? É hora de corrigir isso. O número da conta deve ser atribuído na construção do objeto. Mas não é responsabilidade do chamador criá-lo. O código da classe `BankAccount` deve saber como atribuir novos números de conta.  Uma maneira simples de fazer isso é começar com um número de 10 dígitos. Incremente-o à medida que novas contas são criadas. Por fim, armazene o número da conta atual quando um objeto for construído.

Adicione uma declaração de membro à `BankAccount` classe. Coloque a seguinte linha de código após a chave de abertura `{` no início da `BankAccount` classe:

```csharp
private static int accountNumberSeed = 1234567890;
```

Este é um membro de dados. Ele é `private`, o que significa que ele só pode ser acessado pelo código dentro da classe `BankAccount`. É uma maneira de separar as responsabilidades públicas (como ter um número de conta) da implementação privada (como os números de conta são gerados). Ele também é `static`, o que significa que é compartilhado por todos os objetos `BankAccount`. O valor de uma variável não estática é exclusivo para cada instância do objeto `BankAccount`. Adicione as duas linhas a seguir ao construtor para atribuir o número da conta. Coloque-os após a linha que diz `this.Balance = initialBalance` :

```csharp
this.Number = accountNumberSeed.ToString();
accountNumberSeed++;
```

Digite `dotnet run` para ver os resultados.

## <a name="create-deposits-and-withdrawals"></a>Criar depósitos e saques

A classe da conta bancária precisa aceitar depósitos e saques para funcionar corretamente. Vamos implementar depósitos e saques criando um diário de todas as transações da conta. Isso apresenta algumas vantagens em comparação à simples atualização do saldo em cada transação. O histórico pode ser usado para auditar todas as transações e gerenciar os saldos diários. Ao calcular o saldo do histórico de todas as transações, quando for necessário, todos os erros corrigidos em uma única transação serão refletidos corretamente no saldo no próximo cálculo.

Vamos começar criando um novo tipo para representar uma transação. É um tipo simples que não tem qualquer responsabilidade. Ele precisa de algumas propriedades. Crie um novo arquivo chamado *Transaction.cs*. Adicione os seguintes códigos a ela:

:::code language="csharp" source="./snippets/introduction-to-classes/Transaction.cs":::

Agora, vamos adicionar um <xref:System.Collections.Generic.List%601> de `Transaction` objetos à classe `BankAccount`. Adicione a seguinte declaração após o Construtor em seu arquivo *BankAccount.cs* :

:::code language="csharp" source="./snippets/introduction-to-classes/BankAccount.cs" id="TransactionDeclaration":::

A classe <xref:System.Collections.Generic.List%601> exige que você importe um namespace diferente. Adicione o seguinte no início de *BankAccount.cs*:

```csharp
using System.Collections.Generic;
```

Agora, vamos calcular corretamente o `Balance` . O saldo atual pode ser encontrado somando-se os valores de todas as transações. Como o código é atualmente, você só pode obter o saldo inicial da conta, portanto, você precisará atualizar a `Balance` propriedade. Substitua a linha `public decimal Balance { get; }` em *BankAccount.cs* pelo seguinte código:

:::code language="csharp" source="./snippets/introduction-to-classes/BankAccount.cs" id="BalanceComputation":::

Este exemplo mostra um aspecto importante das ***propriedades***. Agora, você está calculando o saldo quando outro programador solicita o valor. Seu cálculo enumera todas as transações e fornece a soma como o saldo atual.

Depois, implemente os métodos `MakeDeposit` e `MakeWithdrawal`. Esses métodos aplicarão as duas últimas regras: que o saldo inicial deve ser positivo, e que qualquer saque não pode criar um saldo negativo.

Isso introduz o conceito de ***exceções***. A forma padrão de indicar que um método não pode concluir seu trabalho com êxito é lançar uma exceção. O tipo de exceção e a mensagem associada a ele descrevem o erro. Aqui, o método `MakeDeposit` lançará uma exceção se o valor do depósito for negativo. O `MakeWithdrawal` método lançará uma exceção se a quantidade de retirada for negativa ou se a aplicação da retirada resultar em um saldo negativo. Adicione o seguinte código após a declaração da `allTransactions` lista:

:::code language="csharp" source="./snippets/introduction-to-classes/BankAccount.cs" id="DepositAndWithdrawal":::

A [`throw`](../../language-reference/keywords/throw.md) instrução **gera** uma exceção. A execução do bloco atual é encerrada e o controle transferido para o bloco `catch` da primeira correspondência encontrado na pilha de chamadas. Você adicionará um bloco `catch` para testar esse código um pouco mais tarde.

O construtor deve receber uma alteração para que adicione uma transação inicial, em vez de atualizar o saldo diretamente. Como você já escreveu o método `MakeDeposit`, chame-o de seu construtor. O construtor concluído deve ter esta aparência:

:::code language="csharp" source="./snippets/introduction-to-classes/BankAccount.cs" id="Constructor":::

<xref:System.DateTime.Now?displayProperty=nameWithType> é uma propriedade que retorna a data e a hora atuais. Teste isso adicionando alguns depósitos e retirados em seu `Main` método, seguindo o código que cria um novo `BankAccount` :

```csharp
account.MakeWithdrawal(500, DateTime.Now, "Rent payment");
Console.WriteLine(account.Balance);
account.MakeDeposit(100, DateTime.Now, "Friend paid me back");
Console.WriteLine(account.Balance);
```

Em seguida, teste se você está capturando condições de erro tentando criar uma conta com um saldo negativo. Adicione o código a seguir após o código anterior que você acabou de adicionar:

```csharp
// Test that the initial balances must be positive.
try
{
    var invalidAccount = new BankAccount("invalid", -55);
}
catch (ArgumentOutOfRangeException e)
{
    Console.WriteLine("Exception caught creating account with negative balance");
    Console.WriteLine(e.ToString());
}
```

Você usa as [ `try` `catch` instruções e](../../language-reference/keywords/try-catch.md) para marcar um bloco de código que pode gerar exceções e capturar os erros que você espera. Você pode usar a mesma técnica para testar o código que gera uma exceção para um saldo negativo. Adicione o seguinte código ao final do seu `Main` método:

```csharp
// Test for a negative balance.
try
{
    account.MakeWithdrawal(750, DateTime.Now, "Attempt to overdraw");
}
catch (InvalidOperationException e)
{
    Console.WriteLine("Exception caught trying to overdraw");
    Console.WriteLine(e.ToString());
}
```

Salve o arquivo e digite `dotnet run` para testá-lo.

## <a name="challenge---log-all-transactions"></a>Desafio – registrar em log todas as transações

Para concluir este tutorial, escreva o método `GetAccountHistory` que cria um `string` para o histórico de transações. Adicione esse método ao tipo `BankAccount`:

:::code language="csharp" source="./snippets/introduction-to-classes/BankAccount.cs" id="History":::

Isso usa a classe <xref:System.Text.StringBuilder> para formatar uma cadeia de caracteres que contém uma linha para cada transação. Você viu o código de formatação da cadeia de caracteres anteriormente nesses tutoriais. Um caractere novo é `\t`. Ele insere uma guia para formatar a saída.

Adicione esta linha para testá-la no *Program.cs*:

```csharp
Console.WriteLine(account.GetAccountHistory());
```

Execute o programa para ver os resultados.

## <a name="next-steps"></a>Próximas etapas

Se você ficou preso, pode ver a origem deste tutorial [em nosso repositório GitHub](https://github.com/dotnet/docs/tree/master/docs/csharp/tutorials/intro-to-csharp/snippets/introduction-to-classes).

Você pode continuar com o tutorial de [programação orientada a objeto](object-oriented-programming.md) .

Você pode saber mais sobre esses conceitos nestes artigos:

- [Instrução if e else](../../language-reference/keywords/if-else.md)
- [Instrução while](../../language-reference/keywords/while.md)
- [Instrução do](../../language-reference/keywords/do.md)
- [Instrução for](../../language-reference/keywords/for.md)
