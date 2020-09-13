---
title: 'Atributos reservados do C#: análise estática anulável'
ms.date: 04/14/2020
description: Esses atributos são interpretados pelo compilador para fornecer uma análise estática melhor para tipos de referência anuláveis e não anuláveis.
ms.openlocfilehash: d2405162ece3df209111de65fdef54f70cc86d45
ms.sourcegitcommit: 1e8382d0ce8b5515864f8fbb178b9fd692a7503f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89656296"
---
# <a name="reserved-attributes-contribute-to-the-compilers-null-state-static-analysis"></a>Atributos reservados contribuem para a análise estática do estado nulo do compilador

Em um contexto anulável, o compilador executa a análise estática de código para determinar o estado nulo de todas as variáveis de tipo de referência:

- *NOT NULL*: a análise estática determinou que a variável foi atribuída a um valor não nulo.
- *talvez NULL*: a análise estática não pode determinar que uma variável é atribuída a um valor não nulo.

Você pode aplicar um número de atributos que fornecem informações ao compilador sobre a semântica de suas APIs. Essas informações ajudam o compilador a executar análise estática e determinar quando uma variável não é nula. Este artigo fornece uma breve descrição de cada um desses atributos e como usá-los. Todos os exemplos pressupõem C# 8,0 ou mais recente e o código está em um contexto anulável.

Vamos começar com um exemplo familiar. Imagine que sua biblioteca tenha a seguinte API para recuperar uma cadeia de caracteres de recurso:

```csharp
bool TryGetMessage(string key, out string message)
```

O exemplo anterior segue o `Try*` padrão familiar no .net. Há dois argumentos de referência para essa API: o `key` e o `message` parâmetro. Essa API tem as seguintes regras relacionadas à nulidade desses argumentos:

- Os chamadores não devem passar `null` como o argumento para `key` .
- Os chamadores podem passar uma variável cujo valor é `null` como o argumento para `message` .
- Se o `TryGetMessage` método retornar `true` , o valor de `message` não será nulo. Se o valor de retorno for `false,` o valor de `message` (e seu estado nulo) for NULL.

A regra para `key` pode ser expressa pelo tipo de variável: `key` deve ser um tipo de referência não anulável. O `message` parâmetro é mais complexo. Ele permite `null` como o argumento, mas garante que, em caso de sucesso, esse `out` argumento não seja nulo. Para esses cenários, você precisa de um vocabulário mais rico para descrever as expectativas.

Vários atributos foram adicionados para expressar informações adicionais sobre o estado nulo de variáveis. Todo o código que você escreveu antes do C# 8 introduziu tipos de referência anuláveis era *nulo alheios*. Isso significa que qualquer variável de tipo de referência pode ser nula, mas verificações nulas não são necessárias. Depois que o código estiver com *reconhecimento nulo*, essas regras serão alteradas. Os tipos de referência nunca devem ser o `null` valor, e os tipos de referência anuláveis devem ser verificados `null` antes de serem desreferenciados.

As regras para suas APIs são provavelmente mais complicadas, como vimos com o `TryGetValue` cenário de API. Muitas de suas APIs têm regras mais complexas para quando as variáveis podem ou não ser `null` . Nesses casos, você usará um dos seguintes atributos para expressar essas regras:

- [AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute): um argumento de entrada não anulável pode ser nulo.
- [DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute): um argumento de entrada anulável nunca deve ser nulo.
- [MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute): um valor de retorno não anulável pode ser nulo.
- Não [nulo](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute): um valor de retorno anulável nunca será nulo.
- [MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute): um argumento de entrada não anulável pode ser nulo quando o método retorna o `bool` valor especificado.
- [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute): um argumento de entrada anulável não será nulo quando o método retornar o `bool` valor especificado.
- [NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute): um valor de retorno não será nulo se o argumento do parâmetro especificado não for nulo.
- [DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute): um método nunca retorna. Em outras palavras, ele sempre gera uma exceção.
- [DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute): esse método nunca retorna se o `bool` parâmetro associado tiver o valor especificado.

As descrições anteriores são uma referência rápida para o que cada atributo faz. Cada seção a seguir descreve o comportamento e significa mais detalhadamente.

A adição desses atributos fornece ao compilador mais informações sobre as regras para sua API. Quando o código de chamada é compilado em um contexto habilitado para valor nulo, o compilador avisa aos chamadores quando eles violam essas regras. Esses atributos não habilitam verificações adicionais em sua implementação.

## <a name="specify-preconditions-allownull-and-disallownull"></a>Especificar pré-condições: `AllowNull` e `DisallowNull`

Considere uma propriedade de leitura/gravação que nunca retorna `null` porque ela tem um valor padrão razoável. Os chamadores passam `null` para o acessador set ao configurá-lo para esse valor padrão. Por exemplo, considere um sistema de mensagens que solicita um nome de tela em uma sala de chat. Se nenhum for fornecido, o sistema gerará um nome aleatório:

```csharp
public string ScreenName
{
   get => _screenName;
   set => _screenName = value ?? GenerateRandomScreenName();
}
private string _screenName;
```

Quando você compila o código anterior em um contexto alheios anulável, tudo está bem. Depois que você habilitar tipos de referência anuláveis, a `ScreenName` propriedade se tornará uma referência não anulável. Isso está correto para o `get` acessador: ele nunca retorna `null` . Os chamadores não precisam verificar a propriedade retornada `null` . Mas, agora, definir a propriedade para `null` gerar um aviso. Para continuar a dar suporte a esse tipo de código, adicione o <xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute?displayProperty=nameWithType> atributo à propriedade, conforme mostrado no código a seguir:

```csharp
[AllowNull]
public string ScreenName
{
   get => _screenName;
   set => _screenName = value ?? GenerateRandomScreenName();
}
private string _screenName = GenerateRandomScreenName();
```

Talvez seja necessário adicionar uma `using` diretiva para <xref:System.Diagnostics.CodeAnalysis> que o use este e outros atributos discutidos neste artigo. O atributo é aplicado à propriedade, não ao `set` acessador. O `AllowNull` atributo especifica *pré-condições*e só se aplica a entradas. O `get` acessador tem um valor de retorno, mas nenhum argumento de entrada. Portanto, o `AllowNull` atributo só se aplica ao `set` acessador.

O exemplo anterior demonstra o que procurar ao adicionar o `AllowNull` atributo em um argumento:

1. O contrato geral para essa variável é que não deveria ser `null` , portanto, você deseja um tipo de referência não anulável.
1. Há cenários para a variável de entrada `null` , embora eles não sejam o uso mais comum.

Geralmente, você precisará desse atributo para propriedades, ou `in` , `out` e `ref` argumentos. O `AllowNull` atributo é a melhor opção quando uma variável normalmente é não nula, mas você precisa permitir `null` como uma pré-condição.

Compare com cenários para usar `DisallowNull` : Use esse atributo para especificar que uma variável de entrada de um tipo de referência anulável não deve ser `null` . Considere uma propriedade em que `null` é o valor padrão, mas os clientes só podem defini-lo como um valor não nulo. Considere o seguinte código:

```csharp
public string ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string _comment;
```

O código anterior é a melhor maneira de expressar o design que `ReviewComment` pode ser `null` , mas não pode ser definido como `null` . Depois que esse código é ciente de forma anulável, você pode expressar esse conceito mais claramente para os chamadores usando o <xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute?displayProperty=nameWithType> :

```csharp
[DisallowNull]
public string? ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string? _comment;
```

Em um contexto anulável, o `ReviewComment` `get` acessador pode retornar o valor padrão de `null` . O compilador avisa que ele deve ser verificado antes do acesso. Além disso, ele avisa aos chamadores que, embora possa ser `null` , os chamadores não devem defini-los explicitamente como `null` . O `DisallowNull` atributo também especifica uma *pré-condição*, ele não afeta o `get` acessador. Você usa o `DisallowNull` atributo ao observar essas características sobre:

1. A variável pode estar `null` em cenários principais, geralmente quando a primeira instância é instanciada.
1. A variável não deve ser definida explicitamente como `null` .

Essas situações são comuns no código que era originalmente *nulo alheios*. Pode ser que as propriedades do objeto sejam definidas em duas operações de inicialização distintas. Pode ser que algumas propriedades sejam definidas somente após a conclusão de algum trabalho assíncrono.

Os `AllowNull` `DisallowNull` atributos e permitem que você especifique que as pré-condições nas variáveis podem não corresponder às anotações que permitem valor nulo nessas variáveis. Eles fornecem mais detalhes sobre as características de sua API. Essas informações adicionais ajudam os chamadores a usar sua API corretamente. Lembre-se de especificar as pré-condições usando os seguintes atributos:

- [AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute): um argumento de entrada não anulável pode ser nulo.
- [DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute): um argumento de entrada anulável nunca deve ser nulo.

## <a name="specify-post-conditions-maybenull-and-notnull"></a>Especificar pós-condições: `MaybeNull` e `NotNull`

Suponha que você tenha um método com a seguinte assinatura:

```csharp
public Customer FindCustomer(string lastName, string firstName)
```

Você provavelmente escreveu um método como este para retornar `null` quando o nome procurado não foi encontrado. O `null` claramente indica que o registro não foi encontrado. Neste exemplo, você provavelmente alteraria o tipo de retorno de `Customer` para `Customer?` . Declarar o valor de retorno como um tipo de referência anulável especifica claramente a intenção dessa API.

Por motivos abordados em [definições genéricas e nulidade](../../nullable-migration-strategies.md#generic-definitions-and-nullability) que a técnica não funciona com métodos genéricos. Você pode ter um método genérico que segue um padrão semelhante:

```csharp
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> predicate)
```

Você não pode especificar que o valor de retorno é `T?` . O método retorna `null` quando o item procurado não é encontrado. Como não é possível declarar um `T?` tipo de retorno, você adiciona a `MaybeNull` anotação ao método Return:

```csharp
[return: MaybeNull]
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> predicate)
```

O código anterior informa aos chamadores que o contrato implica em um tipo não anulável, mas o valor de retorno *pode* ser, na verdade, nulo.  Use o `MaybeNull` atributo quando sua API deve ser um tipo não anulável, normalmente um parâmetro de tipo genérico, mas pode haver instâncias em que `null` seriam retornadas.

Você também pode especificar que um valor de retorno ou `out` um `ref` argumento or não seja nulo, embora o tipo seja um tipo de referência anulável. Considere um método que garanta que uma matriz seja grande o suficiente para conter vários elementos. Se o argumento de entrada não tiver capacidade, a rotina alocaria uma nova matriz e copiaria todos os elementos existentes nela. Se o argumento de entrada for `null` , a rotina alocaria novo armazenamento. Se houver capacidade suficiente, a rotina não fará nada:

```csharp
public void EnsureCapacity<T>(ref T[] storage, int size)
```

Você pode chamar essa rotina da seguinte maneira:

```csharp
// messages has the default value (null) when EnsureCapacity is called:
EnsureCapacity<string>(ref messages, 10);
// messages is not null.
EnsureCapacity<string>(messages, 50);
```

Depois de habilitar tipos de referência NULL, você deseja garantir que o código anterior seja compilado sem avisos. Quando o método retorna, `storage` é garantido que o argumento não seja nulo. No entanto, é aceitável chamar `EnsureCapacity` com uma referência nula. Você pode criar `storage` um tipo de referência anulável e adicionar a `NotNull` pós-condição à declaração de parâmetro:

```csharp
public void EnsureCapacity<T>([NotNull] ref T[]? storage, int size)
```

O código anterior expressa o contrato existente claramente: os chamadores podem passar uma variável com o `null` valor, mas é garantido que o valor de retorno nunca seja nulo. O `NotNull` atributo é mais útil para `ref` `out` argumentos e em que `null` pode ser passado como um argumento, mas esse argumento é garantido como não nulo quando o método retorna.

Você especifica condições de erro incondicionais usando os seguintes atributos:

- [MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute): um valor de retorno não anulável pode ser nulo.
- Não [nulo](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute): um valor de retorno anulável nunca será nulo.

## <a name="specify-conditional-post-conditions-notnullwhen-maybenullwhen-and-notnullifnotnull"></a>Especificar pós-condições condicionais: `NotNullWhen` , `MaybeNullWhen` e `NotNullIfNotNull`

Você provavelmente está familiarizado com o `string` método <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType> . Esse método retorna `true` quando o argumento é nulo ou uma cadeia de caracteres vazia. É uma forma de verificação nula: os chamadores não precisam ser nulos. Verifique o argumento se o método retornar `false` . Para tornar um método como esse reconhecimento anulável, você definiria o argumento como um tipo de referência anulável e adicionaria o `NotNullWhen` atributo:

```csharp
bool IsNullOrEmpty([NotNullWhen(false)] string? value);
```

Isso informa ao compilador que qualquer código em que o valor de retorno `false` não precisa ser marcado como nulo. A adição do atributo informa a análise estática do compilador que `IsNullOrEmpty` executa a verificação nula necessária: quando retorna `false` , o argumento de entrada não é `null` .

```csharp
string? userInput = GetUserInput();
if (!string.IsNullOrEmpty(userInput))
{
   int messageLength = userInput.Length; // no null check needed.
}
// null check needed on userInput here.
```

O <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType> método será anotado conforme mostrado acima para o .NET Core 3,0. Você pode ter métodos semelhantes em sua base de código que verificam o estado dos objetos em busca de valores nulos. O compilador não reconhecerá os métodos de verificação NULL personalizados e você precisará adicionar as anotações por conta própria. Quando você adiciona o atributo, a análise estática do compilador sabe quando a variável testada foi marcada como nula.

Outro uso para esses atributos é o `Try*` padrão. As condições para `ref` e as `out` variáveis são comunicadas por meio do valor de retorno. Considere este método mostrado anteriormente:

```csharp
bool TryGetMessage(string key, out string message)
```

O método anterior segue um idioma .NET típico: o valor de retorno indica se `message` foi definido como o valor encontrado ou, se nenhuma mensagem for encontrada, ao valor padrão. Se o método retornar `true` , o valor de `message` não será nulo; caso contrário, o método definirá `message` como nulo.

Você pode comunicar esse idioma usando o `NotNullWhen` atributo. Quando você atualiza a assinatura para tipos de referência anuláveis, faça `message` um `string?` e adicione um atributo:

```csharp
bool TryGetMessage(string key, [NotNullWhen(true)] out string? message)
```

No exemplo anterior, o valor de `message` é conhecido como não nulo quando `TryGetMessage` retorna `true` . Você deve anotar métodos semelhantes em sua base de código da mesma maneira: os argumentos podem ser `null` , e são conhecidos como não nulos quando o método retorna `true` .

Há um atributo final que você também pode precisar. Às vezes, o estado nulo de um valor de retorno depende do estado nulo de um ou mais argumentos de entrada. Esses métodos retornarão um valor não nulo sempre que determinados argumentos de entrada não forem `null` . Para anotar corretamente esses métodos, use o `NotNullIfNotNull` atributo. Considere o seguinte método:

```csharp
string GetTopLevelDomainFromFullUrl(string url);
```

Se o `url` argumento não for nulo, a saída não será `null` . Depois que as referências anuláveis estiverem habilitadas, essa assinatura funcionará corretamente, desde que sua API nunca aceite uma entrada nula. No entanto, se a entrada puder ser nula, o valor de retorno também poderá ser nulo. Portanto, você pode alterar a assinatura para o código a seguir:

```csharp
string? GetTopLevelDomainFromFullUrl(string? url);
```

Isso também funciona, mas geralmente forçará os chamadores a implementarem `null` verificações adicionais. O contrato é que o valor de retorno seria `null` apenas quando o argumento de entrada `url` é `null` . Para expressar esse contrato, você anotaria esse método, conforme mostrado no código a seguir:

```csharp
[return: NotNullIfNotNull("url")]
string? GetTopLevelDomainFromFullUrl(string? url);
```

O valor de retorno e o argumento foram anotados com o que `?` indica que pode ser `null` . O atributo esclarece ainda mais que o valor de retorno não será nulo quando o `url` argumento não for `null` .

Você especifica condições recondicionais usando estes atributos:

- [MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute): um argumento de entrada não anulável pode ser nulo quando o método retorna o `bool` valor especificado.
- [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute): um argumento de entrada anulável não será nulo quando o método retornar o `bool` valor especificado.
- [NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute): um valor de retorno não será nulo se o argumento de entrada para o parâmetro especificado não for nulo.

## <a name="verify-unreachable-code"></a>Verificar código inacessível

Alguns métodos, normalmente os auxiliares de exceção ou outros métodos de utilitário, sempre saem lançando uma exceção. Ou, um auxiliar pode gerar uma exceção com base no valor de um argumento booliano.

No primeiro caso, você pode adicionar o `DoesNotReturn` atributo à declaração do método. O compilador o ajuda de três maneiras. Primeiro, o compilador emite um aviso se houver um caminho onde o método pode sair sem lançar uma exceção. Em segundo lugar, o compilador marca qualquer código depois de uma chamada para esse método como *inacessível*, até que uma `catch` cláusula apropriada seja encontrada. Terceiro, o código inacessível não afetará nenhum estado nulo. Considere este método:

```csharp
[DoesNotReturn]
private void FailFast()
{
    throw new InvalidOperationException();
}

public void SetState(object containedField)
{
    if (!isInitialized)
    {
        FailFast();
    }

    // unreachable code:
    _field = containedField;
}
```

No segundo caso, você adiciona o `DoesNotReturnIf` atributo a um parâmetro booliano do método. Você pode modificar o exemplo anterior da seguinte maneira:

```csharp
private void FailFast([DoesNotReturnIf(false)] bool isValid)
{
    if (!isValid)
    {
        throw new InvalidOperationException();
    }
}

public void SetState(object containedField)
{
    FailFast(isInitialized);

    // unreachable code when "isInitialized" is false:
    _field = containedField;
}
```

## <a name="summary"></a>Resumo

[!INCLUDE [C# version alert](../../includes/csharp-version-alert.md)]

A adição de tipos de referência anuláveis fornece um vocabulário inicial para descrever suas expectativas de APIs para variáveis que podem ser `null` . Os atributos adicionais fornecem um vocabulário mais rico para descrever o estado nulo de variáveis como pré-condições e condições. Esses atributos descrevem mais claramente suas expectativas e fornecem uma experiência melhor para os desenvolvedores que usam suas APIs.

Conforme você atualiza as bibliotecas para um contexto anulável, adicione esses atributos para orientar os usuários de suas APIs para o uso correto. Esses atributos ajudam você a descrever totalmente o estado nulo dos argumentos de entrada e valores de retorno:

- [AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute): um argumento de entrada não anulável pode ser nulo.
- [DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute): um argumento de entrada anulável nunca deve ser nulo.
- [MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute): um valor de retorno não anulável pode ser nulo.
- Não [nulo](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute): um valor de retorno anulável nunca será nulo.
- [MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute): um argumento de entrada não anulável pode ser nulo quando o método retorna o `bool` valor especificado.
- [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute): um argumento de entrada anulável não será nulo quando o método retornar o `bool` valor especificado.
- [NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute): um valor de retorno não será nulo se o argumento de entrada para o parâmetro especificado não for nulo.
- [DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute): um método nunca retorna. Em outras palavras, ele sempre gera uma exceção.
- [DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute): esse método nunca retorna se o `bool` parâmetro associado tiver o valor especificado.
