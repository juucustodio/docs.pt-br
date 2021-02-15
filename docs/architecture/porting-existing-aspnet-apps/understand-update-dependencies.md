---
title: Entender e atualizar dependências
description: Para migrar um projeto .NET Framework para o .NET Core, suas dependências devem ser atualizadas para funcionar com o .NET Core. Esta seção examina as ferramentas e abordagens que podem ser usadas para planejar migrações para aplicativos grandes.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: fa789153ac23bf682a6e4d69234782f31059e56b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488429"
---
# <a name="understand-and-update-dependencies"></a>Entender e atualizar dependências

Depois de identificar a sequência na qual os projetos individuais do aplicativo devem ser migrados, a próxima etapa é entender as dependências de cada projeto e atualizá-las, se necessário. Para as dependências de plataforma, a melhor maneira de começar é executar o [analisador de portabilidade do .net](https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer) no assembly em questão e, em seguida, examinar os resultados detalhados gerados. Você configura a ferramenta para especificar uma ou mais plataformas de destino, como .NET Core 3,1 ou .NET Standard 2,0. Os resultados são fornecidos com detalhes para cada plataforma de destino. A Figura 3-4 mostra um exemplo da saída da ferramenta.

![Detalhes do relatório do analisador de portabilidade .NET](./media/Figure3-4.png)

**Figura 3-4.** Detalhes do relatório do .NET Portability Analyzer.

## <a name="update-class-library-dependencies"></a>Atualizar dependências da biblioteca de classes

Aplicativos grandes normalmente envolvem vários projetos, e a maioria dos projetos que não sejam o projeto Web ASP.NET MVC provavelmente são bibliotecas de classes. As bibliotecas de classes tendem a ser a porta mais fácil entre as plataformas .NET, especialmente em comparação com os projetos ASP.NET, que estão entre os mais difíceis (e normalmente precisam ser recriadas).

As equipes podem considerar a [ferramenta tentar-converter](https://github.com/dotnet/try-convert) para migrar bibliotecas de classes para o .NET Core. A ferramenta tentar-converter analisa um arquivo de projeto .NET Framework e tenta migrá-lo para o formato de arquivo de projeto do .NET Core, fazendo quaisquer modificações que possam ser executadas com segurança no processo. Essa ferramenta não funcionará em um projeto ASP.NET, mas pode ajudar a acelerar o processo de migração de bibliotecas de classes.

A ferramenta tentar-converter é implantada como uma ferramenta de linha de comando do .NET Core. Ele só é executado no Windows, já que foi projetado para trabalhar com .NET Framework aplicativos. Você pode instalá-lo executando o seguinte comando em um prompt de comando:

```dotnetcli
dotnet tool install -g try-convert
```

Depois de instalar a ferramenta com êxito, você pode executar `try-convert` na pasta em que o arquivo de projeto da biblioteca de classes está localizado.

## <a name="update-nuget-package-dependencies"></a>Atualizar dependências do pacote NuGet

Analise o uso de pacotes NuGet de terceiros e determine se algum deles ainda não oferece suporte a .NET Standard (ou dê suporte a ele, mas apenas com uma nova versão). Pode ser útil atualizar os [pacotes NuGet para usar a `<PackageReference>` sintaxe usando a ferramenta de conversão do Visual Studio](https://docs.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference), para que as dependências de nível superior fiquem visíveis. Em seguida, verifique se as versões atuais ou posteriores desses pacotes dão suporte ao .NET Core ou .NET Standard. Essas informações podem ser encontradas em [nuget.org] ou no Visual Studio para cada pacote.

Se o suporte existir usando a versão do pacote que o aplicativo usa atualmente, ótimo! Caso contrário, veja se uma versão mais recente do pacote tem o suporte e a pesquisa o que estaria envolvido na atualização. Pode haver alterações significativas no pacote, especialmente se a versão principal do pacote for alterada entre a versão atualmente usada e a que você estiver atualizando.

Em alguns casos, nenhuma versão de um determinado pacote funciona com o .NET Core. Nesse caso, as equipes têm duas opções. Eles podem continuar dependendo da versão do .NET Framework, mas isso tem limitações. O aplicativo só será executado no Windows, e a equipe poderá querer executar o analisador de portabilidade nos binários do pacote para ver se há problemas que possam ser encontrados. Certamente, a equipe desejará testar exaustivamente. A outra opção é localizar um pacote diferente ou, se o pacote necessário for de software livre, atualizá-lo para o .NET Standard ou o próprio .NET Core.

## <a name="migrate-aspnet-mvc-projects"></a>Migrar projetos MVC do ASP.NET

O `System.Web` namespace e os tipos não existem no .NET Core. Quando estiver analisando dependências e usando ferramentas como `try-convert` , você descobrirá que elas não oferecem muitas sugestões para a migração automática de projetos do ASP.NET MVC e qualquer código que faça referência a ele `System.Web` . Para esses projetos, você precisará começar com um novo projeto Web ASP.NET Core e migrar os arquivos manualmente para este projeto.

Em geral, é uma boa prática minimizar o quanto da lógica de negócios de um aplicativo reside em sua camada de interface do usuário. Também é melhor manter os controladores e as exibições pequenas. Os aplicativos que seguiram essas diretrizes serão mais fáceis de porta do que aqueles que têm uma quantidade significativa de lógica no projeto Web ASP.NET. Se você tiver um aplicativo que está considerando portabilidade, mas ainda não tiver iniciado o processo, lembre-se disso ao mantê-lo. Qualquer esforço que você colocar para minimizar a quantidade de código no ASP.NET MVC ou no projeto de API da Web provavelmente resultará em menos trabalho quando o tempo chegar à porta do aplicativo.

O próximo capítulo se aprofunda em detalhes de como migrar de projetos do ASP.NET MVC e da API Web para projetos ASP.NET Core. O capítulo anterior chamou as maiores diferenças entre os aplicativos. Depois que a estrutura básica do projeto estiver em vigor, migrar os controladores e as exibições individuais geralmente é simples, especialmente se elas estiverem concentradas principalmente em responsabilidades da Web.

## <a name="references"></a>Referências

- [ferramenta try – Convert](https://github.com/dotnet/try-convert)
- [ferramenta apiport](https://github.com/microsoft/dotnet-apiport)

>[!div class="step-by-step"]
>[Anterior](identify-migration-sequence.md) 
> [Avançar](strategies-migrating-in-production.md)
