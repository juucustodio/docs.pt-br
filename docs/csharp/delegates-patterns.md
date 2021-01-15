---
title: Padrões Comuns para Delegados
description: Saiba mais sobre os padrões comuns para usar delegados em seu código para evitar acoplamento forte entre os componentes.
ms.date: 06/20/2016
ms.assetid: 0ff8fdfd-6a11-4327-b061-0f2526f35b43
ms.openlocfilehash: 22ab88e5b139381e3a8921baa20df035f1405146
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223690"
---
# <a name="common-patterns-for-delegates"></a>Padrões Comuns para Delegados

[Anterior](delegates-strongly-typed.md)

Os delegados fornecem um mecanismo que permite designs de software que envolvem acoplamento mínimo entre os componentes.

Um exemplo excelente desse tipo de design é o LINQ. O padrão de expressão de consulta LINQ se baseia em delegados para todos os seus recursos. Considere este exemplo simples:

```csharp
var smallNumbers = numbers.Where(n => n < 10);
```

Isso filtra a sequência de números para somente aqueles com valor menor que 10.
O método `Where` usa um delegado que determina quais elementos de uma sequência são passados no filtro. Quando cria uma consulta LINQ, você fornece a implementação do delegado para essa finalidade específica.

O protótipo para o método Where é:

```csharp
public static IEnumerable<TSource> Where<TSource> (this IEnumerable<TSource> source, Func<TSource, bool> predicate);
```

Este exemplo é repetido com todos os métodos que fazem parte do LINQ. Todos eles contam com delegados para o código que gerencia a consulta específica. Trata-se de um padrão de design de API muito eficiente para se aprender e entender.

Este exemplo simples ilustra como delegados requerem muito pouco acoplamento entre componentes. Você não precisa criar uma classe que deriva de uma classe base específica. Você não precisa implementar uma interface específica.
O único requisito é fornecer a implementação de um método que é fundamental para a tarefa em questão.

## <a name="building-your-own-components-with-delegates"></a>Criando seus próprios componentes com delegados

Vamos trabalhar naquele exemplo criando um componente usando um design que se baseia em delegados.

Vamos definir um componente que poderia ser usado para mensagens de log em um sistema grande. Os componentes da biblioteca poderiam ser usados em muitos ambientes diferentes, em várias plataformas diferentes. Há muitos recursos comuns no componente que gerencia os logs. Ele precisará aceitar mensagens de qualquer componente do sistema. Essas mensagens terão prioridades diferentes, que o componente de núcleo pode gerenciar. As mensagens devem ter carimbos de data/hora em sua forma final arquivada. Para cenários mais avançados, é possível filtrar mensagens pelo componente de origem.

Há um aspecto do recurso que é alterado com frequência: onde as mensagens são gravadas. Em alguns ambientes, elas podem ser gravadas no console de erro. Em outros, em um arquivo. Outras possibilidades incluem o armazenamento em banco de dados, logs de eventos do sistema operacional ou outro armazenamento de documentos.

Também há combinações de saídas que podem ser usadas em cenários diferentes. Talvez você queira gravar mensagens no console e em um arquivo.

Um design baseado em delegados fornece muita flexibilidade e facilitam o suporte a mecanismos de armazenamento que podem ser adicionados no futuro.

Nesse design, o componente de log primário pode ser uma classe não virtual, até mesmo lacrada. Você pode conectar qualquer conjunto de delegados para gravar as mensagens em diferentes mídias de armazenamento. O suporte interno para delegados multicast facilita o suporte a cenários em que as mensagens devem ser gravadas em vários locais (um arquivo e um console).

## <a name="a-first-implementation"></a>Uma primeira implementação

Vamos começar pequeno: a implementação inicial aceitará novas mensagens e as gravará usando qualquer delegado anexo. Você pode começar com um delegado que grava mensagens no console.

[!code-csharp[LoggerImplementation](../../samples/snippets/csharp/delegates-and-events/Logger.cs#FirstImplementation "A first Logger implementation.")]

A classe estática acima é a coisa mais simples que pode funcionar. Precisamos escrever a única implementação do método que grava mensagens no console:

[!code-csharp[LogToConsole](../../samples/snippets/csharp/delegates-and-events/LoggingMethods.cs#LogToConsole "A Console logger.")]

Por fim, você precisa conectar o delegado anexando-o ao delegado WriteMessage declarado no agente:

[!code-csharp[ConnectDelegate](../../samples/snippets/csharp/delegates-and-events/Program.cs#ConnectDelegate "Connect to the delegate")]

## <a name="practices"></a>Práticas

Até agora, nossa amostra é bastante simples, mas ainda demonstra algumas das diretrizes importantes para designs que envolvem delegados.

Usar os tipos de delegados definidos no Core Framework torna mais fácil para os usuários trabalhem com os delegados. Você não precisa definir novos tipos e os desenvolvedores que usam sua biblioteca não precisam aprender novos tipos de delegados especializadas.

As interfaces usadas são tão mínimas e flexíveis quanto possível: para criar um novo agente de saída, você precisa criar um método. O método pode ser um método estático ou um método de instância. Ele pode ter qualquer acesso.

## <a name="formatting-output"></a>Formatando a saída

Vamos fazer esta primeira versão um pouco mais robusta e, então, começar a criar outros mecanismos de registro em log.

Em seguida, vamos adicionar alguns argumentos para o método `LogMessage()` para que sua classe de log crie mensagens mais estruturadas:

[!code-csharp[Severity](../../samples/snippets/csharp/delegates-and-events/Logger.cs#Severity "Define severities")]
[!code-csharp[NextLogger](../../samples/snippets/csharp/delegates-and-events/Logger.cs#LoggerTwo "Refine the Logger")]

Em seguida, vamos usar aquele argumento `Severity` para filtrar as mensagens que são enviadas para o log de saída.

[!code-csharp[FinalLogger](../../samples/snippets/csharp/delegates-and-events/Logger.cs#LoggerFinal "Finish the Logger")]

## <a name="practices"></a>Práticas

Você adicionou novos recursos à infraestrutura de registro em log. Como somente o componente do agente está acoplado de forma muito flexível a qualquer mecanismo de saída, esses novos recursos podem ser adicionados sem afetar o código que implementa o delegado do agente.

Conforme prosseguir com sua criação, você verá mais exemplos de como esse acoplamento flexível permite maior versatilidade para atualizar partes do site sem alterar outros locais. De fato, em um aplicativo maior, as classes de saída do agente podem estar em um assembly diferente e nem mesmo precisar ser recriadas.

## <a name="building-a-second-output-engine"></a>Criando um segundo mecanismo de saída

O componente de Log estará indo bem. Vamos adicionar mais um mecanismo de saída que registra as mensagens em um arquivo. Esse será um mecanismo de saída de um pouco mais envolvido. Ele será uma classe que encapsula as operações de arquivo e garante que o arquivo sempre seja fechado após cada gravação. Isso garante que todos os dados sejam liberados no disco após cada mensagem ser gerada.

Este é um agente baseado em arquivo:

[!code-csharp[FileLogger](../../samples/snippets/csharp/delegates-and-events/FileLogger.cs#FileLogger "Log to files")]

Após ter criado essa classe, você pode instanciá-la e ela anexa o método LogMessage ao componente do agente:

[!code-csharp[FileLogger](../../samples/snippets/csharp/delegates-and-events/Program.cs#FileLogger "Log to files")]

Os dois não são mutuamente exclusivos. Você pode anexar os dois métodos de log e gerar mensagens para o console e um arquivo:

```csharp
var fileOutput = new FileLogger("log.txt");
Logger.WriteMessage += LoggingMethods.LogToConsole; // LoggingMethods is the static class we utilized earlier
```

Posteriormente, mesmo no mesmo aplicativo, você pode remover um dos delegados sem problemas para o sistema:

```csharp
Logger.WriteMessage -= LoggingMethods.LogToConsole;
```

## <a name="practices"></a>Práticas

Agora, você adicionou um segundo manipulador de saída para o subsistema de registro em log.
Este precisa de um pouco mais infraestrutura para dar suporte ao sistema de arquivos corretamente. O delegado um método de instância. Ele também é um método particular.
Não é necessário ter mais acessibilidade porque a infraestrutura de delegados pode conectar os delegados.

Em segundo lugar, o design baseado em delegados permite vários métodos de saída sem nenhum código extra. Não é necessário criar nenhuma infraestrutura adicional para dar suporte a vários métodos de saída. Eles simplesmente se tornam outro método na lista de invocação.

Dedique atenção especial ao código no método de saída do registro em log de arquivos. Ele é codificado para garantir que não gere nenhuma exceção. Embora isso nem sempre seja estritamente necessário, geralmente é uma boa prática. Se um dos métodos de delegado gerar uma exceção, os delegados restantes que fazem parte da invocação não serão invocados.

Como uma última observação, o agente de arquivos deve gerenciar seus recursos abrindo e fechando o arquivo em cada mensagem de log. Você pode optar por manter o arquivo aberto e implementar IDisposable para fechar o arquivo quando terminar.
Cada método tem suas vantagens e desvantagens. Ambos criam um pouco mais de acoplamento entre as classes.

Nenhum código na classe de agente precisaria ser atualizado para dar suporte a um dos cenários.

## <a name="handling-null-delegates"></a>Tratando delegados nulos

Por fim, vamos atualizar o método LogMessage para que ele seja robusto para os casos em que nenhum mecanismo de saída está selecionado. A implementação atual gerará um `NullReferenceException` quando o delegado `WriteMessage` não tiver uma lista de invocação anexada.
Talvez você prefira um design que continua silenciosamente quando não nenhum método tiver sido anexado. Isso é fácil usando o operador condicional nulo, combinado com o método `Delegate.Invoke()`:

```csharp
public static void LogMessage(string msg)
{
    WriteMessage?.Invoke(msg);
}
```

O operador condicional nulo (`?.`) entra em curto-circuito quando o operando esquerdo (`WriteMessage` nesse caso) for nulo, o que significa que não é feita nenhuma tentativa de registrar uma mensagem.

Você não encontrará o método `Invoke()` listado na documentação de `System.Delegate` ou `System.MulticastDelegate`. O compilador gera um método `Invoke` fortemente tipado para qualquer tipo de delegado declarado. Neste exemplo, isso significa que `Invoke` usa um único argumento `string` e tem um tipo de retorno nulo.

## <a name="summary-of-practices"></a>Resumo das práticas

Você já viu o início de um componente de log que poderia ser expandido com outros gravadores e outros recursos. Com o uso de delegados no design, esses diferentes componentes ficam acoplados de forma bastante flexível. Isso traz vários benefícios. É muito fácil criar novos mecanismos de saída e anexá-los ao sistema. Esses outros mecanismos precisam de apenas um método: o método que grava a mensagem de log. Trata-se de um design que é muito flexível quando novos recursos são adicionados. O contrato necessário para qualquer gravador é implementar um método. Esse método pode ser estático ou de instância. Ele pode ser ter acesso público, privado ou qualquer outro acesso válido.

A classe de agente pode fazer vários aprimoramentos ou alterações sem introduzir alterações interruptivas. Assim como qualquer classe, você não pode modificar a API pública sem o risco de fazer alterações interruptivas. Mas, como o acoplamento entre o agente e qualquer mecanismo de saída ocorre somente por meio do delegado, nenhum outro tipo (como interfaces ou classes base) é envolvido. O acoplamento é o menor possível.

[Próximo](events-overview.md)
