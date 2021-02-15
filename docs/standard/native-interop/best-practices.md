---
title: Práticas recomendadas de interoperabilidade nativa - .NET
description: Saiba mais sobre as práticas recomendadas para fazer interface com componentes nativos no .NET.
ms.date: 01/18/2019
ms.openlocfilehash: e64aa0aa43a56145bd7636835f507f8433fa3db4
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100465243"
---
# <a name="native-interoperability-best-practices"></a>Práticas recomendadas de interoperabilidade nativa

.NET oferece uma variedade maneiras de personalizar seu código de interoperabilidade nativa. Este artigo inclui as diretrizes que as equipes .NET da Microsoft seguem para a interoperabilidade nativa.

## <a name="general-guidance"></a>Orientação geral

As diretrizes nesta seção se aplicam a todos os cenários de interoperabilidade.

- ✔️ USE a mesma nomenclatura e uso de maiúsculas para seus métodos e parâmetros como o método nativo que você deseja chamar.
- ✔️ CONSIDERE usar a mesma nomenclatura e uso de maiúsculas para valores constantes.
- ✔️ USE tipos .NET com mapeamento mais próximo do tipo nativo. Por exemplo, no caso de C#, use `uint` quando o tipo nativo for `unsigned int`.
- ✔️ USE os atributos `[In]` e `[Out]` somente quando o comportamento desejado for diferente do comportamento padrão.
- ✔️ CONSIDERE usar <xref:System.Buffers.ArrayPool%601?displayProperty=nameWithType> para agrupar seus buffers de matriz nativos.
- ✔️ CONSIDERE encapsular suas declarações P/Invoke em uma classe com o mesmo nome e letras maiúsculas como sua biblioteca nativa.
  - Isso permite que seus atributos `[DllImport]` usem o recurso de linguagem C# `nameof` para passar o nome da biblioteca nativa e garantir que você não tenha digitado errado o nome da biblioteca nativa.

## <a name="dllimport-attribute-settings"></a>Configurações de atributo DllImport

| Configuração | Padrão | Recomendação | Detalhes |
|---------|---------|----------------|---------|
| <xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>   | `true` |  manter padrão  | Quando esta configuração é definida como false, valores de retorno HRESULT com falha serão considerados exceções (e o valor de retorno na definição torna-se nulo).|
| <xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError> | `false`  | depende da API  | Defina esta configuração como true se a API usa GetLastError e usa Marshal.GetLastWin32Error para obter o valor. Se a API definir uma condição que informa um erro, obtenha o erro antes de fazer outras chamadas para evitar que ele seja sobrescrito inadvertidamente.|
| <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> | `CharSet.None`, que reverte para o comportamento `CharSet.Ansi`  | Use explicitamente `CharSet.Unicode` ou `CharSet.Ansi` quando os caracteres ou cadeias de caracteres estiverem presentes na definição | Isso especifica o comportamento de marshaling de cadeias de caracteres e o que `ExactSpelling` faz quando `false`. Note que `CharSet.Ansi` é na verdade UTF8 no Unix. O Windows usa Unicode a _maior parte_ do tempo, enquanto o Unix usa UTF8. Veja mais informações na [documentação sobre conjuntos de caracteres](./charset.md). |
| <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling> | `false` | `true`             | Defina como true e obtenha um pequeno benefício de desempenho: o runtime não irá buscar por nomes de função alternativos com o sufixo "A" ou "W" dependendo do valor da configuração `CharSet` ("A" para `CharSet.Ansi` e "W" para `CharSet.Unicode`). |

## <a name="string-parameters"></a>Parâmetros de cadeia de caracteres

Quando o CharSet é Unicode ou o argumento é explicitamente marcado como `[MarshalAs(UnmanagedType.LPWSTR)]` _e_ a cadeia de caracteres é passada por valor (não `ref` ou `out`), a cadeia de caracteres será fixada e usada diretamente pelo código nativo (em vez de copiado).

Lembre-se de marcar `[DllImport]` como `Charset.Unicode`, a menos que você queira explicitamente o tratamento ANSI de suas cadeias de caracteres.

❌ Não use `[Out] string` parâmetros. Os parâmetros de cadeia de caracteres passados por valor com o atributo `[Out]` podem desestabilizar o runtime se a cadeia de caracteres for uma cadeia de caracteres internada. Veja mais informações sobre a centralização da cadeia de caracteres na documentação do <xref:System.String.Intern%2A?displayProperty=nameWithType>.

❌ Evite `StringBuilder` parâmetros. Marshaling de `StringBuilder`*sempre* cria uma cópia do buffer nativo. Dessa forma, ele pode ser extremamente ineficiente. Veja o cenário típico da chamada de uma API do Windows que usa uma cadeia de caracteres:

1. Criar uma SB da capacidade desejada (aloca capacidade gerenciada) **{1}**
2. Invoke
   1. Aloca um buffer nativo **{2}**
   2. Copia o conteúdo se `[In]` _(o padrão para um parâmetro `StringBuilder`)_
   3. Copia o buffer nativo em uma matriz gerenciada recém-alocada se `[Out]` **{3}** _(também é o padrão para `StringBuilder`)_
3. `ToString()` aloca ainda outra matriz gerenciada **{4}**

São as *{4}* alocações para obter uma cadeia de caracteres de código nativo. O melhor que você pode fazer para limitar isso é reutilizar o `StringBuilder` em outra chamada, mas isso economiza apenas *1* alocação. É muito melhor usar e armazenar em cache um buffer de caractere de `ArrayPool` - você pode então reduzir para apenas a alocação para `ToString()` nas chamadas subsequentes.

O outro problema com `StringBuilder` é que esta configuração sempre copia o buffer de retorno de volta para o primeiro nulo. Se a cadeia de caracteres transmitida não estiver terminada, ou terminar por dois caracteres nulos, na melhor das hipóteses, o recurso P/Invoke estará incorreto.

Se você *usar* o `StringBuilder`, uma última pegadinha é que a capacidade **não** inclui um nulo oculto, que é sempre contabilizado na interoperabilidade. É comum as pessoas entenderem errado, já que a maioria das APIs deseja o tamanho do buffer, *incluindo* o valor nulo. Isso pode resultar em alocações desnecessárias/desperdiçadas. Além disso, esse problema impede que o runtime otimize o marshaling de `StringBuilder` para minimizar as cópias.

✔️ CONSIDERE usar `char[]`s de um `ArrayPool`.

Para obter mais informações sobre o marshaling de cadeia de caracteres, veja [Marshaling padrão para cadeias de caracteres](../../framework/interop/default-marshaling-for-strings.md) e [Personalizando marshaling de cadeia de caracteres](customize-parameter-marshaling.md#customizing-string-parameters).

> __Específico do Windows__ Para `[Out]` cadeias de caracteres, o CLR usará `CoTaskMemFree` por padrão para cadeias de caracteres livres ou `SysStringFree` para cadeias de caracteres marcadas como `UnmanagedType.BSTR` .
> **Para a maioria das APIs com um buffer de cadeia de caracteres de saída:** A contagem de caracteres transmitida deve incluir o nulo. Se o valor retornado for menor que a contagem de caracteres transmitidos, a chamada foi bem-sucedida e o valor consiste no número de caracteres *sem* o nulo à direita. Caso contrário, a contagem consiste no tamanho necessário do buffer *incluindo* o caractere nulo.
>
> - Pass em 5, Get 4: a cadeia de caracteres tem 4 caracteres de comprimento com um nulo à direita.
> - Passar em 5, obter 6: a cadeia de caracteres tem 5 caracteres de comprimento, precisa de um buffer de 6 caracteres para manter o valor nulo.
> [Tipos de dados do Windows para cadeias de caracteres](/windows/desktop/Intl/windows-data-types-for-strings)

## <a name="boolean-parameters-and-fields"></a>Parâmetros e campos boolianos

É fácil cometer erros com boolianos. Por padrão, o marshaling de um `bool` .NET é realizado para um Windows `BOOL`, em que é um valor de 4 bytes. No entanto, os tipos `_Bool` e `bool` em C e C++ são um byte *único*. Isso pode dificultar o rastreamento de bugs, já que metade do valor de retorno será descartado, o que só *potencialmente* alterará o resultado. Para obter mais informações sobre o marshaling de valores do `bool` .NET para tipos `bool` C ou C++, veja a documentação sobre como [personalizar marshaling de campo booliano](customize-struct-marshaling.md#customizing-boolean-field-marshaling).

## <a name="guids"></a>GUIDs

Os GUIDs podem ser usados diretamente em assinaturas. Muitas APIs do Windows usam aliases do tipo `GUID&` como `REFIID`. Quando passadas por ref, elas podem ser passadas por `ref` ou pelo atributo `[MarshalAs(UnmanagedType.LPStruct)]`.

| GUID | GUID by-ref |
|------|-------------|
| `KNOWNFOLDERID` | `REFKNOWNFOLDERID` |

❌ Não use `[MarshalAs(UnmanagedType.LPStruct)]` para nada além dos `ref` parâmetros de GUID.

## <a name="blittable-types"></a>Tipos blittable

Os tipos blittable são tipos que têm a mesma representação em nível de bits no código gerenciado e nativo. Como tal, eles não precisam ser convertidos em outro formato para serem empacotados para e do código nativo e, uma vez que isso melhora o desempenho, eles devem ter preferência. Alguns tipos não são blittable, mas são conhecidos por conterem conteúdo blittable. Esses tipos têm otimizações semelhantes como tipos blittable quando não estão contidas em outro tipo, mas não são consideradas blittable em campos de structs ou para fins de [`UnmanagedCallersOnlyAttribute`](xref:System.Runtime.InteropServices.UnmanagedCallersOnlyAttribute) .

**Tipos blittable:**

- `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `single`, `double`
- structs com layout fixo que só têm tipos de valor blittable para campos de instância
  - layout fixo requer `[StructLayout(LayoutKind.Sequential)]` ou `[StructLayout(LayoutKind.Explicit)]`
  - as structs são `LayoutKind.Sequential` por padrão

**Tipos com conteúdo blittable:**

- matrizes unidimensionais e não aninhadas de tipos primitivos blittable (por exemplo, `int[]` )
- classes com layout fixo que só têm tipos de valor blittable para campos de instância
  - layout fixo requer `[StructLayout(LayoutKind.Sequential)]` ou `[StructLayout(LayoutKind.Explicit)]`
  - as classes são `LayoutKind.Auto` por padrão

**NÃO blittable:**

- `bool`

**ÀS VEZES blittable:**

- `char`

**Tipos com, às vezes, conteúdo blittable:**

- `string`

Quando os tipos blittable são passados por referência com `in` , `ref` ou `out` , ou quando os tipos com conteúdo blittable são passados por valor, eles são simplesmente fixados pelo Marshaller em vez de serem copiados para um buffer intermediário.

`char` é blittable em uma matriz unidimensional **ou** se for parte de um tipo que é explicitamente marcado com `[StructLayout]` com `CharSet = CharSet.Unicode`.

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct UnicodeCharStruct
{
    public char c;
}
```

`string` contém conteúdo blittable se ele não está contido em outro tipo e está sendo passado como um argumento que está marcado com `[MarshalAs(UnmanagedType.LPWStr)]` ou o `[DllImport]` foi `CharSet = CharSet.Unicode` definido.

Você pode ver se um tipo é blittable ou contém conteúdo blittable tentando criar um fixo `GCHandle` . Se o tipo não for uma cadeia de caracteres ou considerado blittable, `GCHandle.Alloc` lançará um `ArgumentException`.

✔️ TORNE suas estruturas mais blittable quando possível.

Para obter mais informações, consulte:

- [Tipos blittable e não blittable](../../framework/interop/blittable-and-non-blittable-types.md)
- [Empacotamento de tipo](type-marshaling.md)

## <a name="keeping-managed-objects-alive"></a>Manter objetos gerenciados ativos

`GC.KeepAlive()` garantirá que um objeto permaneça no escopo até que o método KeepAlive seja alcançado.

[`HandleRef`](xref:System.Runtime.InteropServices.HandleRef) permite que o Marshaller mantenha um objeto ativo pela duração de um P/Invoke. Ele pode ser usado em vez de `IntPtr` em assinaturas de métodos. `SafeHandle` substitui efetivamente essa classe e deve ser usado em seu lugar.

[`GCHandle`](xref:System.Runtime.InteropServices.GCHandle) permite fixar um objeto gerenciado e obter o ponteiro nativo para ele. O padrão básico é:

```csharp
GCHandle handle = GCHandle.Alloc(obj, GCHandleType.Pinned);
IntPtr ptr = handle.AddrOfPinnedObject();
handle.Free();
```

Fixar não é o padrão para `GCHandle`. O outro padrão principal é passar uma referência a um objeto gerenciado por meio do código nativo e voltar ao código gerenciado, geralmente com um retorno de chamada. Aqui está o padrão:

```csharp
GCHandle handle = GCHandle.Alloc(obj);
SomeNativeEnumerator(callbackDelegate, GCHandle.ToIntPtr(handle));

// In the callback
GCHandle handle = GCHandle.FromIntPtr(param);
object managedObject = handle.Target;

// After the last callback
handle.Free();
```

Não se esqueça que `GCHandle` precisa ser explicitamente liberado para evitar perda de memória.

## <a name="common-windows-data-types"></a>Tipos de dados comuns do Windows

Veja a seguir uma lista dos tipos de dados comumente usados em APIs do Windows e quais tipos C# devem ser usados ao chamar o código do Windows.

Os tipos a seguir são do mesmo tamanho no Windows de 32 e 64 bits, apesar de seus nomes.

| Largura | Windows          | C (Windows)          | C#       | Alternativa                          |
|:------|:-----------------|:---------------------|:---------|:-------------------------------------|
| 32    | `BOOL`           | `int`                | `int`    | `bool`                               |
| 8     | `BOOLEAN`        | `unsigned char`      | `byte`   | `[MarshalAs(UnmanagedType.U1)] bool` |
| 8     | `BYTE`           | `unsigned char`      | `byte`   |                                      |
| 8     | `CHAR`           | `char`               | `sbyte`  |                                      |
| 8     | `UCHAR`          | `unsigned char`      | `byte`   |                                      |
| 16    | `SHORT`          | `short`              | `short`  |                                      |
| 16    | `CSHORT`         | `short`              | `short`  |                                      |
| 16    | `USHORT`         | `unsigned short`     | `ushort` |                                      |
| 16    | `WORD`           | `unsigned short`     | `ushort` |                                      |
| 16    | `ATOM`           | `unsigned short`     | `ushort` |                                      |
| 32    | `INT`            | `int`                | `int`    |                                      |
| 32    | `LONG`           | `long`               | `int`    |                                      |
| 32    | `ULONG`          | `unsigned long`      | `uint`   |                                      |
| 32    | `DWORD`          | `unsigned long`      | `uint`   |                                      |
| 64    | `QWORD`          | `long long`          | `long`   |                                      |
| 64    | `LARGE_INTEGER`  | `long long`          | `long`   |                                      |
| 64    | `LONGLONG`       | `long long`          | `long`   |                                      |
| 64    | `ULONGLONG`      | `unsigned long long` | `ulong`  |                                      |
| 64    | `ULARGE_INTEGER` | `unsigned long long` | `ulong`  |                                      |
| 32    | `HRESULT`        | `long`               | `int`    |                                      |
| 32    | `NTSTATUS`       | `long`               | `int`    |                                      |

Os tipos a seguir, sendo ponteiros, seguem a largura da plataforma. Use `IntPtr`/`UIntPtr` para eles.

| Tipos de ponteiros assinados (use `IntPtr`) | Tipos de ponteiros não assinados (use `UIntPtr`) |
|:------------------------------------|:---------------------------------------|
| `HANDLE`                            | `WPARAM`                               |
| `HWND`                              | `UINT_PTR`                             |
| `HINSTANCE`                         | `ULONG_PTR`                            |
| `LPARAM`                            | `SIZE_T`                               |
| `LRESULT`                           |                                        |
| `LONG_PTR`                          |                                        |
| `INT_PTR`                           |                                        |

Um `PVOID`Windows que é um `void*` C pode passar por marshalling como `IntPtr` ou `UIntPtr`, mas prefere `void*` quando possível.

[Tipos de dados do Windows](/windows/desktop/WinProg/windows-data-types)

[Intervalos de tipos de dados](/cpp/cpp/data-type-ranges)

## <a name="structs"></a>Estruturas

As structs gerenciadas são criadas e não são removidas até o método retornar. Por definição, elas são "fixadas" (não serão movidas pelo GC). Você também pode simplesmente pegar o endereço em blocos de código não seguros se o código nativo não usar o ponteiro após o final do método atual.

Structs blittable são muito mais eficazes, pois simplesmente podem ser usados de modo direto pela camada de marshaling. Tente tornar structs blittable (por exemplo, evite `bool`). Para saber mais, veja a seção [Tipos blittable](#blittable-types).

*Se* a struct é blittable, use `sizeof()` em vez de `Marshal.SizeOf<MyStruct>()` para melhor desempenho. Como mencionado acima, você pode validar que o tipo é blittable ao tentar criar um `GCHandle` fixado. Se o tipo não for uma cadeia de caracteres ou considerado blittable, `GCHandle.Alloc` lançara `ArgumentException`.

Os ponteiros para structs nas definições devem ser transmitidos por `ref` ou usar `unsafe` e `*`.

✔️ BUSQUE a struct gerenciada o mais próximo possível da forma e dos nomes usados na documentação ou no cabeçalho da plataforma oficial.

✔️ USE`sizeof()` C# em vez de `Marshal.SizeOf<MyStruct>()` para estruturas blittable a fim de melhorar o desempenho.

❌ Evite usar `System.Delegate` `System.MulticastDelegate` campos ou para representar campos de ponteiro de função em estruturas.

Como <xref:System.Delegate?displayProperty=fullName> e <xref:System.MulticastDelegate?displayProperty=fullName> não têm uma assinatura necessária, elas não garantem que o delegado passado corresponda à assinatura esperada pelo código nativo. Além disso, no .NET Framework e no .NET Core, o marshaling de um struct contendo uma `System.Delegate` ou `System.MulticastDelegate` de sua representação nativa para um objeto gerenciado pode desestabilizar o tempo de execução se o valor do campo na representação nativa não for um ponteiro de função que encapsula um delegado gerenciado. No .NET 5 e versões posteriores, não há suporte para o marshaling de um `System.Delegate` `System.MulticastDelegate` campo ou de uma representação nativa para um objeto gerenciado. Use um tipo delegado específico em vez de `System.Delegate` ou `System.MulticastDelegate` .

### <a name="fixed-buffers"></a>Buffers fixos

Uma matriz como `INT_PTR Reserved1[2]` precisa ser empacotada para dois campos `IntPtr`, `Reserved1a` e `Reserved1b`. Quando a matriz nativa é um tipo primitivo, podemos usar a palavra-chave `fixed` para escrevê-la um pouco mais limpa. Por exemplo, `SYSTEM_PROCESS_INFORMATION` se parece com isso no cabeçalho nativo:

```c
typedef struct _SYSTEM_PROCESS_INFORMATION {
    ULONG NextEntryOffset;
    ULONG NumberOfThreads;
    BYTE Reserved1[48];
    UNICODE_STRING ImageName;
...
} SYSTEM_PROCESS_INFORMATION
```

Em C#, podemos escrevê-lo assim:

```csharp
internal unsafe struct SYSTEM_PROCESS_INFORMATION
{
    internal uint NextEntryOffset;
    internal uint NumberOfThreads;
    private fixed byte Reserved1[48];
    internal Interop.UNICODE_STRING ImageName;
    ...
}
```

No entanto, existem algumas armadilhas com buffers fixos. Buffers fixos de tipos não blittable não serão empacotados corretamente, portanto, a matriz no local precisa ser expandida para vários campos individuais. Além disso, no .NET Framework e no .NET Core antes da versão 3.0, se um struct contendo um campo de buffer fixo for aninhado dentro de um struct não blittable, não será realizado o marshaling correto do campo de buffer fixo para código nativo.
