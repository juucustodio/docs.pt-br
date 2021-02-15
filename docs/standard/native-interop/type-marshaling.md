---
title: Marshaling de tipo – .NET
description: Saiba como o .NET realizar marshal de seus tipos para uma representação nativa.
ms.date: 01/18/2019
ms.openlocfilehash: 7fc3dfe950ecd3ed0ff5e4eb0e101c1596a831e1
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440992"
---
# <a name="type-marshaling"></a>Marshaling de tipo

**Marshaling** é o processo de transformar tipos quando precisam atravessar entre código nativo e gerenciado.

O marshaling é necessário porque os tipos são diferentes, no código gerenciado e não gerenciado. No código gerenciado, por exemplo, você tem um `String` , enquanto nas cadeias de caracteres do mundo não gerenciadas pode ser Unicode ("largo"), não-Unicode, terminação nula, ASCII, etc. Por padrão, o subsistema P/Invoke tenta fazer a coisa certa com base no comportamento padrão, descrito neste artigo. Contudo, nas situações em que você precisa de controle extra, pode utilizar o atributo [MarshalAs](xref:System.Runtime.InteropServices.MarshalAsAttribute) para especificar qual é o tipo esperado no lado não gerenciado. Por exemplo, se você quiser que a cadeia de caracteres seja enviada como uma cadeia de caracteres ANSI terminada em nulo, faça o seguinte:

```csharp
[DllImport("somenativelibrary.dll")]
static extern int MethodA([MarshalAs(UnmanagedType.LPStr)] string parameter);
```

## <a name="default-rules-for-marshaling-common-types"></a>Regras padrão para tipos comuns de marshaling

Geralmente, o runtime tenta fazer a "coisa certa" ao realizar marshaling para exigir a menor quantidade de trabalho de você. As tabelas a seguir descrevem como cada tipo tem o marshaling realizado por padrão quando usado em um parâmetro ou campo. Os tipos de caracteres e números inteiros de largura fixa C99/C++11 são usados ​​para garantir que a tabela a seguir esteja correta para todas as plataformas. Use qualquer tipo nativo que tenha os mesmos requisitos de alinhamento e tamanho que esses tipos.

Esta primeira tabela descreve os mapeamentos para vários tipos para os quais o marshaling é o mesmo para ambos P/Invoke e o marshaling do campo.

| Tipo .NET | Tipo nativo  |
|-----------|-------------------------|
| `byte`    | `uint8_t`               |
| `sbyte`   | `int8_t`                |
| `short`   | `int16_t`               |
| `ushort`  | `uint16_t`              |
| `int`     | `int32_t`               |
| `uint`    | `uint32_t`              |
| `long`    | `int64_t`               |
| `ulong`   | `uint64_t`              |
| `char`    | `char` ou `char16_t` dependendo do `CharSet` do P/Invoke ou da estrutura. Confira a [documentação do conjunto de caracteres](charset.md). |
| `string`  | `char*` ou `char16_t*` dependendo do `CharSet` do P/Invoke ou da estrutura. Confira a [documentação do conjunto de caracteres](charset.md). |
| `System.IntPtr` | `intptr_t`        |
| `System.UIntPtr` | `uintptr_t`      |
| Tipos de ponteiro do .NET (por exemplo: `void*`)  | `void*` |
| Tipo derivado de `System.Runtime.InteropServices.SafeHandle` | `void*` |
| Tipo derivado de `System.Runtime.InteropServices.CriticalHandle` | `void*`          |
| `bool`    | Tipo `BOOL` Win32       |
| `decimal` | Struct `DECIMAL` COM |
| Representante do .NET | Ponteiro de função nativo |
| `System.DateTime` | Tipo `DATE` Win32 |
| `System.Guid` | Tipo `GUID` Win32 |

Algumas categorias de marshaling terão padrões diferentes se você estiver realizando marshaling como um parâmetro ou uma estrutura.

| Tipo .NET | Tipo nativo (parâmetro) | Tipo nativo (campo) |
|-----------|-------------------------|---------------------|
| Matriz .NET | Um ponteiro para o início de uma matriz de representações nativas dos elementos da matriz. | Não é permitida sem um atributo `[MarshalAs]`|
| Uma classe com um `LayoutKind` de `Sequential` ou `Explicit` | Um ponteiro para a representação nativa da classe | A representação nativa da classe |

A tabela a seguir inclui as regras de marshaling padrão que são somente do Windows. Em plataformas que não são Windows, você não pode realizar marshal desses tipos.

| Tipo .NET | Tipo nativo (parâmetro) | Tipo nativo (campo) |
|-----------|-------------------------|---------------------|
| `object`  | `VARIANT`               | `IUnknown*`         |
| `System.Array` | Interface COM | Não é permitida sem um atributo `[MarshalAs]` |
| `System.ArgIterator` | `va_list` | Não permitido |
| `System.Collections.IEnumerator` | `IEnumVARIANT*` | Não permitido |
| `System.Collections.IEnumerable` | `IDispatch*` | Não permitido |
| `System.DateTimeOffset` | `int64_t` representando o número de tiques desde a meia-noite de 1º de janeiro de 1601 | `int64_t` representando o número de tiques desde a meia-noite de 1º de janeiro de 1601 |

Alguns tipos só podem ter o marshaling realizado como parâmetros e não como campos. Esses tipos estão listados na tabela a seguir:

| Tipo .NET | Tipo nativo (parâmetro somente) |
|-----------|------------------------------|
| `System.Text.StringBuilder` | `char*` ou `char16_t*` dependendo do `CharSet` do P/Invoke.  Confira a [documentação do conjunto de caracteres](charset.md). |
| `System.ArgIterator` | `va_list` (no Windows x86/x64/arm64 somente) |
| `System.Runtime.InteropServices.ArrayWithOffset` | `void*` |
| `System.Runtime.InteropServices.HandleRef` | `void*` |

Se esses padrões não fizerem exatamente o que você deseja, personalize como os parâmetros têm o marshaling realizado. O artigo sobre [marshaling de parâmetro](customize-parameter-marshaling.md) explica como personalizar a forma como os tipos de parâmetros diferentes têm o marshaling realizado.

## <a name="default-marshaling-in-com-scenarios"></a>Marshaling padrão em cenários COM

Quando você chama métodos em objetos COM no .NET, o runtime do .NET altera a regras de marshaling padrão para corresponder à semântica de COM. A tabela a seguir lista as regras que os runtimes do .NET usam em cenários COM:

| Tipo .NET | Tipo nativo (chamadas de método COM) |
|-----------|--------------------------------|
| `bool`    | `VARIANT_BOOL`                 |
| `StringBuilder` | `LPWSTR`                 |
| `string`  | `BSTR`                         |
| Tipos delegados | `_Delegate*` no .NET Framework. Não permitido no .NET Core e no .NET 5 +. |
| `System.Drawing.Color` | `OLECOLOR`        |
| Matriz .NET | `SAFEARRAY`                   |
| `string[]` | `SAFEARRAY` de `BSTR`s        |

## <a name="marshaling-classes-and-structs"></a>Marshaling de classes e structs

Outro aspecto do marshaling de tipos é como passar um struct para um método não gerenciado. Por exemplo, alguns dos métodos não gerenciados requerem um struct como parâmetro. Nesses casos, você precisa criar um struct correspondente ou uma classe na parte gerenciada do mundo para usar como parâmetro. No entanto, definir a classe não é suficiente; também é necessário ensinar o marshaler como mapear campos na classe para o struct não gerenciado. Aqui, o atributo `StructLayout` se torna útil.

```csharp
[DllImport("kernel32.dll")]
static extern void GetSystemTime(SystemTime systemTime);

[StructLayout(LayoutKind.Sequential)]
class SystemTime {
    public ushort Year;
    public ushort Month;
    public ushort DayOfWeek;
    public ushort Day;
    public ushort Hour;
    public ushort Minute;
    public ushort Second;
    public ushort Milsecond;
}

public static void Main(string[] args) {
    SystemTime st = new SystemTime();
    GetSystemTime(st);
    Console.WriteLine(st.Year);
}
```

O código anterior mostra um exemplo simples de chamar para a função `GetSystemTime()`. A parte interessante está na linha 4. O atributo especifica que os campos da classe devem ser mapeados em sequência até o struct no outro lado (não gerenciado). Isso significa que os nomes dos campos não são importantes, apenas sua ordem é importante, já que precisa corresponder ao struct não gerenciado, mostrado no exemplo abaixo:

```c
typedef struct _SYSTEMTIME {
  WORD wYear;
  WORD wMonth;
  WORD wDayOfWeek;
  WORD wDay;
  WORD wHour;
  WORD wMinute;
  WORD wSecond;
  WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME;
```

Às vezes, o marshaling padrão para sua estrutura não faz o que você precisa. O artigo [Personalizando o marshaling de estrutura](./customize-struct-marshaling.md) ensina como personalizar a forma como sua estrutura tem o marshaling realizado.
