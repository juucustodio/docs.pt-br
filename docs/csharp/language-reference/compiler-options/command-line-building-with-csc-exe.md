---
description: Build pela linha de comando com csc.exe
title: Build pela linha de comando com csc.exe
ms.date: 04/19/2017
helpviewer_keywords:
- builds [C#]
- command line [C#]
ms.assetid: 66e70056-dd20-453c-a9b3-507e0478b015
ms.openlocfilehash: 9ffd164602862fce7f5e4f0982d3eda7cb403e60
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89125924"
---
# <a name="command-line-build-with-cscexe"></a>Build pela linha de comando com csc.exe

Você pode invocar o compilador C# digitando o nome do seu arquivo executável (*csc.exe*) em um prompt de comando.

Se você usar a janela do **Prompt de Comando do Desenvolvedor do Visual Studio**, todas as variáveis de ambiente necessárias serão definidas para você. Para obter informações sobre como acessar essa ferramenta, consulte o tópico [Prompt de comando do desenvolvedor para o Visual Studio](../../../framework/tools/developer-command-prompt-for-vs.md).

Se você usar uma janela de prompt de comando padrão, deverá ajustar o caminho antes de poder invocar *csc.exe* de qualquer subdiretório no seu computador. Você também deve executar *VsDevCmd.bat* para definir as variáveis de ambiente apropriadas para dar suporte a compilações de linha de comando. Para obter mais informações sobre *VsDevCmd.bat*, incluindo instruções sobre como encontrá-lo e executá-lo, consulte [como definir variáveis de ambiente para a linha de comando do Visual Studio](./how-to-set-environment-variables-for-the-visual-studio-command-line.md).

Se estiver trabalhando em um computador que tenha apenas o SDK (Software Development Kit) do Windows, você poderá usar o compilador do C# no **Prompt de Comando do SDK**, que é aberto na opção de menu **Microsoft .NET Framework SDK**.

Você também pode usar o MSBuild para compilar programas em C# programaticamente. Para mais informações, consulte [MSBuild](/visualstudio/msbuild/msbuild).

O arquivo executável *csc.exe* geralmente está localizado na pasta Microsoft. NET\Framework \\ *\<Version>* no diretório do *Windows* . O local pode variar dependendo da configuração exata de um computador específico. Se mais de uma versão do .NET Framework estiver instalada em seu computador, você encontrará várias versões desse arquivo. Para obter mais informações sobre essas instalações, consulte [Determinando qual versão do .NET Framework está instalada](../../../framework/migration-guide/how-to-determine-which-versions-are-installed.md).

> [!TIP]
> Quando você compila um projeto usando o IDE do Visual Studio, você pode exibir o comando **csc** e suas opções de compilador associadas na janela **Saída**. Para exibir essas informações, siga as instruções em [Como exibir, salvar e configurar arquivos de log de build](/visualstudio/ide/how-to-view-save-and-configure-build-log-files#to-change-the-amount-of-information-included-in-the-build-log), para alterar o nível de detalhes dos dados de log para **Normal** ou **Detalhado**. Depois de recompilar o projeto, pesquise na janela **Saída** por **csc** para localizar a invocação do compilador do C#.

 **Neste tópico**

- [Regras para sintaxe de linha de comando](#rules-for-command-line-syntax-for-the-c-compiler)

- [Linhas de comando de exemplo](#sample-command-lines-for-the-c-compiler)

- [Diferenças entre o compilador C# e a saída do compilador C++](#differences-between-c-compiler-and-c-compiler-output)

## <a name="rules-for-command-line-syntax-for-the-c-compiler"></a>Regras para sintaxe de linha de comando para o compilador do C#

O compilador do C# usa as seguintes regras para interpretar os argumentos fornecidos na linha de comando do sistema operacional:

- Os argumentos são delimitados por espaço em branco, que é um espaço ou uma tabulação.

- O caractere de acento circunflexo (^) não é reconhecido como um caractere de escape ou um delimitador. O caractere é tratado pelo analisador de linha de comando no sistema operacional antes de ser passado para a matriz `argv` no programa.

- Uma cadeia de caracteres entre aspas duplas ("cadeia de caracteres") é interpretada como um único argumento, independentemente do espaço em branco que está contido nela. Uma cadeia de caracteres entre aspas pode ser inserida em um argumento.

- Aspas duplas precedidas por uma barra invertida (\\") são interpretados como um caractere literal de aspas duplas (").

- As barras invertidas são interpretadas literalmente, a menos que precedam imediatamente as aspas duplas.

- Se um número par de barras invertidas for seguido por aspas duplas, uma barra invertida será colocada na matriz `argv` para cada par de barras invertidas e aspas duplas serão interpretadas como um delimitador de cadeia de caracteres.

- Se um número ímpar de barras invertidas for seguido por aspas duplas, uma barra invertida será colocada na matriz `argv` para cada par de barras invertidas e aspas duplas serão "escapadas" pela barra invertida restante. Isso fará com que aspas duplas (") literais sejam adicionadas na `argv`.

## <a name="sample-command-lines-for-the-c-compiler"></a>Linhas de comando de exemplo para o compilador do C#

- Compila o *File.cs* produzindo *File.exe*:

  ```console
  csc File.cs
  ```

- Compila o *File.cs* produzindo *File.dll*:

  ```console
  csc -target:library File.cs
  ```

- Compila *File.cs* e cria *My.exe*:

  ```console
  csc -out:My.exe File.cs
  ```

- Compila todos os arquivos do C# no diretório atual, com otimizações habilitadas e define o símbolo de DEPURAÇÃO. A saída é *File2.exe*:

  ```console
  csc -define:DEBUG -optimize -out:File2.exe *.cs
  ```

- Compila todos os arquivos C# no diretório atual, produzindo uma versão de depuração do *File2.dll*. Logotipos e avisos não são exibidos:

  ```console
  csc -target:library -out:File2.dll -warn:0 -nologo -debug *.cs
  ```

- Compila todos os arquivos C# no diretório atual para *algo. xyz* (uma dll):

  ```console
  csc -target:library -out:Something.xyz *.cs
  ```

## <a name="differences-between-c-compiler-and-c-compiler-output"></a>Diferenças entre as saídas dos compiladores do C# e do C++

Não há arquivos (*. obj*) de objeto criados como resultado da invocação do compilador C#; os arquivos de saída são criados diretamente. Como um resultado disso, o compilador do C# não precisa de um vinculador.

## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Opções do compilador de C# listadas em ordem alfabética](./listed-alphabetically.md)
- [Opções do compilador de C# listadas por categoria](./listed-by-category.md)
- [Argumentos Main () e Command-Line](../../programming-guide/main-and-command-args/index.md)
- [Argumentos de linha de comando](../../programming-guide/main-and-command-args/command-line-arguments.md)
- [Como exibir argumentos de linha de comando](../../programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)
- [Valores de retorno de Main()](../../programming-guide/main-and-command-args/main-return-values.md)
