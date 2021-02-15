---
title: P/Invoke de plataforma cruzada
description: Saiba quais caminhos o tempo de execução pesquisará ao carregar bibliotecas nativas por meio de P/Invoke. Saiba também como usar o SetDllImportResolver.
author: saul
ms.date: 01/31/2021
ms.openlocfilehash: 40ad87fe537ad043a488e4086814a58ef8e0211e
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99427478"
---
# <a name="writing-cross-platform-pinvoke-code"></a>Escrevendo código P/Invoke de plataforma cruzada

## <a name="library-name-variations"></a>Variações de nome de biblioteca

Para facilitar o código P/Invoke de plataforma cruzada, o tempo de execução adiciona a extensão de biblioteca compartilhada canônica ( `.dll` `.so` ou `.dylib` ) aos nomes de biblioteca nativa. No Linux e no macOS, o tempo de execução também tentará aguardar `lib` . Essas variações de nomes de biblioteca são pesquisadas automaticamente quando você usa APIs que carregam bibliotecas não gerenciadas (por exemplo, <xref:System.Runtime.InteropServices.DllImportAttribute> ).

> [!NOTE]
> Caminhos absolutos em nomes de biblioteca (por exemplo, `/usr/lib/libc` ) são tratados como estão e nenhuma variação será pesquisada.

Considere o seguinte exemplo de uso de P/Invoke:

```csharp
[DllImport("nativedep")]
static extern int ExportedFunction();
```

Ao executar no Windows, a DLL é pesquisada na seguinte ordem:

1. `nativedep`
1. `nativedep.dll` (se o nome da biblioteca ainda não terminar com `.dll` ou. `exe` )

Quando executado no Linux ou no macOS, o tempo de execução tentará prependente `lib` e acrescentará a extensão de biblioteca compartilhada canônica. Nesses sistemas operacionais, as variações de nome de biblioteca são tentadas na seguinte ordem:

1. `nativedep.so` / `nativedep.dylib`
1. `libnativedep.so` / `libnativedep.dylib`<sup>1</sup>
1. `nativedep`
1. `libnativedep` <sup>1</sup>

No Linux, a ordem de pesquisa será diferente se o nome da biblioteca terminar com `.so` ou contiver `.so.` (Observe o final `.` ). Considere o seguinte exemplo:

```csharp
[DllImport("nativedep.so.6")]
static extern int ExportedFunction();
```

Nesse caso, as variações de nome de biblioteca são tentadas na seguinte ordem:

1. `nativedep.so.6`
1. `libnativedep.so.6` <sup>1</sup>
1. `nativedep.so.6.so`
1. `libnativedep.so.6.so` <sup>1</sup>

<sup>1</sup> caminho será verificado somente se o nome da biblioteca não contiver um caractere separador de diretório ( `/` ).

## <a name="custom-import-resolver"></a>Resolvedor de importação personalizado

Em cenários mais complexos, você pode usar <xref:System.Runtime.InteropServices.NativeLibrary.SetDllImportResolver%2A> para resolver importações de dll em tempo de execução. No exemplo a seguir, `nativedep` é resolvido para `nativedep_avx2` se a CPU oferecer suporte a ela.

> [!TIP]
> Essa funcionalidade só está disponível no .NET 5 e no .NET Core 3,1 ou posterior.

[!code-csharp[import resolver](~/samples/snippets/standard/interop/pinvoke/import-resolver/Program.cs)]

## <a name="see-also"></a>Confira também

- [Invocação de plataforma (P/Invoke)](pinvoke.md)
