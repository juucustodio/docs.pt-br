---
title: Exemplo de migração de eShop para ASP.NET Core
description: Uma explicação da migração de um aplicativo MVC ASP.NET existente para ASP.NET Core, usando um aplicativo de loja online de exemplo como uma referência.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 2b7e3aaf70d7400cf84814c7c9845d5444321f1f
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488390"
---
# <a name="example-migration-of-eshop-to-aspnet-core"></a>Exemplo de migração de eShop para ASP.NET Core

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Neste capítulo, você verá como migrar um aplicativo .NET Framework para o .NET Core. O capítulo examina um aplicativo de loja online de exemplo escrito para ASP.NET 5,0. O aplicativo usará muitos dos conceitos e ferramentas descritos anteriormente neste livro. Você encontrará o aplicativo de ponto de partida no [repositório GitHub do *eShopModernizing*](https://github.com/dotnet-architecture/eShopModernizing). Há vários aplicativos de ponto de partida diferentes. Este capítulo se concentra no *eShopLegacyMVCSolution*.

A versão inicial do projeto é mostrada na Figura 4-1. É um aplicativo ASP.NET MVC 5 bastante padrão.

![Figura 4-1](media/Figure4-1.png)

**Figura 4-1.** A estrutura do projeto de exemplo do *eShopModernizing* MVC.

## <a name="run-apiport-to-identify-problematic-apis"></a>Executar *ApiPort* para identificar APIs problemáticas

A primeira etapa na preparação para migrar é executar a ferramenta *ApiPort* . A ferramenta identifica quantas .NET Framework APIs o aplicativo chama e quantos deles têm .NET Standard ou equivalentes do .NET Core. Concentre-se principalmente na lógica do seu aplicativo, não em dependências de terceiros e preste atenção às `System.Web` dependências que precisarão ser portadas. A ferramenta ApiPort foi introduzida no último capítulo sobre como [entender e atualizar dependências](/understand-update-dependencies.md).

Depois de [instalar e configurar a ferramenta *ApiPort*](https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer), execute a análise de dentro do Visual Studio, como mostra a Figura 4-2.

![Figura 4-2](media/Figure4-2.png)

**Figura 4-2.** Analise a portabilidade do assembly no Visual Studio.

Escolha o assembly do projeto Web na pasta *bin* do projeto, conforme mostrado na Figura 4-3.

![Figura 4-3](media/Figure4-3.png)

**Figura 4-3.** Escolha o assembly da Web do projeto.

Se sua solução incluir vários projetos, você poderá escolher todos eles. O exemplo *eshop* inclui apenas um único projeto MVC.

Depois que o relatório for gerado, abra o arquivo e examine os resultados. O resumo fornece uma exibição de alto nível da porcentagem de chamadas de .NET Framework que seu aplicativo está fazendo em versões compatíveis. A Figura 4-4 mostra o resumo do projeto *eshop* MVC.

![Figura 4-4](media/Figure4-4.png)

**Figura 4-4.** Resumo de ApiPort.

Para este aplicativo, cerca de 80% das chamadas de .NET Framework são compatíveis. 20 por cento das chamadas precisam ser abordadas durante o processo de portamento. A exibição dos detalhes revela que todas as chamadas incompatíveis são parte do `System.Web` , que é uma incompatibilidade esperada. As dependências nas `System.Web` chamadas serão resolvidas quando os controladores e as classes relacionadas do aplicativo forem migrados em uma etapa posterior. A Figura 4-5 lista alguns dos tipos específicos encontrados pela ferramenta:

![Figura 4-5](media/Figure4-5.png)

**Figura 4-5.** Detalhes do tipo incompatível do *ApiPort* .

A maioria dos tipos incompatíveis refere-se a `Controller` e a vários atributos relacionados que têm equivalentes em ASP.NET Core.

## <a name="update-project-files-and-nuget-reference-syntax"></a>Atualizar arquivos de projeto e sintaxe de referência do NuGet

Em seguida, migre da estrutura de arquivos *. csproj* mais antiga para a estrutura mais recente e mais simples introduzida com o .NET Core. Ao fazer isso, você também migrará do uso de um arquivo *packages.config* para referências do NuGet para o uso de `<PackageReference>` elementos no arquivo de projeto.

O arquivo *eShopLegacyMVC. csproj* do projeto original tem 418 linhas de comprimento. Uma amostra do arquivo de projeto é mostrada na Figura 4-6. Para oferecer uma noção de seu tamanho e complexidade gerais, o lado direito da imagem contém uma exibição em miniatura de todo o arquivo.

![Figura 4-6](media/Figure4-6.png)

**Figura 4-6.** A estrutura do arquivo *eShopLegacyMVC. csproj* .

Uma maneira comum de criar um novo arquivo de projeto para um projeto ASP.net existente é criar um novo aplicativo ASP.NET Core usando `dotnet new` ou **arquivo**  >  **novo**  >  **projeto** no Visual Studio. Em seguida, os arquivos podem ser copiados do projeto antigo para o novo para concluir a migração.

Além do arquivo de projeto C#, as dependências do NuGet são armazenadas em um arquivo de *packages.config* de linha de 45 separado, como mostra a Figura 4-7.

![Figura 4-7](media/Figure4-7.png)

**Figura 4-7.** O arquivo de *packages.config* .

Depois de atualizar para o novo formato de arquivo *. csproj* , você pode migrar *packages.config* em projetos de biblioteca de classes usando o Visual Studio. No entanto, essa funcionalidade não funciona com projetos ASP.NET. [Saiba mais sobre como migrar *packages.config* para o `<PackageReference>` no Visual Studio](https://docs.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference). Se você tiver um grande número de projetos para migrar, [essa ferramenta de Comunidade poderá ajudar](https://github.com/MarkKharitonov/NuGetPCToPRMigrator).

## <a name="create-new-aspnet-core-project"></a>Criar novo projeto de ASP.NET Core

Adicione um novo projeto ASP.NET Core à solução do aplicativo existente para facilitar a movimentação de arquivos, pois a maior parte do trabalho pode ser feita no **Gerenciador de soluções** do Visual Studio. No Visual Studio, clique com o botão direito do mouse na solução do seu aplicativo e escolha **Adicionar novo projeto**. Escolha **ASP.NET Core aplicativo Web** e dê um nome ao novo projeto, conforme mostrado na Figura 4-8.

![Figura 4-8](media/Figure4-8.png)

**Figura 4-8.** Adicionar novo aplicativo Web ASP.NET Core.

A próxima caixa de diálogo solicitará que você escolha qual modelo usar. Selecione o modelo **Vazio**. Certifique-se também de alterar a lista suspensa do **.NET Core** para **.NET Framework**. Selecione **ASP.NET Core 2,2**, conforme mostrado na Figura 4-9.

![Figura 4-9](media/Figure4-9.png)

**Figura 4-9.** Escolha um modelo de projeto vazio destinado a .NET Framework com ASP.NET Core 2,2.

### <a name="migrating-nuget-packages"></a>Migrando pacotes NuGet

Como a ferramenta de migração interna para migrar *packages.config* para o `<PackageReference>` não funciona em projetos ASP.net, você pode usar uma ferramenta de comunidade em vez disso ou migrar manualmente. Uma [ferramenta da Comunidade que](https://gist.github.com/tomkuijsten/2d75074d9a3c19c04ee8ea19a6289ddf) usei usa um arquivo XSL para transformar de um formato para outro. Para usá-lo, primeiro copie o arquivo de *packages.config* para a pasta de projeto de ASP.NET Core recém-criada. Faça um backup de seus arquivos, pois esse script remove o arquivo de *packages.config* de todas as pastas em que você executa o script. Em seguida, execute estes comandos na pasta do projeto (ou para toda a solução, se preferir):

```powershell
iwr https://git.io/vdKaV -OutFile Convert-ToPackageReference.ps1
iwr https://git.io/vdKar -OutFile  Convert-ToPackageReference.xsl
./Convert-ToPackageReference.ps1 | Out-Null
```

Os dois primeiros comandos baixam arquivos para que eles existam localmente. A última linha executa o script. Depois de executá-lo, tente Compilar o novo projeto. Você provavelmente obterá alguns erros. Para resolvê-los, você desejará eliminar algumas referências (como a maioria dos `Microsoft.AspNet` `System` pacotes e), e talvez seja necessário remover alguns `xmlns` atributos.

Na maioria dos aplicativos MVC ASP.NET, muitas dependências do lado do cliente, como Bootstrap e jQuery, foram implantadas usando pacotes NuGet. No ASP.NET Core, os pacotes NuGet são usados apenas para a funcionalidade do lado do servidor. Os arquivos do cliente devem ser gerenciados por outros meios. Examine a lista de `<PackageReference>` elementos adicionados e remova e anote quaisquer que sejam para bibliotecas de cliente, incluindo:

- Bootstrap
- jQuery
- jQuery. Validation
- Modernizr
- popper.js
- Responder

Os arquivos de cliente estáticos instalados pelo NuGet para esses pacotes serão copiados para a pasta *wwwroot* do novo projeto e hospedados a partir daí. Vale a pena considerar se esses arquivos ainda são necessários para o aplicativo e se faz sentido continuar hospedando-os ou usar uma CDN (rede de distribuição de conteúdo) em vez disso. Essas versões de biblioteca podem ser gerenciadas no momento da compilação usando ferramentas como [LibMan](https://docs.microsoft.com/aspnet/core/client-side/libman/) ou [NPM](https://www.npmjs.com/). A Figura 4-10 mostra o arquivo *eShopPorted. csproj* completo após a migração de referências de pacote usando a ferramenta de conversão mostrada e removendo pacotes desnecessários.

![Figura 4-10](media/Figure4-10.png)

**Figura 4-10.** Referências de pacote no arquivo *eShopPorted. csproj* .

As referências de pacote podem ser ainda mais compactadas, fazendo com que o `<Version>1.0.0.0</Version>` elemento seja um `Version=1.0.0.0` atributo `<PackageReference>` .

### <a name="migrate-static-files"></a>Migrar arquivos estáticos

Todos os arquivos estáticos que o aplicativo usa, incluindo scripts e estruturas de terceiros, mas também imagens e folhas de estilo personalizadas, devem ser copiados do projeto antigo para o novo. Em aplicativos MVC ASP.NET, os arquivos normalmente eram acessados com base em sua localização dentro da pasta do projeto. Em ASP.NET Core aplicativos, esses arquivos estáticos serão acessados com base em sua localização dentro da pasta *wwwroot* . Para o projeto *eshop* , há arquivos estáticos nas seguintes pastas:

* *Conteúdo*
* *TrueType*
* *Imagens*
* *Classificação pics*
* *Scripts*

O modelo de projeto **vazio** usado na etapa anterior não inclui essa pasta por padrão ou o middleware necessário para que ela funcione. Você precisará adicioná-los.

Adicione uma pasta *wwwroot* à raiz do projeto.

Adicione a versão 2.2.0 do `Microsoft.AspNetCore.StaticFiles` pacote NuGet.

No *Startup.cs*, adicione uma chamada para `app.UseStaticFiles()` no `Configure` método:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseStaticFiles();
    
    // ...
}
```

Copie a pasta de *conteúdo* do aplicativo ASP.NET MVC para a pasta *wwwroot* do novo projeto.

Execute o aplicativo e navegue até sua pasta */Content/base.css* para verificar se o arquivo estático foi servido corretamente a partir do caminho esperado. Continue copiando o restante das pastas que contêm arquivos estáticos para o novo projeto. Você também desejará copiar o arquivo *favicon. ico* da raiz do projeto para a pasta *wwwroot* . A Figura 4-11 mostra os resultados depois que esses arquivos e suas pastas são copiados.

![Figura 4-11](media/Figure4-11.png)

**Figura 4-11.** Pastas estáticas copiadas para a pasta *wwwroot* .

### <a name="migrate-c-files"></a>Migrar arquivos C#

Em seguida, copie os arquivos C# usados pelo aplicativo, incluindo as pastas MVC padrão e seu conteúdo, como *controladores*, *modelos*, *ViewModel* e *Serviços*. Provavelmente, haverá algumas alterações necessárias nesses arquivos. É melhor copiar uma pasta (ou subpasta) de cada vez e compilar para ver quais erros precisam ser resolvidos conforme o uso.

Para o exemplo *eshop* , a primeira pasta que escolho para migrar é a pasta *modelos* , que inclui entidades do C# e classes de Entity Framework. As classes dessa pasta são usadas pela maioria das outras, portanto, não funcionarão até que essas classes tenham sido copiadas. Depois de copiar a pasta e compilar, o compilador revelava erros relacionados a namespace ausente `System.Web.Hosting` , acesso relacionado ao `HostingEnvironment` e uma referência a `ConfigurationManager.AppSettings` . A solução para esses problemas será passar os dados de caminho necessários; por enquanto, as linhas de interrupção são comentadas e um `TODO:` comentário é adicionado a cada uma para rastreá-la. Depois de alterar cinco linhas, o **lista de tarefas** mostra cinco itens e o projeto é compilado.

Em seguida, a pasta *ViewModel* , com sua única classe, é copiada. É fácil e compila imediatamente.

A pasta *Serviços* é copiada. As classes dessa pasta dependem de Entity Framework classes da pasta *modelos* , que é o motivo pelo qual ela precisava ser copiada após essa pasta. Felizmente, ela é compilada sem erros.

Isso deixa a pasta *controladores* e suas duas `Controller` classes. Depois de copiar a pasta para o novo projeto e compilar, há sete erros de compilação. Quatro deles estão relacionados ao `ViewBag` acesso e reportam um erro de:

> `Missing compiler required member 'Microsoft.CSharp.RuntimeBinder.CSharpArgumentInfo.Create'`

Para resolver esse erro, adicione uma referência de pacote NuGet ao C#:

```xml
<PackageReference Include="Microsoft.CSharp" Version="4.7.0" />
```

Os três erros restantes especificam tipos que são definidos em um assembly que não é referenciado. Especificamente, esses tipos:

- `HttpServerUtilityBase`
- `RouteValueDictionary`
- `HttpRequestBase`

Vamos examinar cada erro um por um. O primeiro erro ocorre ao tentar referenciar a `Server` propriedade de `Controller` , que não existe mais. O objetivo da operação é obter o caminho para um arquivo de imagem no aplicativo:

```csharp
if (item != null)
{
    var webRoot = Server.MapPath("~/Pics"); // compiler error on this line
    var path = Path.Combine(webRoot, item.PictureFileName);

    string imageFileExtension = Path.GetExtension(item.PictureFileName);
    string mimetype = GetImageMimeTypeFromImageFileExtension(imageFileExtension);

    var buffer = System.IO.File.ReadAllBytes(path);

    return File(buffer, mimetype);
}
```

Há duas soluções possíveis para esse problema. A primeira é manter a funcionalidade como está. Nesse caso, em vez de usar `Server.MapPath` , um caminho fixo referenciando o local dos arquivos de imagem em *wwwroot* deve ser usado. Como alternativa, como a única finalidade desse método de ação é retornar um arquivo de imagem estático, as referências a essa ação nos arquivos de exibição podem ser atualizadas para referenciar os arquivos estáticos diretamente, o que melhora o desempenho do tempo de execução. Como nenhum processamento está sendo feito como parte dessa ação, não há motivo para não apenas servir os arquivos diretamente. Se não for tenable atualizar todas as referências a essa ação, a ação poderá ser reescrita para produzir um redirecionamento para o local do arquivo estático.

Os dois próximos erros ocorrem no mesmo método privado na mesma linha de código:

```csharp
private void AddUriPlaceHolder(CatalogItem item)
{
    item.PictureUri = this.Url.RouteUrl(PicController.GetPicRouteName, new { catalogItemId = item.Id }, this.Request.Url.Scheme);
}
```

Ambos `this.Url` e `this.Request` causam erros de compilador. Observando como esse código é usado, sua finalidade é criar um link para a `PicController` ação que processa arquivos de imagem. O mesmo que acabamos de descobrir pode ser substituído por links diretos para os arquivos estáticos localizados em *wwwroot*. Por enquanto, vale a pena comentar esse código e adicionar um `TODO:` comentário para fazer referência à pics de outra maneira.

Vale a pena observar que a classe base `Controller` , usada pela `CatalogController` classe na qual esse código aparece, ainda está se referindo `System.Web.Mvc.Controller` . Certamente haverá mais erros a serem corrigidos depois que atualizarmos isso para usar ASP.NET Core. Primeiro, remova a `using System.Web.Mvc;` linha da lista de `using` instruções em `CatalogController` . Em seguida, adicione o pacote NuGet `Microsoft.AspNetCore.Mvc` . Por fim, adicione uma `using Microsoft.AspNetCore.Mvc;` instrução e compile o aplicativo novamente.

Desta vez, há 16 erros:

- `Include` Não é um argumento de atributo nomeado válido (2)
- `HttpStatusCodeResult` não encontrado (3)
- `HttpNotFound` Não existe (3)
- `SelectList` não encontrado (8)

Mais uma vez, vamos examinar esses erros um a um. Primeiro, `SelectList` pode ser corrigido adicionando `using Microsoft.AspNetCore.Mvc.Rendering;` , o que elimina a metade dos erros.

Todas as referências a `return HttpNotFound();` devem ser substituídas por `return NotFound();` .

Todas as referências a `return new HttpStatusCodeResult(HttpStatusCode.BadRequest);` devem ser substituídas por `return BadRequest();` .

Isso apenas deixa o uso de `Include` com um `[Bind]` atributo em dois métodos de ação que têm esta aparência:

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public ActionResult Create([Bind(Include = "Id,Name,Description,Price,PictureFileName,CatalogTypeId,CatalogBrandId,AvailableStock,RestockThreshold,MaxStockThreshold,OnReorder")] CatalogItem catalogItem)
{
```

O código anterior restringe a associação de modelo às propriedades listadas na `Include` cadeia de caracteres. No ASP.NET Core MVC, o `[Bind]` atributo ainda existe, mas não precisa mais do `Include =` argumento. Passe a lista de propriedades diretamente para o `[Bind]` atributo:

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public ActionResult Create([Bind("Id,Name,Description,Price,PictureFileName,CatalogTypeId,CatalogBrandId,AvailableStock,RestockThreshold,MaxStockThreshold,OnReorder")] CatalogItem catalogItem)
{
```

Com essas alterações, o projeto é compilado mais uma vez. Geralmente, é uma prática melhor usar tipos de modelo separados para entradas de controlador, em vez de usar a associação de modelo diretamente para o modelo de domínio ou tipos de modelo de dados.

## <a name="migrate-views"></a>Migrar exibições

Os dois maiores ASP.NET Core recursos do MVC relacionados às exibições são [Razor Pages](https://docs.microsoft.com/aspnet/core/razor-pages/) e os [auxiliares de marca](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/built-in/). Para a migração inicial, não usaremos nenhum recurso. No entanto, você deve manter os recursos em mente se continuar a dar suporte ao aplicativo depois que ele tiver sido migrado. A próxima etapa é copiar a pasta *views* do projeto original para uma nova. Após a criação, há nove erros:

- HttpContext não existe (2)
- Os scripts não existem (5)
- Os estilos não existem (1)
- Não foi possível encontrar a HtmlString (1)

A investigação desses erros descobre que a maioria deles está no principal *_Layout. cshtml*, com vários relacionados à renderização de marcas de script e estilo, ou a exibição quando o servidor que hospeda o aplicativo foi reiniciado pela última vez. A listagem de código a seguir mostra áreas problemáticas no arquivo *_Layout. cshtml* :

```razor
// other lines omitted; only errors shown
@Styles.Render("~/Content/css")
@Scripts.Render("~/bundles/modernizr")

@{ var sessionInfo = new HtmlString($"{HttpContext.Current.Session["MachineName"]}, {HttpContext.Current.Session["SessionStartTime"]}");}

@Scripts.Render("~/bundles/jquery")
@Scripts.Render("~/bundles/bootstrap")
```

A referência ao Modernizr pode ser removida. As referências a Bootstrap e jQuery podem ser substituídas por links CDN para a versão apropriada.

Substituir `@Styles.Render` linha por:

```html
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
```

Substitua as duas últimas `Scripts.Render` linhas por:

```html
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
```

Finalmente, após a inicialização `<link>` , adicione outros `<link>` elementos para os estilos locais que seu aplicativo usa. Para *eshop*, o resultado é mostrado aqui:

```html
<link rel="stylesheet" href="~/Content/custom.css" />
<link rel="stylesheet" href="~/Content/base.css" />
<link rel="stylesheet" href="~/Content/Site.css" />
```

Para determinar a ordem na qual os `<link>` elementos devem aparecer, examine o HTML renderizado do aplicativo original. Como alternativa, examine *BundleConfig.cs*, que para o exemplo *eshop* inclui esse código indicando a sequência apropriada:

```csharp
bundles.Add(new StyleBundle("~/Content/css").Include(
          "~/Content/bootstrap.css",
          "~/Content/custom.css",
          "~/Content/base.css",
          "~/Content/site.css"));
```

A criação de novamente revela mais um erro ao carregar a validação do jQuery nas exibições *criar* e *Editar* . Substituir por este script:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.17.0/jquery.validate.min.js" integrity="sha512-O/nUTF5mdFkhEoQHFn9N5wmgYyW323JO6v8kr6ltSRKriZyTr/8417taVWeabVS4iONGk2V444QD0P2cwhuTkg==" crossorigin="anonymous"></script>
```

A última coisa a ser corrigida nas exibições é a referência a `Session` para exibir por quanto tempo o aplicativo está em execução e em qual computador. Podemos coletar esses dados `Startup` como variáveis estáticas e exibir as variáveis na página de layout. Adicione as seguintes propriedades a *Startup.cs*:

```csharp
public static DateTime StartTime { get; } = DateTime.UtcNow;
public static string MachineName { get; } = Environment.MachineName;
```

Em seguida, substitua o conteúdo do rodapé no layout pelo código a seguir:

```razor
<section class="col-sm-6">
    <img class="esh-app-footer-text hidden-xs" src="~/images/main_footer_text.png" width="335" height="26" alt="footer text image" />
    <br />
<small>@eShopPorted.Startup.MachineName - @eShopPorted.Startup.StartTime.ToString() UTC</small>
</section>
```

Neste ponto, o aplicativo mais uma vez compila com êxito. No entanto, tentar executá-lo apenas produz *Olá, mundo!* Porque o modelo de ASP.NET Core **vazio** só é configurado para exibir isso em resposta a qualquer solicitação. Na próxima seção, concluo a migração Configurando o aplicativo para usar ASP.NET Core MVC, incluindo injeção de dependência e configuração. Quando isso estiver em vigor, o aplicativo deverá ser executado. Em seguida, será hora de corrigir as `TODO:` tarefas que foram criadas anteriormente.

## <a name="migrate-app-startup-components"></a>Migrar componentes de inicialização de aplicativo

A última etapa de migração é pegar as tarefas de inicialização do aplicativo do *global. asax* e as classes que ele chama e migrá-las para seus equivalentes ASP.NET Core. Essas tarefas incluem a configuração do MVC em si, a configuração da injeção de dependência e o trabalho com o novo sistema de configuração. No ASP.NET Core, essas tarefas são tratadas no arquivo *Startup.cs* .

### <a name="configure-mvc"></a>Configurar o MVC

O aplicativo MVC original do ASP.NET tem o seguinte código em `Application_Start` *global. asax*, que é executado quando o aplicativo é inicializado:

```csharp
protected void Application_Start()
{
    container = RegisterContainer();
    AreaRegistration.RegisterAllAreas();
    FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
    RouteConfig.RegisterRoutes(RouteTable.Routes);
    BundleConfig.RegisterBundles(BundleTable.Bundles);
    ConfigDataBase();
}
```

Observando essas linhas uma por uma, o `RegisterContainer` método configura a injeção de dependência, que será portada abaixo. As próximas três linhas configuram diferentes partes do MVC: áreas, filtros e rotas. Os pacotes são substituídos por arquivos estáticos no aplicativo portado. A última linha configura o acesso a dados para o aplicativo, que será mostrado em uma seção posterior.

Como esse aplicativo não está realmente usando áreas, não há nada que precise ser feito para migrar a chamada de registro de área. Se seu aplicativo precisar migrar áreas, o [docs especificará como configurar áreas no ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/controllers/areas).

A chamada para registrar filtros globais invoca um auxiliar na `FilterConfig` classe na pasta *App_Start* do aplicativo:

```csharp
public static void RegisterGlobalFilters(GlobalFilterCollection filters)
{
    filters.Add(new HandleErrorAttribute());
}
```

O único atributo adicionado ao aplicativo é o filtro MVC do ASP.NET, `HandleErrorAttribute` . Esse filtro garante que quando uma exceção ocorrer como parte de uma solicitação, uma ação e uma exibição padrão serão exibidas, em vez dos detalhes da exceção. Em ASP.NET Core, essa mesma funcionalidade é executada pelo `UseExceptionHandler` middleware. As mensagens de erro detalhadas não são habilitadas por padrão. Eles devem ser configurados usando o `UseDeveloperExceptionPage` middleware. Para configurar esse comportamento para corresponder ao aplicativo original, o código a seguir deve ser adicionado ao início do `Configure` método em *Startup.cs*:

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
    }
    // ...
}
```

Isso se encarrega do único filtro usado pelo aplicativo eShop e, nesse caso, foi feito usando o middleware interno. Se você tiver filtros globais que devem ser configurados em seu aplicativo, isso é feito quando o MVC é adicionado no `ConfigureServices` método, que é mostrado mais adiante neste capítulo.

A última parte da lógica relacionada ao MVC que precisa ser migrada são as rotas padrão do aplicativo. A chamada para `RouteConfig.RegisterRoutes(RouteTable.Routes)` passa a tabela de rotas MVC para o `RegisterRoutes` método auxiliar, em que o código a seguir é executado quando o aplicativo é inicializado:

```csharp
public static void RegisterRoutes(RouteCollection routes)
{
    routes.MapMvcAttributeRoutes();
    routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Catalog", action = "Index", id = UrlParameter.Optional }
    );
}
```

Ao usar esse código linha por linha, a primeira linha configura o suporte para rotas de atributo. Isso é criado em ASP.NET Core, portanto, não é necessário configurá-lo separadamente. Da mesma forma, os arquivos de *{Resource}. axd* não são usados com ASP.NET Core, portanto, não há necessidade de ignorar essas rotas. O `MapRoute` método configura o padrão para MVC, que usa o `{controller}/{action}/{id}` modelo de rota típico. Ele também especifica os padrões para esse modelo, de modo que o `CatalogController` é o controlador padrão usado e o `Index` método é a ação padrão. Aplicativos maiores geralmente incluirão mais chamadas para `MapRoute` configurar rotas adicionais.

ASP.NET Core MVC dá suporte ao roteamento [convencional e ao roteamento de atributos](https://docs.microsoft.com/aspnet/core/mvc/controllers/routing?view=aspnetcore-2.2&preserve-view=true). O roteamento convencional é análogo a como a tabela de rotas é configurada no `RegisterRoutes` método listado anteriormente. Para configurar o roteamento convencional com uma rota padrão como aquela usada no aplicativo *eshop* , adicione o seguinte código à parte inferior do `Configure` método em *Startup.cs*:

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute("default", "{controller=Catalog}/{action=Index}/{id?}");
});
```

> [!NOTE]
> Com o ASP.NET Core 3,0 e posterior, isso é alterado para usar pontos de extremidade. Para a porta inicial para ASP.NET Core 2,2, essa é a sintaxe adequada para mapear rotas convencionais.

Com essas alterações em vigor, o `Configure` método é quase concluído. O método do modelo original `app.Run` que imprime *Olá, mundo!* deve ser excluído. Neste ponto, o método é como mostrado aqui:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseStaticFiles();

    app.UseMvc(routes =>
    {
        routes.MapRoute("default", "{controller=Catalog}/{action=Index}/{id?}");
    });
}
```

Agora é hora de configurar os serviços MVC, seguidos pelo restante do suporte do aplicativo para injeção de dependência (DI). Até agora, o método do projeto *eShopPorted* `ConfigureServices` permaneceu vazio. Agora é hora de começar a preenchê-lo.

Primeiro, para obter ASP.NET Core o MVC funcione corretamente, ele precisa ser adicionado:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
}
```

O código anterior é a configuração mínima necessária para obter recursos do MVC funcionando. Há muitos recursos adicionais que podem ser configurados nessa chamada, mas por enquanto isso será suficiente para compilar o aplicativo. Executá-lo agora roteia a solicitação padrão corretamente, mas como ainda não configuramos DI, ocorre um erro durante a ativação `CatalogController` , pois nenhuma implementação do tipo foi `ICatalogService` fornecida ainda. Retornaremos para configurar o MVC mais adiante em alguns instantes. Por enquanto, vamos migrar a injeção de dependência do aplicativo.

#### <a name="migrate-dependency-injection-configuration"></a>Migrar configuração de injeção de dependência

O arquivo *global. asax* do aplicativo original define o seguinte método, chamado quando o aplicativo é inicializado:

```csharp
protected IContainer RegisterContainer()
{
  var builder = new ContainerBuilder();

  builder.RegisterControllers(typeof(MvcApplication).Assembly);

  var mockData = bool.Parse(ConfigurationManager.AppSettings["UseMockData"]);
  builder.RegisterModule(new ApplicationModule(mockData));

  var container = builder.Build();
  DependencyResolver.SetResolver(new AutofacDependencyResolver(container));

  return container;
}
```

Esse código configura um contêiner [Autofac](https://autofac.org/) , lê uma definição de configuração para determinar se dados reais ou fictícios devem ser usados e passa essa configuração para um módulo Autofac (encontrado no diretório */modules* do aplicativo). Felizmente, o Autofac dá suporte ao .NET Core, portanto, o módulo pode ser migrado diretamente. Copie a pasta no novo projeto e atualize o namespace da classe e ela deverá ser compilada.

ASP.NET Core tem suporte interno para injeção de dependência, mas você pode conectar um contêiner de terceiros, como o Autofac facilmente, se necessário. Nesse caso, como o aplicativo já está configurado para usar o Autofac, a solução mais simples é manter seu uso. Para fazer isso, a `ConfigureServices` assinatura do método deve ser modificada para retornar um `IServiceProvider` , e a instância de contêiner Autofac deve ser configurada e retornada do método.

**Observação:** No .NET Core 3,0 e posterior, o processo de integração de um contêiner de DI de terceiros foi alterado.

Parte da configuração do Autofac requer uma chamada para `builder.Populate(services)` . Essa extensão é encontrada no `Autofac.Extensions.DependencyInjection` pacote NuGet, que deve ser instalado antes que o código seja compilado.

Depois `ConfigureServices` de modificar para configurar um contêiner Autofac, o novo método é como mostrado aqui:

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    // Create Autofac container builder
    var builder = new ContainerBuilder();
    builder.Populate(services);
    bool useMockData = true; // TODO: read from config
    builder.RegisterModule(new ApplicationModule(useMockData));

    ILifetimeScope container = builder.Build();

    return new AutofacServiceProvider(container);
}
```

Por enquanto, a configuração para `useMockData` é definida como `true` . Essa configuração será lida a partir da configuração em breve. Neste ponto, o aplicativo é compilado e carregado com êxito quando executado, como mostra a Figura 4-12.

![Figura 4-12](media/Figure4-12.png)

**Figura 4-12.** Aplicativo *eshop* com porta em execução localmente com dados fictícios.

#### <a name="migrate-app-settings"></a>Migrar configurações de aplicativo

O ASP.NET Core usa um novo [sistema de configuração](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/?view=aspnetcore-2.2&preserve-view=true), que por padrão utiliza um *appsettings.jsno* arquivo. Usando `CreateDefaultBuilder` o no *Program.cs*, a configuração padrão já está configurada no aplicativo. Para acessar a configuração, as classes precisam apenas solicitá-las em seu construtor. A `Startup` classe não é exceção. Para começar a acessar a configuração no `Startup` e no restante do aplicativo, solicite uma instância do `IConfiguration` de seu construtor:

```csharp
public Startup(IConfiguration configuration)
{
    Configuration = configuration;
}

public IConfiguration Configuration { get; }
```

O aplicativo original referenciou suas configurações usando `ConfigurationManager.AppSettings` . Uma pesquisa rápida de todas as referências deste termo produz o conjunto de configurações que o novo aplicativo precisa. Há apenas dois:

- `UseMockData`
- `UseCustomizationData`

Se seu aplicativo tiver uma configuração mais complexa, especialmente se estiver usando seções de configuração personalizadas, você provavelmente desejará criar e associar objetos a diferentes partes da configuração do aplicativo. Esses tipos podem então ser acessados usando o [padrão de opções](https://docs.microsoft.com/dotnet/core/extensions/options). No entanto, conforme observado no documento referenciado, esse padrão não deve ser usado no `ConfigureServices` . Em vez disso, o aplicativo portado fará referência ao `UseMockData` valor de configuração diretamente.

Primeiro, modifique o arquivo do aplicativo portado `appsettings.json` e adicione as duas configurações na raiz:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*",
  "UseMockData": "true",
  "UseCustomizationData" :  "true"
}
```

Agora, modifique `ConfigureServices` para acessar a `UseMockData` configuração da `Configuration` Propriedade (onde, anteriormente, definimos o valor como `true` ):

```csharp
  bool useMockData = Configuration.GetValue<bool>("UseMockData");
```

Neste ponto, a configuração é extraída da configuração. A outra configuração, `UseCustomizationData` , é usada pela `CatalogDBInitializer` classe. Ao portar essa classe pela primeira vez, você comentou o acesso ao `ConfigurationManager.AppSettings["UseCustomizationData"]` . Agora é hora de modificá-lo para usar ASP.NET Core configuração. Modifique o construtor de da seguinte `CatalogDBInitializer` maneira:

```csharp
  // add using Microsoft.Extensions.Configuration
  public CatalogDBInitializer(CatalogItemHiLoGenerator indexGenerator,
      IConfiguration configuration)
  {
      this.indexGenerator = indexGenerator;
      useCustomizationData = configuration.GetValue<bool>("UseCustomizationData");
  }
```

Todo o acesso à configuração no aplicativo Web deve ser modificado dessa maneira para usar o novo `IConfiguration` tipo. As dependências que exigem acesso ao .NET Framework configuração podem incluir essas configurações em um arquivo de *app.config* adicionado ao projeto Web. Os projetos dependentes podem trabalhar com o `ConfigurationManager` para acessar as configurações e não devem exigir alterações se já usarem essa abordagem. No entanto, como ASP.NET Core aplicativos são executados como seu próprio executável, eles não fazem referência a *web.config* , mas sim *app.config*. Ao migrar as configurações do arquivo de *web.config* do aplicativo herdado para um novo arquivo de *app.config* no aplicativo ASP.NET Core, os componentes que usam o `ConfigurationManager` para acessar suas configurações continuarão a funcionar corretamente.

A migração do aplicativo está quase concluída. A única tarefa restante é a configuração de acesso a dados.
  
## <a name="data-access-considerations"></a>Considerações de acesso a dados

ASP.NET Core aplicativos em execução no .NET Framework podem continuar a aproveitar Entity Framework (EF). Se estiver executando uma migração incremental, obter o aplicativo que funciona com o EF 6 antes de tentar portar seu acesso a dados para usar EF Core pode ser válido. Dessa forma, todos os problemas com a migração do aplicativo podem ser identificados e resolvidos antes que outro bloco de esforço de migração seja iniciado.

Como acontece, a configuração do EF 6 no exemplo eShop de migração não exige nenhum trabalho especial, pois esse trabalho foi realizado no Autofac `ApplicationModule` . O único problema é que, atualmente, a `CatalogDBContext` classe tenta ler sua cadeia de conexão de *web.config*. Para resolver isso, os detalhes da conexão precisam ser adicionados ao *appsettings.jsem*. Em seguida, a cadeia de conexão deve ser passada em `CatalogDBContext` quando ela é criada.

Atualize o *appsettings.jsem* para incluir a cadeia de conexão. O arquivo completo é listado aqui:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=eShopPorted;Trusted_Connection=True;MultipleActiveResultSets=true"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*",
  "UseMockData": "false",
  "UseCustomizationData": "true"
}
```

A cadeia de conexão deve ser passada para o Construtor quando o `DbContext` é criado. Como as instâncias são criadas pelo Autofac, a alteração precisa ser feita no `ApplicationModule` . Modifique o módulo a ser levado em um `connectionString` em seu construtor e atribua-o a um campo. Em seguida, modifique o registro para `CatalogDBContext` para adicionar a cadeia de conexão como um parâmetro:

```csharp
builder.RegisterType<CatalogDBContext>()
  .WithParameter("connectionString", _connectionString)
  .InstancePerLifetimeScope();
```

O parâmetro também deve ser adicionado a uma nova sobrecarga de Construtor em `CatalogDBContext` si próprio:

```csharp
public CatalogDBContext(string connectionString) : base(connectionString)
{
}
```

Por fim, `ConfigureServices` o deve ler a cadeia de conexão de `Config` e passá-la para `ApplicationModule` quando ela for instanciada:

```csharp
bool useMockData = Configuration.GetValue<bool>("UseMockData");
string connectionString = Configuration.GetConnectionString("DefaultConnection");
builder.RegisterModule(new ApplicationModule(useMockData, connectionString));
```

Com esse código em vigor, o aplicativo é executado como fazia antes, conectando-se a um banco de dados SQL Server quando `UseMockData` é `false` .

O aplicativo pode ser implantado e executado em produção neste ponto, convertido em ASP.NET Core, mas ainda em execução no .NET Framework e no EF 6. Se desejar, o aplicativo poderá ser migrado para ser executado no .NET Core e Entity Framework Core, o que trará vantagens adicionais descritas em capítulos anteriores. Específico do Entity Framework, [esta documentação compara EF Core e o EF 6](https://docs.microsoft.com/ef/efcore-and-ef6/) e inclui uma grade que mostra qual biblioteca dá suporte a cada um de dezenas de recursos individuais.

### <a name="migrate-to-entity-framework-core"></a>Migrar para o Entity Framework Core

Supondo que seja feita uma decisão de migrar para EF Core, as etapas podem ser bem simples, especialmente se o aplicativo original usava uma abordagem de modelo baseada em código. Ao se [preparar para a porta do EF 6 para EF Core](https://docs.microsoft.com/ef/efcore-and-ef6/porting/), examine a disponibilidade dos recursos na versão de destino do EF Core que você usará. Examine a documentação sobre [portabilidade e modelo baseado em EDMX](https://docs.microsoft.com/ef/efcore-and-ef6/porting/port-edmx) versus [portabilidade de um modelo baseado em código](https://docs.microsoft.com/ef/efcore-and-ef6/porting/port-code).

Para atualizar para o EF Core 2,2, as etapas básicas envolvidas são adicionar os pacotes do NuGet e os namespaces de atualização apropriados. Em seguida, ajuste como a cadeia de conexão é passada para o `DbContext` tipo e como ele está conectado para injeção de dependência.

EF Core é adicionado como uma referência de pacote ao projeto:

```xml
<PackageReference Include="Microsoft.EntityFrameworkCore" Version="2.2.6" />
```

A referência ao EF 6 é removida:

```xml
<PackageReference Include="EntityFramework" Version="6.2.0" />
```

O compilador relatará erros no `CatalogDBContext` e no `CatalogDBInitializer` . `CatalogDbContext` precisa ter os namespaces antigos removidos e substituídos por `Microsoft.EntityFrameworkCore` . Seus construtores podem ser removidos. `DbModelBuilder` deve ser substituído por `ModelBuilder` . Os métodos auxiliares para configurar tipos são movidos para classes separadas implementando `IEntityTypeConfiguration<T>` . Em seguida, o `CatalogDBContext` método da classe `OnModelCreating` simplesmente se torna:

```csharp
protected override void OnModelCreating(ModelBuilder builder)
{
    builder.ApplyConfigurationsFromAssembly(Assembly.GetExecutingAssembly());

    base.OnModelCreating(builder);
}
```

Outras alterações envolvidas incluem:

- `HasDatabaseGeneratedOption(DatabaseGeneratedOption.None)` substituído por `ValueGeneratedNever()`
- `HasRequired<T>` substituído por `HasOne<T>`
- `Microsoft.EntityFrameworkCore.Relational`Pacote instalado
- Adicionar um construtor para `CatalogDBContext` pegar `DbContextOptions` e passá-lo para o construtor base

Uma classe de configuração de exemplo para `CatalogType` é mostrada aqui:

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Metadata.Builders;

namespace eShopPorted.Models.Config
{
    public class CatalogTypeConfig : IEntityTypeConfiguration<CatalogType>
    {
        public void Configure(EntityTypeBuilder<CatalogType> builder)
        {
            builder.ToTable(nameof(CatalogType));

            builder.HasKey(ci => ci.Id);

            builder.Property(ci => ci.Id)
               .IsRequired();

            builder.Property(cb => cb.Type)
                .IsRequired()
                .HasMaxLength(100);
        }
    }
}
```

O `CatalogDBInitializer` e sua classe base, `CreateDatabaseIfNotExists<T>` , são incompatíveis com EF Core. A finalidade dessa classe é criar e propagar o banco de dados. Usar EF Core [criará e descartará o banco de `DbContext` dados associado para um](https://docs.microsoft.com/ef/core/managing-schemas/ensure-created) usando estes métodos:

```csharp
dbContext.Database.EnsureDeleted();
dbContext.Database.EnsureCreated();
```

A propagação de dados no EF Core pode ser feita com scripts manuais ou como parte da configuração do tipo. Junto com outras propriedades de entidade, os dados de semente podem ser configurados em `IEntityTypeConfiguration` classes usando o `builder.HasData()` . O aplicativo original carregou dados de semente de arquivos CSV no diretório de *instalação* . Considerando que há apenas alguns itens, esses registros de dados podem ser adicionados como parte da configuração da entidade. Essa abordagem funciona bem para dados de pesquisa em tabelas que são alteradas com pouca frequência. A adição do seguinte `CatalogTypeConfig` ao `Configure` método do garante que as linhas associadas estejam presentes quando o banco de dados for criado:

```csharp
builder.HasData(
    new CatalogType { Id = 1, Type = "Mug" },
    new CatalogType { Id = 2, Type = "T-Shirt" },
    new CatalogType { Id = 3, Type = "Sheet" },
    new CatalogType { Id = 4, Type = "USB Memory Stick" }
);
```

O aplicativo inicial inclui uma `PreconfiguredData` classe, que inclui dados para `CatalogBrand` e `CatalogType` , portanto, usando esse método, a `HasData` chamada reduz para:

```csharp
builder.HasData(
    PreconfiguredData.GetPreconfiguredCatalogBrands()
);
```

Os `CatalogItem` dados também podem ser extraídos `PreconfiguredData` e supondo que as imagens associadas sejam mantidas no controle do código-fonte, essa é a última tabela necessária para que o aplicativo funcione. A `CatalogDBInitializer` classe pode ser removida, juntamente com todas as referências a ela. A `CatalogItemHiLoGenerator` classe e os arquivos SQL no `Infrastructure` diretório também são removidos, juntamente com todas as referências a eles (no `CatalogService` , `ApplicationModule` ).

Com a eliminação das classes especiais do gerador de chave para `CatalogItem` , esse código agora é removido de `CatalogItemConfig` :

```csharp
builder.Property(ci => ci.Id)
    .ValueGeneratedNever()
    .IsRequired();
```

Com essas modificações, o aplicativo ASP.NET Core compila, mas ainda não funciona com EF Core, o que ainda deve ser configurado para injeção de dependência. Com o EF Core, a maneira mais simples de configurá-lo é `ConfigureServices` :

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    bool useMockData = Configuration.GetValue<bool>("UseMockData");
    if (!useMockData)
    {
        string connectionString = Configuration.GetConnectionString("DefaultConnection");

        services.AddDbContext<CatalogDBContext>(options =>
            options.UseSqlServer(connectionString)
        );
    }

    // Create Autofac container builder
    var builder = new ContainerBuilder();
    builder.Populate(services);
    builder.RegisterModule(new ApplicationModule(useMockData));

    ILifetimeScope container = builder.Build();

    return new AutofacServiceProvider(container);
}
```

A versão final do Autofac `ApplicationModule` configura apenas um tipo, dependendo se o aplicativo está configurado para usar dados fictícios:

```csharp
public class ApplicationModule : Module
{
    private bool _useMockData;

    public ApplicationModule(bool useMockData)
    {
        _useMockData = useMockData;
    }
    
    protected override void Load(ContainerBuilder builder)
    {
        if (_useMockData)
        {
            builder.RegisterType<CatalogServiceMock>()
                .As<ICatalogService>()
                .SingleInstance();
        }
        else
        {
            builder.RegisterType<CatalogService>()
                .As<ICatalogService>()
                .InstancePerLifetimeScope();
        }
    }
}
```

O aplicativo portado é executado, mas não exibe nenhum dado se estiver configurado para usar dados não fictícios. Os dados de semente adicionados por meio do `HasData` só são inseridos quando as migrações são aplicadas. O aplicativo de origem não usou migrações e, se ela tinha, não migraria como está. A melhor abordagem é iniciar com um novo script de migração. Para fazer isso, adicione uma referência de pacote para `Microsoft.EntityFrameworkCore.Design` e abra uma janela de terminal na raiz do projeto. Em seguida, execute:

```dotnetcli
dotnet ef migrations add Initial
```

Descartar o banco de dados *eShopPorted* existente se ele existir, em seguida, execute:

```dotnetcli
dotnet ef database update
```

Isso cria e propaga o banco de dados. Agora ele está pronto para ser executado, com algumas pequenas atualizações restantes para resolver.

## <a name="fix-all-todo-tasks"></a>Corrigir todas as tarefas TODO

A execução do aplicativo portado neste ponto revela que nenhuma imagem é mostrada na página. Isso ocorre porque a `PictureUri` propriedade de `CatalogItem` nunca é definida. Observando a lista de `TODO` itens que criamos usando o **lista de tarefas** do Visual Studio, o único que resta está em `CatalogController` , com uma nota para "Reference pic from wwwroot". O código em questão é:

```csharp
private void AddUriPlaceHolder(CatalogItem item)
{
    //TODO: Reference pic from wwwroot
    //item.PictureUri = this.Url.RouteUrl(PicController.GetPicRouteName, new { catalogItemId = item.Id }, this.Request.Url.Scheme);
}
```

A correção mais simples é fazer referência aos arquivos de imagem pública no diretório *wwwroot/pics* público do site. Essa tarefa pode ser realizada substituindo o método pelo código a seguir:

```csharp
private void AddUriPlaceHolder(CatalogItem item)
{
    item.PictureUri = $"/Pics/{item.Id}.png";
}
```

Com essa alteração, a execução do aplicativo revela que as imagens funcionam como antes.

## <a name="additional-mvc-customizations"></a>Personalizações adicionais do MVC

O aplicativo *eShopLegacyMVC* é bastante simples, portanto, não há muito a ser configurado em termos de comportamento padrão do MVC. No entanto, se você precisar configurar componentes MVC adicionais, como CORS, filtros e restrições de rota, geralmente fornece essas informações em `Startup.ConfigureServices` , onde `UseMvc` é chamado. Por exemplo, a listagem de código a seguir configura o [CORS](https://docs.microsoft.com/aspnet/core/security/cors?view=aspnetcore-2.2&preserve-view=true) e configura um filtro de ação global:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy(MyAllowSpecificOrigins,
            builder =>
                builder.WithOrigins("http://example.com", "http://www.contoso.com")
                    .AllowAnyHeader()
                    .AllowAnyMethod());
    });

    services.AddMvc(options =>
    {
      options.Filters.Add(new SampleGlobalActionFilter());
    }).SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
}
```

> [!Note]
> Para concluir a configuração do CORS, você também deve chamar `app.UseCors()` `Configure` .

Outros cenários avançados, como adicionar [ASSOCIADORES de modelo personalizados](https://docs.microsoft.com/aspnet/core/mvc/advanced/custom-model-binding?view=aspnetcore-2.2&preserve-view=true), formatadores e muito mais, são abordados no ASP.NET Core documentos detalhados. Geralmente, eles podem ser aplicados em um controlador individual ou em uma base de ação ou, globalmente, usando a mesma abordagem de opções mostrada na listagem de código anterior.

## <a name="other-dependencies"></a>Outras dependências

As dependências que usam .NET Framework recursos que tinham uma dependência no modelo de configuração herdado, como o tipo de cliente do WCF e o código de rastreamento, devem ser modificadas quando portadas. Em vez de fazer com que esses tipos recebam suas informações de configuração diretamente, eles devem ser configurados no código. Por exemplo, uma conexão com um serviço WCF que foi configurada em uma *web.config* do aplicativo ASP.net para uso `basicHttpBinding` pode ser configurada programaticamente com o seguinte código:

```csharp
var binding = new BasicHttpBinding();
binding.MaxReceivedMessageSize = 2_000_000;

var endpointAddress = new EndpointAddress("http://localhost:9200/ExampleService");

var myClient = new MyServiceClient(binding, endpointAddress);
```

Em vez de depender de arquivos de configuração para suas configurações, os clientes WCF e outros tipos de .NET Framework devem ter suas configurações especificadas no código. Configurado dessa maneira, esses tipos podem continuar a funcionar em ASP.NET Core aplicativos 2,2.

## <a name="references"></a>Referências

- [repositório GitHub do eShopModernizing](https://github.com/dotnet-architecture/eShopModernizing)
- [Sua API e ViewModels não devem referenciar modelos de domínio](https://ardalis.com/your-api-and-view-models-should-not-reference-domain-models/)
- [Middleware de página de exceção do desenvolvedor](https://docs.microsoft.com/aspnet/core/fundamentals/error-handling#developer-exception-page)
- [Aprofunde-se no EF Core HasData](https://docs.microsoft.com/archive/msdn-magazine/2018/august/data-points-deep-dive-into-ef-core-hasdata-seeding)

>[!div class="step-by-step"]
>[Anterior](strategies-migrating-in-production.md) 
> [Avançar](deployment-scenarios.md)
