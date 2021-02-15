---
title: Migrando do DNX para a CLI do .NET Core
description: Migre para mudar do uso de ferramentas de DNX para ferramentas da CLI do .NET Core.
ms.date: 06/20/2016
ms.openlocfilehash: e5ebbab2551cf750a5b1136e7b1d4b67816c3b03
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91071112"
---
# <a name="migrating-from-dnx-to-net-core-cli-projectjson"></a>Migrando do DNX para a CLI do .NET Core (project.json)

## <a name="overview"></a>Visão geral

A versão RC1 do .NET Core e ASP.NET Core 1.0 introduziu ferramentas DNX. A versão RC2 do .NET Core e ASP.NET Core 1.0 mudou do DNX para a CLI do .NET Core.

Como um ligeiro lembrete, vamos recapitular o que foi o DNX. O DNX era um runtime e um conjunto de ferramentas usado para criar aplicativos do .NET Core e, mais especificamente, do ASP.NET Core 1.0. Ele era composto por 3 partes principais:

1. DNVM – um script de instalação para obter o DNX
2. DNX (Dotnet Execution Runtime) – o tempo de execução que executa o código
3. DNU (Dotnet Developer Utility) – ferramentas para gerenciar dependências, criar e publicar seus aplicativos

Com a introdução da CLI, todos os itens acima agora fazem parte de um único conjunto de ferramentas. No entanto, como o DNX estava disponível na época do RC1, você poderá ter projetos que foram criados usando com ele, os quais terão que ser movidos para as novas ferramentas da CLI.

Este guia de migração abordará os princípios básicos de como migrar projetos do DNX para a CLI do .NET Core. Se você estiver começando um projeto no .NET Core do zero, poderá ignorar totalmente este documento.

## <a name="main-changes-in-the-tooling"></a>Principais mudanças nas ferramentas

Há algumas das mudanças gerais nas ferramentas que devem ser descritas primeiro.

### <a name="no-more-dnvm"></a>Não há mais DNVM

DNVM, abreviação de *DotNet Version Manager* foi um script do bash/PowerShell usado para instalar um DNX em seu computador. Ele ajudou os usuários a obter o DNX necessário do feed especificado (ou padrão), bem como marcar um determinado DNX como "ativo", que o colocaria no $PATH de determinada sessão. Isso permitiria que você usasse as várias ferramentas.

DNVM foi descontinuado porque seu conjunto de recursos foi tornado redundante por alterações recebidas na CLI do .NET Core.

A CLI vem empacotada de duas maneiras principais:

1. Instaladores nativos para uma determinada plataforma
2. Instalam o script em outras situações (como servidores CI)

Devido a isso, os recursos de instalação do DNVM não são necessários. Mas e quanto aos recursos de seleção de runtime?

Um runtime é referenciado em seu `project.json` adicionando um pacote de uma determinada versão às suas dependências. Com essa alteração, seu aplicativo poderá usar os novos bits de runtime. Levar esses bits para seu computador é o mesmo que na CLI: você instala o runtime por meio de um dos instaladores nativos com suporte ou por meio do script de instalação.

### <a name="different-commands"></a>Comandos diferentes

Se você estivesse usando o DNX, teria usado comandos de uma das suas três partes (DNX, DNU ou DNVM). Com a CLI, alguns desses comandos mudaram, outros não estão disponíveis e outros ainda permaneceram os mesmos, mas têm semântica ligeiramente diferente.

A tabela a seguir mostra o mapeamento entre os comandos DNX/DNU e seus equivalentes da CLI.

| Comando do DNX                    | Comando da CLI    | Descrição                                                                                                     |
|--------------------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| dnx run                        | `dotnet run`     | Execute o código da origem.                                                                                           |
| dnu build                      | `dotnet build`   | Crie um binário IL do seu código.                                                                                |
| dnu pack                       | `dotnet pack`    | Empacote um pacote NuGet do seu código.                                                                        |
| dnx \[comando] (por exemplo, "dnx web") | N/D\*          | No mundo DNX, execute um comando conforme definido no project.json.                                                     |
| dnu install                    | N/D\*          | No mundo DNX, instale um pacote como uma dependência.                                                            |
| dnu restore                    | `dotnet restore` | Restaure as dependências especificadas no seu project.json. ([consulte a observação](#dotnet-restore-note))                                                            |
| dnu publish                    | `dotnet publish` | Publica seu aplicativo para implantação em uma das três formas (portátil, portátil com nativo e autônomo). |
| dnu wrap                       | N/D\*          | No mundo DNX, encapsule um project.json em csproj.                                                                    |
| dnu commands                   | N/D\*          | No mundo DNX, gerencie os comandos instalados globalmente.                                                           |

(\*) – esses recursos não têm suporte na CLI por padrão.

## <a name="dnx-features-that-are-not-supported"></a>Recursos DNX sem suporte

Como mostrado na tabela acima, há recursos do mundo DNX aos quais decidimos não dar suporte na CLI, pelo menos por enquanto. Esta seção abordará os mais importantes deles e descreverá os motivos para não dar suporte a eles, bem como soluções alternativas caso você precise deles.

### <a name="global-commands"></a>Comandos globais

O DNU vinha com um conceito chamado "comandos globais". Eles eram, essencialmente, aplicativos de console empacotados como NuGet com um script de shell que invocaria o DNX especificado para executar o aplicativo.

A CLI não dá suporte a esse conceito. Contudo, ela dá suporte ao conceito de adição de comandos por projeto, os quais podem ser invocados usando a sintaxe familiar do `dotnet <command>`.

### <a name="installing-dependencies"></a>Instalar dependências

A partir de v1, o CLI do .NET Core não tem um `install` comando para instalar dependências. Para instalar um pacote NuGet, você precisará adicioná-lo como uma dependência ao arquivo `project.json` e, em seguida, executar `dotnet restore` ([veja observação](#dotnet-restore-note)).

### <a name="running-your-code"></a>Como executar código

Há duas maneiras principais de executar o código. Uma delas é da origem, com `dotnet run`. Diferente do `dnx run`, isso não gerará nenhuma compilação na memória. Na verdade, isso invocará `dotnet build` para compilar seu código e executar o binário compilado.

Outra maneira é usar o `dotnet` para executar seu código. Isso é feito fornecendo um caminho para o assembly: `dotnet path/to/an/assembly.dll`.

## <a name="migrating-your-dnx-project-to-net-core-cli"></a>Migrando seu projeto DNX para a CLI do .NET Core

Além de usar os novos comandos ao trabalhar com seu código, há três coisas principais que ainda faltam para migrar do DNX:

1. Migrar o arquivo `global.json` se você quiser que ele possa usar a CLI.
2. Migrar o próprio arquivo de projeto (`project.json`) para as ferramentas da CLI.
3. Migrar as APIs DNX para seus equivalentes de BCL.

### <a name="changing-the-globaljson-file"></a>Alterar o arquivo global.json

O arquivo `global.json` funciona como um arquivo de solução para projetos RC1 e RC2 (ou posterior). Para que o CLI do .NET Core (bem como o Visual Studio) Diferencie entre o RC1 e versões posteriores, eles usam a `"sdk": { "version" }` propriedade para fazer a distinção de qual projeto é RC1 ou posterior. Se `global.json` não tiver esse nó, ele será considerado o mais recente.

Para atualizar o arquivo `global.json`, remova a propriedade ou defina-a para a versão exata das ferramentas que você deseja usar, neste caso **1.0.0-preview2-003121**:

```json
{
    "sdk": {
        "version": "1.0.0-preview2-003121"
    }
}
```

### <a name="migrating-the-project-file"></a>Migrando o arquivo de projeto

A CLI e o DNX usam o mesmo sistema de projeto básico com base no arquivo `project.json`. A sintaxe e a semântica do arquivo de projeto são praticamente as mesmas, com pequenas diferenças dependendo dos cenários. Também há algumas alterações no esquema que podem ser vistas no [arquivo de esquema](http://json.schemastore.org/project).

Se você estiver criando um aplicativo de console, precisará adicionar o snippet a seguir ao arquivo de projeto:

```json
"buildOptions": {
    "emitEntryPoint": true
}
```

Isso instrui o `dotnet build` a emitir um ponto de entrada para seu aplicativo, tornando o código efetivamente executável. Se você estiver criando uma biblioteca de classes, basta omita a seção acima. É claro que, uma vez adicionado o snippet acima ao `project.json` arquivo, você precisa adicionar um ponto de entrada estático. Ao deixar de usar o DNX, os serviços de DI fornecidos por ele não estão mais disponíveis e, portanto, esse deve ser um ponto de entrada .NET básico: `static void Main()`.

Se você tiver uma seção "commands" em seu `project.json`, poderá removê-la. Alguns dos comandos que existiam como comandos DNU, como comandos da CLI do Entity Framework, estão sendo portados para extensões por projeto para a CLI. Se você compilou seus próprios comandos que estão sendo usados em seus projetos, será necessário substituí-los por extensões CLI. Nesse caso, o nó `commands` em `project.json` precisa ser substituído pelo nó `tools` e ele precisa listar as dependências de ferramentas.

Depois de concluir essas coisas, você precisará decidir qual tipo de portabilidade deseja para seu aplicativo. Com o .NET Core, investimos em fornecer uma variedade de opções de portabilidade à sua escolha. Por exemplo, você pode escolher um aplicativo totalmente *portátil* ou *autocontido*. A opção de aplicativo portátil parece-se com a maneira como os aplicativos do .NET Framework funcionam: ele precisa de um componente compartilhado para executá-lo no computador de destino (.NET Core). O aplicativo autocontido não requer que o .NET Core seja instalado no destino, mas você deve produzir um aplicativo para cada sistema operacional ao qual você deseja dar suporte. Esses tipos de portabilidade e muito mais é discutido no documento [tipo de portabilidade do aplicativo](../deploying/index.md).

Depois de escolher qual tipo de portabilidade você deseja, será necessário alterar as estruturas de destino. Se estivesse criando aplicativos para .NET Core, você provavelmente usaria `dnxcore50` como sua estrutura de destino. Com a CLI e as mudanças resultantes do novo [.NET Standard](../../standard/net-standard.md), a estrutura deve ser uma das seguintes:

1. `netcoreapp1.0` – Se você estiver criando aplicativos no .NET Core (incluindo aplicativos ASP.NET Core)
2. `netstandard1.6` – Se você estiver criando bibliotecas de classes para .NET Core

Se você estiver usando outros destinos `dnx` como o `dnx451`, será necessário alterá-los também. `dnx451` deve ser alterado para `net451`.
Consulte o tópico [.NET Standard](../../standard/net-standard.md) para saber mais.

Seu `project.json` agora está quase pronto. Você precisa examinar a lista de dependências e atualizá-las para suas versões mais recentes, especialmente se estiver usando dependências ASP.NET Core. Se estiver usando pacotes separados para as APIs BCL, poderá usar o pacote de runtime, conforme explicado no documento [tipo de portabilidade do aplicativo](../deploying/index.md).

Quando estiver pronto, tente fazer a restauração com `dotnet restore` ([veja observação](#dotnet-restore-note)). Dependendo da versão das suas dependências, você poderá encontrar erros se o NuGet não puder resolvê-las para um das estruturas de destino acima. Este é um problema “pontual”, pois à medida que o tempo passa, cada vez mais pacotes incluirão suporte a essas estruturas. Por enquanto, se você enfrentar isso, poderá usar a instrução `imports` dentro do nó `framework` para especificar para o NuGet que ele pode restaurar os pacotes direcionando a estrutura dentro da instrução "imports".
Os erros de restauração obtidos nesse caso devem fornecer informações suficientes para indicar quais estruturas você precisa importar. Se você ficar um pouco confuso ou não tiver experiência nisso, especificar `dnxcore50` e `portable-net45+win8` na instrução `imports` geralmente é suficiente. O snippet JSON a seguir mostra como isso se parece:

```json
    "frameworks": {
        "netcoreapp1.0": {
            "imports": ["dnxcore50", "portable-net45+win8"]
        }
    }
```

Executar `dotnet build` mostrará os eventuais erros de build, porém não deve haver muitos. Depois de o código ser criado e executado corretamente, você poderá testá-lo com o executor. Execute `dotnet <path-to-your-assembly>` e observe a execução.

<a name="dotnet-restore-note"></a>

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]
