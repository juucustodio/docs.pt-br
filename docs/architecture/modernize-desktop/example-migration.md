---
title: Exemplo de migração para o .NET 5
description: Mostrando como migrar um aplicativo de exemplo destinado a .NET Framework para o .NET 5.
ms.date: 01/19/2021
ms.openlocfilehash: f924f90046fdcd7dfe5e23740fc921a09383a81a
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98618000"
---
# <a name="example-of-migrating-to-net"></a>Exemplo de migração para o .NET

Neste capítulo, apresentamos diretrizes práticas para ajudá-lo a realizar uma migração de seu aplicativo existente do .NET Framework para o .NET.

Apresentamos um processo bem estruturado que você pode seguir e as coisas mais importantes a serem consideradas em cada etapa.

Em seguida, documentamos um processo de migração passo a passo para um aplicativo de desktop de exemplo, tanto de WinForms quanto de versões do WPF.

## <a name="migration-process-overview"></a>Visão geral do processo de migração

O processo de migração consiste em quatro etapas sequenciais:

1. **Preparação**: entenda as dependências que o projeto tem para ter uma ideia do que está em frente. Nesta etapa, você pega o projeto atual em um estado que simplifica o ponto de inicialização para a migração.

2. **Migrar arquivo de projeto:** os projetos .NET usam o novo formato de projeto no estilo SDK. Crie um novo arquivo de projeto com esse formato ou atualize o que você precisa para usar o estilo SDK.

3. **Corrigir código e compilar:** Compile o código no .NET que aborda as diferenças de nível de API entre .NET Framework e .NET. Se necessário, atualize pacotes de terceiros para aqueles que dão suporte ao .NET.

4. **Executar e testar:** Pode haver diferenças que não aparecem até o tempo de execução. Portanto, não se esqueça de executar o aplicativo e testar se tudo funciona conforme o esperado.

### <a name="preparation"></a>Preparação

#### <a name="migrate-packagesconfig-file"></a>Migrar arquivo de packages.config

Em um aplicativo .NET Framework, todas as referências a pacotes externos são declaradas no arquivo *packages.config* . No .NET, não há mais a necessidade de usar o arquivo *packages.config* . Em vez disso, use a propriedade [PackageReference](../../core/project-sdk/msbuild-props.md#packagereference) dentro do arquivo de projeto para especificar os pacotes NuGet para seu aplicativo.

Portanto, você precisa fazer a transição de um formato para outro. Você pode fazer a atualização manualmente, levando as dependências contidas no arquivo de *packages.config* e migrando-as para o arquivo de projeto com o `PackageReference` formato. Ou, você pode deixar o Visual Studio fazer o trabalho para você: clique com o botão direito do mouse no arquivo *packages.config* e selecione a opção **migrar packages.config para PackageReference** .

#### <a name="verify-every-dependency-compatibility-in-net"></a>Verificar cada compatibilidade de dependência no .NET

Depois de migrar as referências de pacote, você deve verificar a compatibilidade de cada referência. Você pode explorar as dependências de cada pacote NuGet que seu aplicativo está usando no [NuGet.org](https://www.nuget.org/). Se o pacote tiver dependências .NET Standard, ele vai funcionar no .NET 5,0 porque o .NET [oferece suporte](../../standard/net-standard.md#net-implementation-support) a todas as versões do .net Standard. A imagem a seguir mostra as dependências para o `Castle.Windsor` pacote:

![Captura de tela das dependências do NuGet para o pacote Castle. Windsor](./media/example-migration-core/nuget-dependencies.png)

Para verificar a compatibilidade do pacote, você pode usar a ferramenta <https://fuget.org> que oferece informações mais detalhadas sobre as versões e dependências.

Talvez o projeto faça referência a versões mais antigas do pacote que não dão suporte ao .NET, mas você pode encontrar versões mais recentes que dão suporte a ela. Portanto, a atualização de pacotes para versões mais recentes é geralmente uma boa recomendação. No entanto, você deve considerar que a atualização da versão do pacote pode introduzir algumas alterações significativas que forçariam a atualização do código.

O que acontecerá se você não encontrar uma versão compatível? E se você simplesmente não quiser atualizar a versão de um pacote devido a essas alterações significativas? Não se preocupe porque é possível depender de .NET Framework pacotes de um aplicativo .NET. Não se esqueça de testá-lo extensivamente, pois isso poderá causar erros em tempo de execução se o pacote externo chamar uma API que não está disponível no .NET. Isso é ótimo para quando você estiver usando um pacote antigo que não será atualizado e você pode simplesmente redirecionar para trabalhar no .NET.

#### <a name="check-for-api-compatibility"></a>Verificar compatibilidade de API

Como a superfície da API no .NET Framework e no .NET é semelhante, mas não idêntica, você deve verificar quais APIs estão disponíveis no .NET e quais não são. Você pode usar a ferramenta do analisador de portabilidade .NET para retonar as APIs usadas que não estão presentes no .NET. Ele examina o nível binário do seu aplicativo, extrai todas as APIs que são chamadas e, em seguida, lista quais APIs não estão disponíveis em sua estrutura de destino (.NET 5,0 nesse caso).

Você pode encontrar mais informações sobre essa ferramenta em:

<https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer>

Um aspecto interessante dessa ferramenta é que ela só faz a superfície das diferenças de seu próprio código e não do código de pacotes externos, que não podem ser alterados. Lembre-se de que você deve ter atualizado a maioria desses pacotes para que eles funcionem com o .NET.

### <a name="migrate-with-try-convert-tool"></a>Migrar com o try converter ferramenta

A ferramenta [tentar converter](https://github.com/dotnet/try-convert/releases) é uma ótima maneira de migrar um projeto. É uma ferramenta global que tenta atualizar o arquivo de projeto do estilo antigo para o novo estilo do SDK e redirecionar os projetos aplicáveis para o .NET 5. Uma vez instalado, você pode executar os seguintes comandos:

```dotnetcli
try-convert -p "<path to your project file>"
```

Ou:

```dotnetcli
try-convert -w "<path to your solution>"
```

Depois que a ferramenta tentar a conversão, recarregue os arquivos no Visual Studio para executar e testar. Há uma possibilidade de que tentar converter não seja capaz de executar a conversão devido a especificidades do seu projeto. Nesse caso, você pode consultar as etapas a seguir.

#### <a name="migrate-manually"></a>Migrar manualmente

1. Criar o novo projeto .NET

Na maioria dos casos, você desejará atualizar seu projeto existente para o novo formato .NET. No entanto, você também pode criar um novo projeto mantendo o antigo. A principal desvantagem de atualizar o projeto antigo é que você perde o suporte ao designer, que pode ser importante para você e sua equipe de desenvolvimento. Se você quiser continuar usando o designer, deverá criar um novo projeto .NET em paralelo com o antigo e compartilhar os ativos. Se você precisar modificar elementos da interface do usuário no designer, poderá alternar para o projeto antigo para fazer isso. E, como os ativos são vinculados, eles também serão atualizados no projeto .NET.

O [projeto em estilo SDK](../../core/project-sdk/msbuild-props.md) para .net é muito mais simples do que .NET Framework formato de projeto. Além das entradas mencionadas anteriormente `PackageReference` , você não precisará fazer muito mais. O novo formato de projeto [inclui arquivos com determinadas extensões por padrão](../../core/project-sdk/overview.md#default-includes-and-excludes), como `.cs` e `.xaml` arquivos, sem a necessidade de incluí-los explicitamente no arquivo do projeto.

#### <a name="assemblyinfo-considerations"></a>Considerações sobre AssemblyInfo

Os atributos são gerados automaticamente em projetos .NET. Se o projeto contiver um arquivo *AssemblyInfo.cs* , as definições serão duplicadas, o que causará conflitos de compilação. Você pode excluir o arquivo *AssemblyInfo.cs* mais antigo ou desabilitar a geração automática adicionando a seguinte entrada ao arquivo de projeto do .net:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>    
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

#### <a name="resources"></a>Recursos

Os recursos inseridos são incluídos automaticamente, mas os recursos não são, portanto, você precisa migrar os recursos para o novo arquivo de projeto.

#### <a name="package-references"></a>Referências de pacote

Com a opção **migrar packages.config para PackageReference** , você pode facilmente mover suas referências de pacote externo para o novo formato conforme mencionado anteriormente.

#### <a name="update-package-references"></a>Referências do pacote de atualização

Atualize as versões dos pacotes que você encontrou para serem compatíveis, conforme mostrado na seção anterior.

### <a name="fix-the-code-and-build"></a>Corrigir o código e compilar

#### <a name="microsoftwindowscompatibility"></a>Microsoft. Windows. Compatibility

Se seu aplicativo depende de APIs que não estão disponíveis no .NET, como registro, ACLs ou WCF, você precisa incluir uma referência ao `Microsoft.Windows.Compatibility` pacote para adicionar essas APIs específicas do Windows. Eles funcionam no .NET, mas não são incluídos, pois não são de plataforma cruzada.

Há uma ferramenta chamada API Analyzer ( <https://docs.microsoft.com/dotnet/standard/analyzers/api-analyzer> ) que ajuda a identificar APIs que não são compatíveis com seu código.

#### <a name="use-if-directives"></a>Usar as \# diretivas If

Se você precisar de caminhos de execução diferentes ao direcionar .NET Framework e .NET, deverá usar constantes de compilação. Adicione algumas \# diretivas If ao seu código para manter a mesma base de código para ambos os destinos.

#### <a name="technologies-not-available-on-net"></a>Tecnologias não disponíveis no .NET

Algumas tecnologias não estão disponíveis no .NET, como:

* AppDomains
* Comunicação remota
* Segurança de Acesso do Código
* Servidor WCF
* Fluxo de trabalho do Windows

É por isso que você precisa encontrar uma substituição para essas tecnologias se você as estiver usando em seu aplicativo. Para obter mais informações, consulte o artigo [.NET Framework tecnologias não disponíveis no .NET Core e no .NET 5 +](../../core/porting/net-framework-tech-unavailable.md) .

#### <a name="regenerate-autogenerated-clients"></a>Regenerar clientes gerados automaticamente

Se seu aplicativo usar código gerado automaticamente, como um cliente WCF, talvez seja necessário gerar novamente esse código para o .NET de destino. Às vezes, você pode encontrar algumas referências ausentes, já que elas não podem ser incluídas como parte do conjunto de assemblies do .NET padrão. Usando uma ferramenta como <https://apisof.net/> , você pode facilmente localizar o assembly no qual a referência ausente reside e adicioná-lo do NuGet.

#### <a name="rolling-back-package-versions"></a>Revertendo versões de pacote

Como regra geral, mencionamos anteriormente que você atualiza melhor cada versão de pacote para ser compatível com o .NET. No entanto, você pode descobrir que a direcionamento de uma versão atualizada e compatível de um assembly não é paga. Se o custo da alteração não for aceitável, você poderá considerar a reversão de versões do pacote, mantendo aquelas que você usa em .NET Framework. Embora eles possam não ser direcionados ao .NET, eles devem funcionar bem, a menos que chamem algumas APIs sem suporte.

### <a name="run-and-test"></a>Executar e testar

Depois de criar seu aplicativo sem erros, você pode iniciar a última etapa da migração testando cada funcionalidade.

Nesta etapa final, você pode encontrar vários problemas diferentes dependendo da complexidade do seu aplicativo e das dependências e das APIs que você está usando.

Por exemplo, se você usar arquivos de configuração (*app.config*), poderá encontrar alguns erros em tempo de execução, como seções de configuração não presentes. O uso do `Microsoft.Extensions.Configuration` pacote NuGet deve corrigir esse erro.

Outro motivo para erros é o uso dos `BeginInvoke` métodos e `EndInvoke` porque eles não têm suporte no .net. Eles não têm suporte no .NET porque têm uma dependência de comunicação remota, que não existe no .NET. Para resolver esse problema, tente usar a `await` palavra-chave (quando disponível) ou o <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> método.

Você pode usar analisadores de compatibilidade para permitir que você identifique APIs e padrões de código em seu código que podem causar problemas em tempo de execução com o .NET. Vá para <https://github.com/dotnet/platform-compat> e use o analisador de API do .net em seu projeto.

## <a name="migrating-a-windows-forms-application"></a>Migrando um aplicativo Windows Forms

Para demonstrar um processo de migração completo de um aplicativo Windows Forms, optamos por migrar o aplicativo de exemplo eShop disponível em <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopLegacyNTier/src/eShopWinForms> . Você pode encontrar o resultado completo da migração em <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopModernizedNTier/src/eShopWinForms> .

Este aplicativo mostra um catálogo de produtos e permite que o usuário navegue, filtre e pesquise produtos. Do ponto de vista da arquitetura, o aplicativo depende de um serviço WCF externo que serve como uma fachada para um banco de dados back-end.

Você pode ver a janela principal do aplicativo na imagem a seguir:

![Janela principal do aplicativo](./media/example-migration-core/main-application-window.png)

Se você abrir o arquivo de projeto *. csproj* , poderá ver algo assim:

![Captura de tela do conteúdo do arquivo csproj](./media/example-migration-core/csproj-file.png)

Como mencionado anteriormente, o projeto do .NET tem um estilo mais compacto e você precisa migrar a estrutura do projeto para o novo estilo .NET SDK.

Na Gerenciador de soluções, clique com o botão direito do mouse no projeto Windows Forms e selecione **descarregar**  >  **edição** do projeto.

Agora você pode atualizar o arquivo. csproj. Você excluirá todo o conteúdo e o substituirá pelo código a seguir:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

Salve e recarregue o projeto. Agora você concluiu a atualização do arquivo de projeto e o projeto está direcionando o .NET.

Se você compilar o projeto neste ponto, encontrará alguns erros relacionados à referência do cliente WCF. Como esse código é gerado automaticamente, você deve gerá-lo novamente para o .NET de destino.

![Captura de tela de erros de compilação no Visual Studio](./media/example-migration-core/winforms-compilation-errors.png)

Exclua o arquivo *Reference.cs* e gere um novo cliente de serviço.

Clique com o botão direito do mouse em **Serviços conectados** e selecione a opção **Adicionar serviço conectado** .

![Captura de tela do menu serviços conectados com a opção Adicionar serviço conectado selecionada](./media/example-migration-core/add-connected-service.png)

A janela Serviços conectados é aberta. Selecione a opção **Microsoft WCF Web Service** .

![Captura de tela da janela de serviços conectados](./media/example-migration-core/connected-services-window.png)

Se você tiver o serviço WCF na mesma solução que temos neste exemplo, você pode selecionar a opção **Discover** em vez de especificar uma URL de serviço.

![Captura de tela da janela Configurar referência do serviço Web WCF](./media/example-migration-core/configure-wcf-reference.png)

Quando o serviço estiver localizado, a ferramenta refletirá o contrato de API implementado pelo serviço. Altere o nome do namespace para que ele seja `eShopServiceReference` conforme mostrado na imagem a seguir:

![Captura de tela do contrato de API e o namespace alterado](./media/example-migration-core/api-contract-namespace.png)

Selecione o botão **concluir** . Após alguns instantes, você verá o código gerado.

Você deve ver três arquivos gerados automaticamente:

1. *Introdução*: um link para o GitHub para fornecer algumas informações sobre o WCF.
2. *ConnectedService.jsem*: parâmetros de configuração para se conectar ao serviço.
3. *Reference.cs*: o código do cliente WCF real.

![Captura de tela da janela de Gerenciador de Soluções com os três arquivos gerados automaticamente](./media/example-migration-core/autogenerated-files.png)

Se você compilar novamente, verá muitos erros provenientes de arquivos *. cs* dentro da pasta *auxiliar* . Essa pasta estava presente na versão .NET Framework, mas não está incluída no Old *. csproj*. Mas com o novo projeto no estilo SDK, todos os arquivos de código presentes abaixo do local do arquivo de projeto são incluídos por padrão. Ou seja, o novo projeto .NET Core tenta compilar os arquivos dentro da pasta *auxiliar* . Como essa pasta não é necessária, você pode excluí-la com segurança.

Se você compilar o projeto novamente e executá-lo, não verá as imagens do produto. O problema é que agora o caminho para os arquivos foi ligeiramente alterado. Para corrigir esse problema, você precisa adicionar outro nível de profundidade no caminho, atualizando no arquivo `CatalogView.cs` a linha:

```csharp
string image_name = Environment.CurrentDirectory + "\\..\\..\\Assets\\Images\\Catalog\\" + catalogItems.Picturefilename;
```

para

```csharp
string image_name = Environment.CurrentDirectory + "\\..\\..\\..\\Assets\\Images\\Catalog\\" + catalogItems.Picturefilename;
```

Após essa alteração, você pode verificar se o aplicativo é iniciado e executado conforme o esperado no .NET Core.

## <a name="migrating-a-wpf-application"></a>Migrando um aplicativo WPF

Usaremos o aplicativo de `Shop.ClassicWPF` exemplo para executar a migração. A imagem a seguir mostra uma captura de tela do aplicativo antes da migração:

![Aplicativo de exemplo antes da migração](./media/example-migration-core/app-before-migration.png)

Esse aplicativo usa um banco de dados SQL Server Express local para armazenar as informações do catálogo de produtos. Esse banco de dados é acessado diretamente do aplicativo do WPF.

Primeiro, você deve atualizar o arquivo *. csproj* para o novo estilo do SDK usado por aplicativos do .NET Core. Você seguirá as mesmas etapas descritas na Windows Forms migração: você descarregará o projeto, abrirá o arquivo *. csproj* , atualizará seu conteúdo e recarregará o projeto.

Nesse caso, exclua todo o conteúdo do arquivo *. csproj* e substitua-o pelo seguinte código:

```xml
 <Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>
    <UseWpf>true</UseWpf>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

Se você recarregar o projeto e compilá-lo, obterá o seguinte erro:

![Captura de tela de erros de compilação no Visual Studio](./media/example-migration-core/wpf-compilation-error.png)

Como você excluiu todo o conteúdo *. csproj* , você perdeu uma especificação de referência de projeto presente no projeto antigo. Você só precisa adicionar essa linha ao arquivo *. csproj* para incluir a referência do projeto de volta:

```xml
<ItemGroup>
    <ProjectReference Include="..\\eShop.SqlProvider\\eShop.SqlProvider.csproj" />
<ItemGroup>
```

Você também pode permitir que o Visual Studio o ajude clicando com o botão direito do mouse no nó **dependências** e selecionando **Adicionar referência de projeto**. Selecione o projeto da solução e clique em **OK**:

![Captura de tela da caixa de diálogo Gerenciador de referências com o projeto eShop. sqlfornecetor selecionado](./media/example-migration-core/reference-manager.png)

Depois de adicionar a referência de projeto ausente, o aplicativo é compilado e executado conforme o esperado no .NET.

>[!div class="step-by-step"]
>[Anterior](windows-migration.md) 
> [Avançar](deploy-modern-applications.md)
