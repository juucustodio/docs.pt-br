---
title: Invocação de plataforma (P/Invoke)
description: Saiba como chamar funções nativas via P/Invoke no .NET.
ms.date: 01/18/2019
ms.openlocfilehash: cde52d9d0a4e3b84fec632b615b635e7b7df3924
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678264"
---
# <a name="platform-invoke-pinvoke"></a>Invocação de plataforma (P/Invoke)

P/Invoke é uma tecnologia que permite acessar structs, retornos de chamada e funções em bibliotecas não gerenciadas de um código gerenciado. A maior parte da API do P/Invoke está contida em dois namespaces: `System` e `System.Runtime.InteropServices`. O uso desses dois namespaces fornece as ferramentas que descrevem como você deseja se comunicar com o componente nativo.

Vamos começar com exemplo mais comum, que é chamar funções não gerenciadas no seu código gerenciado. Vamos mostrar uma caixa de mensagem de um aplicativo de linha de comando:

[!code-csharp[MessageBox](~/samples/snippets/standard/interop/pinvoke/messagebox.cs)]

O exemplo anterior é simples, mas mostra o que é necessário para invocar funções não gerenciadas de um código gerenciado. Vamos analisar o exemplo:

- A linha #2 mostra a instrução using para o `System.Runtime.InteropServices` namespace que contém todos os itens necessários.
- A linha #8 apresenta o `DllImport` atributo. Esse atributo é crucial, pois informa ao runtime que deve carregar a DLL não gerenciada. A cadeia de caracteres passada é a DLL na qual nossa função de destino está incluída. Além disso, especifica qual [conjunto de caracteres](./charset.md) deve ser usado para realizar marshaling de cadeias de caracteres. Por fim, especifica que essa função chama [SetLastError](/windows/desktop/api/errhandlingapi/nf-errhandlingapi-setlasterror) e que o runtime deve capturar esse código de erro para que o usuário possa recuperá-lo via <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error?displayProperty=nameWithType>.
- A linha #9 é a crux do trabalho P/Invoke. Define um método gerenciado que tem **exatamente a mesma assinatura** que o não gerenciado. A declaração tem uma nova palavra-chave que você pode observar, `extern`, que informa ao runtime que é um método externo; quando invocado, o runtime deve encontrá-la na DLL especificada no atributo `DllImport`.

O restante do exemplo é simplesmente chamar o método como você faria com qualquer outro método gerenciado.

A amostra é semelhante para macOS. O nome da biblioteca deve ser alterado no atributo `DllImport`, pois o macOS tem um esquema diferente de nomenclatura para bibliotecas dinâmicas. O exemplo a seguir usa a função `getpid(2)` para obter a ID do processo do aplicativo e imprimi-la para o console:

[!code-csharp[getpid macOS](~/samples/snippets/standard/interop/pinvoke/getpid-macos.cs)]

Também é semelhante no Linux. O nome da função é o mesmo, já que `getpid(2)` é uma chamada do sistema [POSIX](https://en.wikipedia.org/wiki/POSIX) padrão.

[!code-csharp[getpid Linux](~/samples/snippets/standard/interop/pinvoke/getpid-linux.cs)]

## <a name="invoking-managed-code-from-unmanaged-code"></a>Chamando código gerenciado do código não gerenciado

O runtime viabiliza o fluxo da comunicação nas duas direções, o que permite retornar a chamada no código gerenciado das funções nativas usando ponteiros de função. A coisa mais próxima a um ponteiro de função no código gerenciado é um **delegado**; portanto, isso é usado para permitir retornos de chamada do código nativo para o código gerenciado.

A maneira de usar esse recurso é semelhante ao processo gerenciado para nativo, conforme descrito anteriormente. Para um retorno de chamada específico, você define um delegado que corresponda à assinatura e o passa para o método externo. O runtime cuidará do resto.

[!code-csharp[EnumWindows](~/samples/snippets/standard/interop/pinvoke/enumwindows.cs)]

Antes de analisar o exemplo, é uma boa ideia examinar as assinaturas das funções não gerenciadas com as quais você precisa trabalhar. A função a ser chamada para enumerar todas as janelas tem esta assinatura: `BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`

O primeiro parâmetro é um retorno de chamada. Esse retorno de chamada tem a seguinte assinatura: `BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`

Agora, vamos analisar o exemplo:

- A linha 9 no exemplo define um delegado que corresponde à assinatura do retorno de chamada do código não gerenciado. Observe como os tipos LPARAM e HWND são representados usando `IntPtr` no código gerenciado.
- As linhas 13 e 14 introduzem a função `EnumWindows` da biblioteca user32.dll.
- As linhas de 17 a 20 implementam o delegado. Neste exemplo simples, queremos apenas produzir o identificador para o console.
- Por fim, na linha 24, chamamos o método externo e passamos o delegado.

Os exemplos de Linux e macOS são mostrados abaixo. Para eles, usamos a função `ftw` que pode ser encontrada em `libc`, a biblioteca C. Essa função é usada para percorrer as hierarquias de diretório e leva um ponteiro para uma função como um dos seus parâmetros. Essa função tem a seguinte assinatura: `int (*fn) (const char *fpath, const struct stat *sb, int typeflag)`.

[!code-csharp[ftw Linux](~/samples/snippets/standard/interop/pinvoke/ftw-linux.cs)]

O exemplo do macOS usa a mesma função; a única diferença é o argumento para o atributo `DllImport`, pois o macOS mantém `libc` em um local diferente.

[!code-csharp[ftw macOS](~/samples/snippets/standard/interop/pinvoke/ftw-macos.cs)]

Os exemplos anteriores dependem de parâmetros e, em ambos os casos, os parâmetros são fornecidos como tipos gerenciados. O runtime faz a "coisa certa" e processa esses parâmetros em seus equivalentes no outro lado. Saiba mais sobre é realizado o marshaling de tipos para código nativo em nossa página sobre [Marshaling de tipo](type-marshaling.md).

## <a name="more-resources"></a>Mais recursos

- [Wiki do PInvoke.net](https://www.pinvoke.net/) uma wiki excelente com informações sobre as APIs comuns do Windows e como chamá-las.
- [P/Invoke em C++/CLI](/cpp/dotnet/native-and-dotnet-interoperability)
- [Documentação do Mono no P/Invoke](https://www.mono-project.com/docs/advanced/pinvoke/)
