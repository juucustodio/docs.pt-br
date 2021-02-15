---
title: Provedores de configuração no .NET
description: Saiba como a API do provedor de configuração é usada para configurar aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/04/2020
ms.openlocfilehash: 036eb403318200bc0ae1d93e2c7cf9d074cb0bfb
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97899443"
---
# <a name="configuration-providers-in-net"></a>Provedores de configuração no .NET

A configuração no .NET é possível com provedores de configuração. Há vários tipos de provedores que dependem de várias fontes de configuração. Este artigo fornece detalhes sobre todos os diferentes provedores de configuração e suas fontes correspondentes.

- [Provedor de configuração de arquivo](#file-configuration-provider)
- [Provedor de configuração de variável de ambiente](#environment-variable-configuration-provider)
- [Provedor de configuração de linha de comando](#command-line-configuration-provider)
- [Provedor de configuração de chave por arquivo](#key-per-file-configuration-provider)
- [Provedor de configuração de memória](#memory-configuration-provider)

## <a name="file-configuration-provider"></a>Provedor de configuração de arquivo

<xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> é a classe base para carregamento da configuração do sistema de arquivos. Os seguintes provedores de configuração derivam de `FileConfigurationProvider` :

- [Provedor de configuração JSON](#json-configuration-provider)
- [Provedor de configuração XML](#xml-configuration-provider)
- [Provedor de configuração INI](#ini-configuration-provider)

### <a name="json-configuration-provider"></a>Provedor de configuração JSON

A <xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider> classe carrega a configuração de um arquivo JSON. Instale o [`Microsoft.Extensions.Configuration.Json`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) pacote NuGet.

Sobrecargas podem especificar:

- Se o arquivo é opcional
- Se a configuração será recarregada se o arquivo for alterado

Considere o seguinte código:

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="1-39,43-44" highlight="23-29":::

O código anterior:

- Limpa todos os provedores de configuração existentes que foram adicionados por padrão no <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> método.
- Configura o provedor de configuração JSON para carregar o *appsettings.js* e  *appSettings*. `Environment` . arquivos *JSON* com as seguintes opções:
  - `optional: true`: O arquivo é opcional.
  - `reloadOnChange: true` : O arquivo é recarregado quando as alterações são salvas.

As configurações de JSON são substituídas pelas configurações no [provedor de configuração de variáveis de ambiente](#environment-variable-configuration-provider) e no provedor de configuração de linha de [comando](#command-line-configuration-provider).

Segue um exemplo *appsettings.jsno* arquivo com várias definições de configuração:

:::code language="json" source="snippets/configuration/console-json/appsettings.json":::

Na <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> instância, após a adição de provedores de configuração, você pode chamar <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder.Build?displayProperty=nameWithType> para obter o <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> objeto. A raiz de configuração representa a raiz de uma hierarquia de configuração. As seções da configuração podem ser associadas a instâncias de objetos .NET e, posteriormente, fornecidas como <xref:Microsoft.Extensions.Options.IOptions%601> por meio de injeção de dependência.

Considere o `TransientFaultHandlingOptions` tipo de registro definido da seguinte maneira:

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs":::

Para obter informações sobre tipos de registro, consulte [tipos de registro em C# 9](../../csharp/whats-new/csharp-9.md#record-types).

O código a seguir cria a raiz de configuração, associa uma seção ao `TransientFaultHandlingOptions` tipo de registro e imprime os valores associados na janela do console:

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="31-38":::

O aplicativo gravaria a seguinte saída de exemplo:

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="40-42":::

### <a name="xml-configuration-provider"></a>Provedor de configuração XML

A <xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider> classe carrega a configuração de um arquivo XML em tempo de execução. Instale o [`Microsoft.Extensions.Configuration.Xml`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml) pacote NuGet.

O código a seguir demonstra a configuração de arquivos XML usando o provedor de configuração XML.

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="1-34,52,58-59" highlight="23-34":::

O código anterior:

- Limpa todos os provedores de configuração existentes que foram adicionados por padrão no <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> método.
- Configura o provedor de configuração XML para carregar os arquivos de *appsettings.xml* e *repeating-example.xml* com as seguintes opções:
  - `optional: true`: O arquivo é opcional.
  - `reloadOnChange: true` : O arquivo é recarregado quando as alterações são salvas.
- Configura o provedor de configuração de variáveis de ambiente.
- Configura o provedor de configuração de linha de comando se os `args` argumentos Contains especificados.

As configurações de XML são substituídas pelas configurações no [provedor de configuração de variáveis de ambiente](#environment-variable-configuration-provider) e no provedor de configuração de linha de [comando](#command-line-configuration-provider).

Segue um exemplo *appsettings.xml* arquivo com várias definições de configuração:

:::code language="xml" source="snippets/configuration/console-xml/appsettings.xml":::

Elementos repetidos que usam o mesmo nome de elemento funcionarão se o atributo `name` for usado para diferenciar os elementos:

:::code language="xml" source="snippets/configuration/console-xml/repeating-example.xml":::

O código a seguir lê o arquivo de configuração anterior e exibe as chaves e valores:

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="36-51":::

O aplicativo gravaria a seguinte saída de exemplo:

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="53-57":::

É possível usar atributos para fornecer valores:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <key attribute="value" />
  <section>
    <key attribute="value" />
  </section>
</configuration>
```

O arquivo de configuração anterior carrega as seguintes chaves com `value`:

- `key:attribute`
- `section:key:attribute`

### <a name="ini-configuration-provider"></a>Provedor de configuração INI

A <xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider> classe carrega a configuração de um arquivo ini em tempo de execução. Instale o [`Microsoft.Extensions.Configuration.Ini`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)  pacote NuGet.

O código a seguir limpa todos os provedores de configuração e adiciona o `IniConfigurationProvider` com dois arquivos ini como a origem:

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="1-37,44-45" highlight="24-30":::

Segue um exemplo *appsettings.ini* arquivo com várias definições de configuração:

:::code language="ini" source="snippets/configuration/console-ini/appsettings.ini":::

O código a seguir exibe as definições de configuração anteriores, gravando-as na janela do console:

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="32-36":::

O aplicativo gravaria a seguinte saída de exemplo:

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="38-43":::

## <a name="environment-variable-configuration-provider"></a>Provedor de configuração de variável de ambiente

Usando a configuração padrão, o <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> carrega a configuração de pares chave-valor da variável de ambiente depois de ler *appsettings.jsem*, *appSettings.* `Environment` *. JSON* e o Gerenciador de segredo. Portanto, os valores de chave lidos dos valores de substituição de ambiente lidos de *appsettings.jsem*, *appSettings.* `Environment` *. JSON* e o Gerenciador de segredo.

O `:` separador não funciona com chaves hierárquicas de variáveis de ambiente em todas as plataformas. O sublinhado duplo ( `__` ) é substituído automaticamente por um `:` e tem suporte em todas as plataformas. Por exemplo, o `:` separador não tem suporte do [bash](https://linuxhint.com/bash-environment-variables), mas sim `__` .

Os seguintes `set` comandos:

- Defina as chaves de ambiente e os valores do exemplo anterior no Windows.
- Teste as configurações alterando-as de seus valores padrão. O `dotnet run` comando deve ser executado no diretório do projeto.

```dotnetcli
set SecretKey="Secret key from environment"
set TransientFaultHandlingOptions__Enabled="true"
set TransientFaultHandlingOptions__AutoRetryDelay="00:00:13"

dotnet run
```

As configurações de ambiente anteriores:

- São definidos apenas em processos iniciados na janela de comando em que foram definidos.
- Não serão lidos por aplicativos Web iniciados com o Visual Studio.

Os comandos [setx](/windows-server/administration/windows-commands/setx) a seguir podem ser usados para definir as chaves de ambiente e os valores no Windows. Ao contrário `set` de, `setx` as configurações são persistidas. `/M` define a variável no ambiente do sistema. Se a `/M` opção não for usada, uma variável de ambiente do usuário será definida.

```dotnetcli
setx SecretKey "Secret key from setx environment" /M
setx TransientFaultHandlingOptions__Enabled "true" /M
setx TransientFaultHandlingOptions__AutoRetryDelay "00:00:05" /M

dotnet run
```

Para testar se os comandos anteriores substituem *appsettings.js* e *appSettings.* `Environment` *. JSON*:

- Com o Visual Studio: saia e reinicie o Visual Studio.
- Com a CLI: iniciar uma nova janela de comando e Enter `dotnet run` .

Chame <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables%2A> com uma cadeia de caracteres para especificar um prefixo para variáveis de ambiente:

:::code language="csharp" source="snippets/configuration/console-env/Program.cs" highlight="21-22":::

No código anterior:

- `config.AddEnvironmentVariables(prefix: "CustomPrefix_")` é adicionado após os provedores de configuração padrão. Para obter um exemplo de como ordenar os provedores de configuração, consulte [provedor de configuração XML](#xml-configuration-provider).
- Variáveis de ambiente definidas com o `CustomPrefix_` prefixo substituem os provedores de configuração padrão. Isso inclui variáveis de ambiente sem o prefixo.

O prefixo é eliminado quando os pares chave-valor de configuração são lidos.

Os comandos a seguir testam o prefixo personalizado:

```dotnetcli
set CustomPrefix__SecretKey="Secret key with CustomPrefix_ environment"
set CustomPrefix__TransientFaultHandlingOptions__Enabled=true
set CustomPrefix__TransientFaultHandlingOptions__AutoRetryDelay=00:00:21

dotnet run
```

A configuração padrão carrega variáveis de ambiente e argumentos de linha de comando prefixados com `DOTNET_` . O `DOTNET_` prefixo é usado pelo .net para a configuração de [host](generic-host.md#host-configuration) e [aplicativo](generic-host.md#app-configuration), mas não para a configuração do usuário.

Para obter mais informações sobre a configuração de host e aplicativo, consulte [host genérico .net](generic-host.md).

Em [Azure app serviço](https://azure.microsoft.com/services/app-service), selecione **nova configuração de aplicativo** na página **configurações > configuração** . Azure App configurações do aplicativo de serviço são:

- Criptografado em repouso e transmitido por um canal criptografado.
- Exposto como variáveis de ambiente.

### <a name="connection-string-prefixes"></a>Prefixos de cadeia de conexão

A API de configuração tem regras de processamento especiais para quatro variáveis de ambiente de cadeia de conexão. Essas cadeias de conexão estão envolvidas na configuração de cadeias de conexão do Azure para o ambiente de aplicativo. As variáveis de ambiente com os prefixos mostrados na tabela são carregadas no aplicativo com a configuração padrão ou quando nenhum prefixo é fornecido para `AddEnvironmentVariables` .

| Prefixo da cadeia de conexão | Provedor                                                                |
|--------------------------|-------------------------------------------------------------------------|
| `CUSTOMCONNSTR_`         | Provedor personalizado                                                         |
| `MYSQLCONNSTR_`          | [MySQL](https://www.mysql.com)                                          |
| `SQLAZURECONNSTR_`       | [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database) |
| `SQLCONNSTR_`            | [SQL Server](https://www.microsoft.com/sql-server)                      |

Quando uma variável de ambiente for descoberta e carregada na configuração com qualquer um dos quatro prefixos mostrados na tabela:

- A chave de configuração é criada removendo o prefixo da variável de ambiente e adicionando uma seção de chave de configuração (`ConnectionStrings`).
- Um novo par chave-valor de configuração é criado para representar o provedor de conexão de banco de dados (exceto para `CUSTOMCONNSTR_`, que não tem um provedor indicado).

| Chave de variável de ambiente | Chave de configuração convertida | Entrada de configuração do provedor                                                    |
|--------------------------|-----------------------------|---------------------------------------------------------------------------------|
| `CUSTOMCONNSTR_{KEY}`    | `ConnectionStrings:{KEY}`   | Entrada de configuração não criada.                                                |
| `MYSQLCONNSTR_{KEY}`     | `ConnectionStrings:{KEY}`   | Chave: `ConnectionStrings:{KEY}_ProviderName`:<br>Valor: `MySql.Data.MySqlClient` |
| `SQLAZURECONNSTR_{KEY}`  | `ConnectionStrings:{KEY}`   | Chave: `ConnectionStrings:{KEY}_ProviderName`:<br>Valor: `System.Data.SqlClient`  |
| `SQLCONNSTR_{KEY}`       | `ConnectionStrings:{KEY}`   | Chave: `ConnectionStrings:{KEY}_ProviderName`:<br>Valor: `System.Data.SqlClient`  |

### <a name="environment-variables-set-in-launchsettingsjson"></a>Variáveis de ambiente definidas no launchSettings.jsem

As variáveis de ambiente definidas no *launchSettings.js* substituir aquelas definidas no ambiente do sistema.

## <a name="command-line-configuration-provider"></a>Provedor de configuração de linha de comando

Usando a configuração padrão, o <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> carrega a configuração de pares de chave-valor de argumento de linha de comando após as seguintes fontes de configuração:

- *appsettings.js* e *appSettings*. `Environment` . arquivos *JSON* .
- Segredos do aplicativo (Gerenciador de segredo) no `Development` ambiente.
- Variáveis de ambiente.

Por padrão, os valores de configuração definidos na linha de comando substituem os valores de configuração definidos por todos os outros provedores de configuração.

### <a name="command-line-arguments"></a>Argumentos de linha de comando

O comando a seguir define chaves e valores usando `=` :

```dotnetcli
dotnet run SecretKey="Secret key from command line"
```

O comando a seguir define chaves e valores usando `/` :

```dotnetcli
dotnet run /SecretKey "Secret key set from forward slash"
```

O comando a seguir define chaves e valores usando `--` :

```dotnetcli
dotnet run --SecretKey "Secret key set from double hyphen"
```

O valor da chave:

- Deve seguir `=` , ou a chave deve ter um prefixo `--` ou `/` quando o valor segue um espaço.
- Não será necessário se `=` for usado. Por exemplo, `SomeKey=`.

No mesmo comando, não misture pares de chave-valor de argumento de linha de comando que usam `=` com pares de chave-valor que usam um espaço.

## <a name="key-per-file-configuration-provider"></a>Provedor de configuração de chave por arquivo

O <xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider> usa arquivos do diretório como pares chave-valor de configuração. A chave é o nome do arquivo. O valor é o conteúdo do arquivo. O provedor de configuração de chave por arquivo é usado em cenários de hospedagem do Docker.

Para ativar a configuração de chave por arquivo, chame o método de extensão <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile%2A> em uma instância do <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>. O `directoryPath` para os arquivos deve ser um caminho absoluto.

As sobrecargas permitem especificar:

- Um delegado `Action<KeyPerFileConfigurationSource>` que configura a origem.
- Se o diretório é opcional, e o caminho para o diretório.

O sublinhado duplo (`__`) é usado como um delimitador de chave de configuração em nomes de arquivo. Por exemplo, o nome do arquivo `Logging__LogLevel__System` produz a chave de configuração `Logging:LogLevel:System`.

Chame `ConfigureAppConfiguration` ao criar o host para especificar a configuração do aplicativo:

```csharp
.ConfigureAppConfiguration((_, configuration) =>
{
    var path = Path.Combine(
        Directory.GetCurrentDirectory(), "path/to/files");

    configuration.AddKeyPerFile(directoryPath: path, optional: true);
})
```

## <a name="memory-configuration-provider"></a>Provedor de configuração de memória

O <xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider> usa uma coleção na memória como pares chave-valor de configuração.

O código a seguir adiciona uma coleção de memória ao sistema de configuração:

:::code language="csharp" source="snippets/configuration/console-memory/Program.cs" highlight="22-29":::

No código anterior, <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection(Microsoft.Extensions.Configuration.IConfigurationBuilder,System.Collections.Generic.IEnumerable{System.Collections.Generic.KeyValuePair{System.String,System.String}})?displayProperty=nameWithType> adiciona o provedor de memória após os provedores de configuração padrão. Para obter um exemplo de como ordenar os provedores de configuração, consulte [provedor de configuração XML](#xml-configuration-provider).

## <a name="see-also"></a>Veja também

- [Configuração no .NET](configuration.md)
- [Host Genérico .NET](generic-host.md)
- [Implementar um provedor de configuração personalizado](custom-configuration-provider.md)
