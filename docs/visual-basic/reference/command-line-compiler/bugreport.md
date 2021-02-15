---
description: Saiba mais sobre:-bugreport
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 45831073121991774e462bce26040c575e0a0dc2
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100468207"
---
# <a name="-bugreport"></a>-bugreport

Cria um arquivo que você pode usar ao arquivar um relatório de bug.

## <a name="syntax"></a>Sintaxe

```console
-bugreport:file
```

## <a name="arguments"></a>Argumentos

|Termo|Definição|
|---|---|
|`file`|Obrigatório. O nome do arquivo que conterá seu relatório de bugs. Coloque o nome do arquivo entre aspas ("") se o nome contiver um espaço.|

## <a name="remarks"></a>Comentários

As informações a seguir são adicionadas a `file` :

- Uma cópia de todos os arquivos de código-fonte na compilação.

- Uma lista das opções de compilador usadas na compilação.

- Informações de versão sobre seu compilador, Common Language Runtime e sistema operacional.

- Saída do compilador, se houver.

- Uma descrição do problema, para o qual você será solicitado.

- Uma descrição de como você acredita que o problema deve ser corrigido, para o qual você será solicitado.

Como uma cópia de todos os arquivos de código-fonte está incluída no `file` , talvez você queira reproduzir o defeito do código (suspeito) no programa mais curto possível.

> [!IMPORTANT]
> A `-bugreport` opção produz um arquivo que contém informações potencialmente confidenciais. Isso inclui a hora atual, a versão do compilador, a versão .NET Framework, a versão do sistema operacional, o nome de usuário, os argumentos de linha de comando com os quais o compilador foi executado, todo o código-fonte e a forma binária de qualquer assembly referenciado. Essa opção pode ser acessada especificando-se opções de linha de comando no arquivo Web.config para uma compilação no lado do servidor de um aplicativo ASP.NET. Para evitar isso, modifique o arquivo de Machine.config para impedir que os usuários sejam compilados no servidor.

Se essa opção for usada com `-errorreport:prompt` , `-errorreport:queue` ou `-errorreport:send` , e seu aplicativo encontrar um erro de compilador interno, as informações em `file` serão enviadas para a Microsoft Corporation. Essas informações ajudarão os engenheiros da Microsoft a identificar a causa do erro e poderão ajudar a melhorar a próxima versão do Visual Basic. Por padrão, nenhuma informação é enviada à Microsoft. No entanto, quando você compila um aplicativo usando o `-errorreport:queue` , que é habilitado por padrão, o aplicativo coleta seus relatórios de erros. Em seguida, quando o administrador do computador fizer logon, o sistema de relatórios de erros exibirá uma janela pop-up que permite ao administrador encaminhar à Microsoft quaisquer relatórios de erros ocorridos desde o logon.

> [!NOTE]
> A `-bugreport` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente quando você compila a partir da linha de comando.

## <a name="example"></a>Exemplo

O exemplo a seguir compila *T2. vb* e coloca todas as informações de relatório de bugs no arquivo *Problem.txt*.

```console
vbc -bugreport:problem.txt t2.vb
```

## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [-debug (Visual Basic)](debug.md)
- [-errorreport](errorreport.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
- [Elemento trustLevel para securityPolicy (esquema de configurações do ASP.NET)](/previous-versions/dotnet/netframework-4.0/as399f0x(v=vs.100))
