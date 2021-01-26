---
title: Programação orientada a objeto (C#)
description: O C# fornece suporte completo para a programação orientada a objeto, incluindo abstração, encapsulamento, herança e polimorfismo.
ms.date: 09/30/2020
ms.openlocfilehash: b778b7c42bbfb1f20bdd2d83b9cb10512ea3f41b
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794846"
---
# <a name="object-oriented-programming-c"></a>Programação de Object-Oriented (C#)

O C# é uma linguagem orientada a objeto. Quatro das principais técnicas usadas na programação orientada a objeto são:

- *Abstração* significa ocultar os detalhes desnecessários do tipo consumidores.
- *Encapsulamento* significa que um grupo de propriedades, métodos e outros membros relacionados é tratado como uma única unidade ou objeto.
- *Herança* descreve a capacidade de criar novas classes com base em uma classe existente.
- *Polimorfismo* significa que você pode ter várias classes que podem ser usadas de forma intercambiável, ainda que cada classe implemente as mesmas propriedades ou métodos de maneiras diferentes.

No tutorial anterior, [introdução às classes](introduction-to-classes.md) que você viu *abstração* e *encapsulamento*. A `BankAccount` classe forneceu uma abstração para o conceito de uma conta bancária. Você poderia modificar sua implementação sem afetar nenhum código que usava a `BankAccount` classe. As `BankAccount` classes e `Transaction` fornecem encapsulamento dos componentes necessários para descrever esses conceitos no código.

Neste tutorial, você estenderá esse aplicativo para fazer uso de *herança* e *polimorfismo* para adicionar novos recursos. Você também adicionará recursos à `BankAccount` classe, aproveitando as técnicas de *abstração* e de *encapsulamento* aprendidas no tutorial anterior.

## <a name="create-different-types-of-accounts"></a>Criar diferentes tipos de contas

Depois de criar esse programa, você receberá solicitações para adicionar recursos a ele. Ele funciona muito bem na situação em que há apenas um tipo de conta bancária. Ao longo do tempo, as necessidades mudam e os tipos de conta relacionados são solicitados:

- Uma conta de conquista de interesse que acumula interesse no final de cada mês.
- Uma linha de crédito que pode ter um saldo negativo, mas quando há um saldo, há um encargo de juros a cada mês.
- Uma conta de vale-presente pré-paga que começa com um único depósito e pode ser paga. Ele pode ser recarregado uma vez no início de cada mês.

Todas essas contas diferentes são semelhantes à `BankAccount` classe definida no tutorial anterior. Você pode copiar esse código, renomear as classes e fazer modificações. Essa técnica funcionaria a curto prazo, mas seria mais trabalho ao longo do tempo. Todas as alterações seriam copiadas em todas as classes afetadas.

Em vez disso, você pode criar novos tipos de conta bancária que herdam métodos e dados da `BankAccount` classe criada no tutorial anterior. Essas novas classes podem estender a `BankAccount` classe com o comportamento específico necessário para cada tipo:

```csharp
public class InterestEarningAccount : BankAccount
{
}

public class LineOfCreditAccount : BankAccount
{
}

public class GiftCardAccount : BankAccount
{
}
```

Cada uma dessas classes *herda* o comportamento compartilhado de sua *classe base* compartilhada, a `BankAccount` classe. Escreva as implementações para uma funcionalidade nova e diferente em cada uma das *classes derivadas*.  Essas classes derivadas já têm todo o comportamento definido na `BankAccount` classe.

É uma boa prática criar cada nova classe em um arquivo de origem diferente. No [Visual Studio](https://visualstudio.com), você pode clicar com o botão direito do mouse no projeto e selecionar *Adicionar classe* para adicionar uma nova classe em um novo arquivo. Em [Visual Studio Code](https://code.visualstudio.com), selecione *arquivo* e *novo* para criar um novo arquivo de origem. Em qualquer ferramenta, nomeie o arquivo para corresponder à classe: *InterestEarningAccount.cs*, *LineOfCreditAccount.cs* e *GiftCardAccount.cs*.

Ao criar as classes conforme mostrado no exemplo anterior, você descobrirá que nenhuma de suas classes derivadas são compiladas. Um construtor é responsável por inicializar um objeto. Um construtor de classe derivada deve inicializar a classe derivada e fornecer instruções sobre como inicializar o objeto da classe base incluído na classe derivada. A inicialização apropriada normalmente ocorre sem nenhum código extra. A `BankAccount` classe declara um construtor público com a seguinte assinatura:

```csharp
public BankAccount(string name, decimal initialBalance)
```

O compilador não gera um construtor padrão quando você define um construtor por conta própria. Isso significa que cada classe derivada deve chamar explicitamente esse construtor. Você declara um construtor que pode passar argumentos para o construtor da classe base.  O código a seguir mostra o construtor para o `InterestEarningAccount` :

:::code language="csharp" source="./snippets/object-oriented-programming/InterestEarningAccount.cs" ID="DerivedConstructor":::

Os parâmetros para esse novo Construtor correspondem ao tipo de parâmetro e aos nomes do construtor da classe base. Você usa a `: base()` sintaxe para indicar uma chamada para um construtor de classe base. Algumas classes definem vários construtores, e essa sintaxe permite que você escolha qual Construtor de classe base você chama. Depois de atualizar os construtores, você pode desenvolver o código para cada uma das classes derivadas. Os requisitos para as novas classes podem ser declarados da seguinte maneira:

- Uma conta de conquista de interesse:
  - Receberá um crédito de 2% do saldo de término do mês.
- Uma linha de crédito:
  - Pode ter um saldo negativo, mas não deve ser maior em valor absoluto do que o limite de crédito.
  - Incorrerá em um encargo de juros a cada mês em que o saldo do fim do mês não é 0.
  - Incorrerá em uma taxa em cada retirada que passa pelo limite de crédito.
- Uma conta de cartão de presente:
  - Pode ser recarregado com um valor especificado uma vez por mês, no último dia do mês.

Você pode ver que todos esses três tipos de conta têm uma ação que usa locais no final de cada mês. No entanto, cada tipo de conta executa tarefas diferentes. Você usa *polimorfismo* para implementar esse código. Crie um único `virtual` método na `BankAccount` classe:

:::code language="csharp" source="./snippets/object-oriented-programming/BankAccount.cs" ID="DeclareMonthEndTransactions":::

O código anterior mostra como você usa a `virtual` palavra-chave para declarar um método na classe base para a qual uma classe derivada pode fornecer uma implementação diferente. Um `virtual` método é um método em que qualquer classe derivada pode optar por reimplementar. As classes derivadas usam a `override` palavra-chave para definir a nova implementação. Normalmente, você faz referência a isso como "substituindo a implementação da classe base". A `virtual` palavra-chave especifica que as classes derivadas podem substituir o comportamento. Você também pode declarar `abstract` métodos em que classes derivadas devem substituir o comportamento. A classe base não fornece uma implementação para um `abstract` método. Em seguida, você precisa definir a implementação para duas das novas classes que você criou. Comece com `InterestEarningAccount` :

:::code language="csharp" source="./snippets/object-oriented-programming/InterestEarningAccount.cs" ID="ApplyMonthendInterest":::

Adicione o código a seguir ao `LineOfCreditAccount` . O código nega o saldo para computar um encargo de interesse positivo que é retirado da conta:

:::code language="csharp" source="./snippets/object-oriented-programming/LineOfCreditAccount.cs" ID="ApplyMonthendInterest":::

A `GiftCardAccount` classe precisa de duas alterações para implementar sua funcionalidade de fim de mês. Primeiro, modifique o construtor para incluir um valor opcional a ser adicionado a cada mês:

:::code language="csharp" source="./snippets/object-oriented-programming/GiftCardAccount.cs" ID="GiftCardAccountConstruction":::

O construtor fornece um valor padrão para o `monthlyDeposit` valor para que os chamadores possam omitir um `0` para nenhum depósito mensal. Em seguida, substitua o `PerformMonthEndTransactions` método para adicionar o depósito mensal, se ele tiver sido definido como um valor diferente de zero no construtor:

:::code language="csharp" source="./snippets/object-oriented-programming/GiftCardAccount.cs" ID="AddMonthlyDeposit":::

A substituição aplica o conjunto de depósito mensal no construtor. Adicione o seguinte código ao `Main` método para testar essas alterações para o `GiftCardAccount` e o `InterestEarningAccount` :

:::code language="csharp" source="./snippets/object-oriented-programming/Program.cs" ID="FirstTests":::

Verifique os resultados. Agora, adicione um conjunto semelhante de código de teste para o `LineOfCreditAccount` :

```
    var lineOfCredit = new LineOfCreditAccount("line of credit", 0);
    // How much is too much to borrow?
    lineOfCredit.MakeWithdrawal(1000m, DateTime.Now, "Take out monthly advance");
    lineOfCredit.MakeDeposit(50m, DateTime.Now, "Pay back small amount");
    lineOfCredit.MakeWithdrawal(5000m, DateTime.Now, "Emergency funds for repairs");
    lineOfCredit.MakeDeposit(150m, DateTime.Now, "Partial restoration on repairs");
    lineOfCredit.PerformMonthEndTransactions();
    Console.WriteLine(lineOfCredit.GetAccountHistory());
 ```

Ao adicionar o código anterior e executar o programa, você verá algo semelhante ao seguinte erro:

```console
Unhandled exception. System.ArgumentOutOfRangeException: Amount of deposit must be positive (Parameter 'amount')
   at OOProgramming.BankAccount.MakeDeposit(Decimal amount, DateTime date, String note) in BankAccount.cs:line 42
   at OOProgramming.BankAccount..ctor(String name, Decimal initialBalance) in BankAccount.cs:line 31
   at OOProgramming.LineOfCreditAccount..ctor(String name, Decimal initialBalance) in LineOfCreditAccount.cs:line 9
   at OOProgramming.Program.Main(String[] args) in Program.cs:line 29
```

> [!NOTE]
> A saída real inclui o caminho completo para a pasta com o projeto. Os nomes das pastas foram omitidos para fins de brevidade. Além disso, dependendo do seu formato de código, os números de linha podem ser um pouco diferentes.

Esse código falha porque o `BankAccount` supõe que o saldo inicial deve ser maior que 0. Outra suposição inclusas na `BankAccount` classe é que o saldo não pode ficar negativo. Em vez disso, qualquer retirada que redesenha a conta é rejeitada. Ambas as suposições precisam ser alteradas. A linha de conta de crédito começa em 0 e geralmente terá um saldo negativo. Além disso, se um cliente emprestando muito dinheiro, ele incorrerá em uma taxa. A transação é aceita, ela apenas custa mais. A primeira regra pode ser implementada adicionando um argumento opcional ao `BankAccount` Construtor que especifica o saldo mínimo. O padrão é `0`. A segunda regra requer um mecanismo que permita que as classes derivadas modifiquem o algoritmo padrão. De certa forma, a classe base "pergunta" o tipo derivado o que deve acontecer quando há um superrascunho. O comportamento padrão é rejeitar a transação lançando uma exceção.

Vamos começar adicionando um segundo construtor que inclui um `minimumBalance` parâmetro opcional. Esse novo construtor executa todas as ações feitas pelo Construtor existente. Além disso, ele define a propriedade de saldo mínimo. Você pode copiar o corpo do Construtor existente. Mas isso significa que dois locais são alterados no futuro. Em vez disso, você pode usar o *encadeamento de Construtor* para fazer com que um Construtor Chame outro. O código a seguir mostra os dois construtores e o novo campo adicional:

 :::code language="csharp" source="./snippets/object-oriented-programming/BankAccount.cs" ID="ConstructorModifications":::

O código anterior mostra duas novas técnicas. Primeiro, o `minimumBalance` campo é marcado como `readonly` . Isso significa que o valor não pode ser alterado depois que o objeto é construído. Depois que um `BankAccount` é criado, o `minimumBalance` não pode mudar. Em segundo lugar, o construtor que usa dois parâmetros utiliza `: this(name, initialBalance, 0) { }` como sua implementação. A `: this()` expressão chama o outro construtor, aquele com três parâmetros. Essa técnica permite que você tenha uma única implementação para inicializar um objeto, embora o código do cliente possa escolher um dos muitos construtores.

Essa implementação só chamará `MakeDeposit` se o saldo inicial for maior que `0` . Isso preserva a regra que os depósitos devem ser positivos, mas permite que a conta de crédito seja aberta com um `0` saldo.

Agora que a `BankAccount` classe tem um campo somente leitura para o saldo mínimo, a alteração final é alterar o código físico `0` para `minimumBalance` no `MakeWithdrawal` método:

```csharp
if (Balance - amount < minimumBalance)
```

Depois de estender a `BankAccount` classe, você pode modificar o `LineOfCreditAccount` construtor para chamar o novo construtor base, conforme mostrado no código a seguir:

:::code language="csharp" source="./snippets/object-oriented-programming/LineOfCreditAccount.cs" ID="ConstructLineOfCredit":::

Observe que o `LineOfCreditAccount` Construtor altera o sinal do `creditLimit` parâmetro para que ele corresponda ao significado do `minimumBalance` parâmetro.

## <a name="different-overdraft-rules"></a>Regras diferentes de rascunho

O último recurso a ser adicionado permite que o `LineOfCreditAccount` encarregue uma taxa para passar pelo limite de crédito em vez de recusar a transação.

Uma técnica é definir uma função virtual na qual você implementa o comportamento necessário. A `BankAccount` classe refatora o `MakeWithdrawal` método em dois métodos. O novo método faz a ação especificada quando a retirada usa o saldo abaixo do mínimo. O `MakeWithdrawal` método existente tem o seguinte código:

```csharp
public void MakeWithdrawal(decimal amount, DateTime date, string note)
{
    if (amount <= 0)
    {
        throw new ArgumentOutOfRangeException(nameof(amount), "Amount of withdrawal must be positive");
    }
    if (Balance - amount < minimumBalance)
    {
        throw new InvalidOperationException("Not sufficient funds for this withdrawal");
    }
    var withdrawal = new Transaction(-amount, date, note);
    allTransactions.Add(withdrawal);
}
```

Substitua-o pelo seguinte código:

:::code language="csharp" source="./snippets/object-oriented-programming/BankAccount.cs" ID="RefactoredMakeWithdrawal":::

O método adicionado é `protected` , o que significa que ele pode ser chamado somente de classes derivadas. Essa declaração impede que outros clientes chamem o método. Também é `virtual` para que as classes derivadas possam alterar o comportamento. O tipo de retorno é um `Transaction?` . A `?` anotação indica que o método pode retornar `null` . Adicione a seguinte implementação no `LineOfCreditAccount` para cobrar uma taxa quando o limite de retirada for excedido:

:::code language="csharp" source="./snippets/object-oriented-programming/LineOfCreditAccount.cs" ID="AddOverdraftFee":::

A substituição retorna uma transação de taxa quando a conta é sobredesenhada. Se a retirada não ultrapassar o limite, o método retornará uma `null` transação. Isso indica que não há nenhuma taxa. Teste essas alterações adicionando o seguinte código ao seu `Main` método na `Program` classe:

:::code language="csharp" source="./snippets/object-oriented-programming/Program.cs" ID="TestLineOfCredit":::

Execute o programa e verifique os resultados.

## <a name="summary"></a>Resumo

Se você ficou preso, pode ver a origem deste tutorial [em nosso repositório GitHub](https://github.com/dotnet/docs/tree/master/docs/csharp/tutorials/intro-to-csharp/snippets/object-oriented-programming).

Este tutorial demonstrou muitas das técnicas usadas na programação de Object-Oriented:

- Você usou a *abstração* quando manteve muitos detalhes `private` em cada classe.
- Você usou o *encapsulamento* quando definiu classes para cada um dos tipos de conta diferentes. Essas classes descreveram o comportamento para esse tipo de conta.
- Você usou a *herança* quando utilizou a implementação já criada na `BankAccount` classe para salvar o código.
- Você usou *polimorfismo* quando criou `virtual` métodos que classes derivadas poderiam substituir para criar um comportamento específico para esse tipo de conta.

Parabéns, você concluiu toda a nossa introdução aos tutoriais em C#. Para saber mais, experimente mais nossos [tutoriais](../index.md).
