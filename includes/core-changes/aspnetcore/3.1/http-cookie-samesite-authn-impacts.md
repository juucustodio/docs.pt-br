---
ms.openlocfilehash: 8b6d334677991382d235fd53cd3c98e3a77d650d
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032224"
---
### <a name="http-browser-samesite-changes-impact-authentication"></a>HTTP: navegador SameSite alterações de impacto na autenticação

Alguns navegadores, como Chrome e Firefox, fizeram alterações interruptivas nas respectivas implementações de `SameSite` para cookies. As alterações afetam os cenários de autenticação remota, como OpenID Connect e WS-Federation, que devem ser recusadas enviando `SameSite=None` . No entanto, o `SameSite=None` interrompe o IOS 12 e algumas versões mais antigas de outros navegadores. O aplicativo precisa farejar essas versões e omitir `SameSite` .

Para obter uma discussão sobre esse problema, consulte [dotnet/aspnetcore # 14996](https://github.com/dotnet/aspnetcore/issues/14996).

#### <a name="version-introduced"></a>Versão introduzida

3,1 visualização 1

#### <a name="old-behavior"></a>Comportamento antigo

`SameSite` é uma extensão padrão de rascunho 2016 para cookies HTTP. Ele se destina a reduzir a falsificação de solicitação entre sites (CSRF). Isso foi originalmente projetado como um recurso que os servidores optaram por adicionar os novos parâmetros. ASP.NET Core 2,0 adicionou suporte inicial para `SameSite` .

#### <a name="new-behavior"></a>Novo comportamento

O Google propôs um novo padrão de rascunho que não é compatível com versões anteriores. O padrão altera o modo padrão para `Lax` e adiciona uma nova entrada `None` a ser recusada. `Lax` é suficiente para a maioria dos cookies de aplicativo; no entanto, ele quebra cenários entre sites como o OpenID Connect e WS-Federation logon. A maioria dos logons OAuth não é afetada devido a diferenças em como a solicitação flui. O novo `None` parâmetro causa problemas de compatibilidade com clientes que implementaram o rascunho padrão anterior (por exemplo, IOS 12). O Chrome 80 incluirá as alterações. Consulte [atualizações do SameSite](https://www.chromium.org/updates/same-site) para a linha do tempo de lançamento do produto Chrome.

ASP.NET Core 3,1 foi atualizado para implementar o novo `SameSite` comportamento. A atualização redefine o comportamento de `SameSiteMode.None` para emissão `SameSite=None` e adiciona um novo valor `SameSiteMode.Unspecified` para omitir o `SameSite` atributo. Todas as APIs de cookie agora são padronizadas para `Unspecified` , embora alguns componentes que usam os cookies definam valores mais específicos para seus cenários, como a correlação do OpenID Connect e os cookies de nonce.

Para outras alterações recentes nessa área, consulte [http: alguns padrões de SameSite de cookie foram alterados para nenhum](../../../../docs/core/compatibility/2.2-3.0.md#http-some-cookie-samesite-defaults-changed-to-none). No ASP.NET Core 3,0, a maioria dos padrões foi alterada de <xref:Microsoft.AspNetCore.Http.SameSiteMode.Lax?displayProperty=nameWithType> para <xref:Microsoft.AspNetCore.Http.SameSiteMode.None?displayProperty=nameWithType> (mas ainda usando o padrão anterior).

#### <a name="reason-for-change"></a>Motivo da alteração

Alterações de navegador e especificação, conforme descrito no texto anterior.

#### <a name="recommended-action"></a>Ação recomendada

Os aplicativos que interagem com sites remotos, como por logon de terceiros, precisam:

* Teste esses cenários em vários navegadores.
* Aplique o navegador de política de cookie a mitigação de detecção discutida em [suporte a navegadores mais antigos](#support-older-browsers).

Para testar e obter instruções de detecção de navegador, consulte a seção a seguir.

##### <a name="determine-if-youre-affected"></a>Determine se você é afetado

Teste seu aplicativo Web usando uma versão do cliente que pode optar pelo novo comportamento. O Chrome, o Firefox e o Microsoft Edge Chromium têm novos sinalizadores de recurso de aceitação que podem ser usados para teste. Verifique se seu aplicativo é compatível com versões mais antigas do cliente depois de aplicar os patches, especialmente o Safari. Para obter mais informações, consulte [suporte a navegadores mais antigos](#support-older-browsers).

##### <a name="chrome"></a>Chrome

O Chrome 78 e posterior geram resultados de teste enganosos. Essas versões têm uma mitigação temporária em vigor e permitem cookies com menos de dois minutos de idade. Com os sinalizadores de teste apropriados habilitados, o Chrome 76 e o 77 geram resultados mais precisos. Para testar o novo comportamento, alterne `chrome://flags/#same-site-by-default-cookies` para habilitado. O Chrome 75 e versões anteriores são relatados para falha com a nova `None` configuração. Para obter mais informações, consulte [suporte a navegadores mais antigos](#support-older-browsers).

O Google não disponibiliza versões mais antigas do Chrome. No entanto, você pode baixar versões mais antigas do Chromium, o que será suficiente para teste. Siga as instruções em [baixar o Chromium](https://www.chromium.org/getting-involved/download-chromium).

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

##### <a name="safari"></a>Safari

O Safari 12 implementou estritamente o rascunho anterior e falha se ele vê o novo `None` valor em cookies. Isso deve ser evitado por meio do código de detecção do navegador mostrado em [suporte a navegadores mais antigos](#support-older-browsers). Certifique-se de testar o Safari 12 e 13, bem como OS logons de estilo do sistema operacional baseados em WebKit usando a MSAL (biblioteca de autenticação da Microsoft), a ADAL (Biblioteca de Autenticação do Active Directory) ou qualquer biblioteca que você esteja usando. O problema depende da versão subjacente do sistema operacional. O OSX Mojave 10,14 e o iOS 12 são conhecidos por ter problemas de compatibilidade com o novo comportamento. A atualização para OSX Catalina 10,15 ou iOS 13 corrige o problema. No momento, o Safari não tem um sinalizador de aceitação para testar o novo comportamento de especificação.

##### <a name="firefox"></a>Firefox

O suporte do Firefox para o novo padrão pode ser testado na versão 68 e posterior, optando na `about:config` página pelo sinalizador de recurso `network.cookie.sameSite.laxByDefault` . Nenhum problema de compatibilidade foi relatado em versões mais antigas do Firefox.

##### <a name="microsoft-edge"></a>Microsoft Edge

Embora o Microsoft Edge dê suporte ao antigo `SameSite` padrão, a partir da versão 44, não havia nenhum problema de compatibilidade com o novo padrão.

##### <a name="microsoft-edge-chromium"></a>Chromium do Microsoft Edge

O sinalizador de recurso é `edge://flags/#same-site-by-default-cookies` . Nenhum problema de compatibilidade foi observado durante o teste com o Microsoft Edge Chromium 78.

##### <a name="electron"></a>Digital

As versões do at-SS são versões mais antigas do Chromium. Por exemplo, a versão do at-SS de uso da Microsoft Teams é Chromium 66, que exibe o comportamento mais antigo. Execute seus próprios testes de compatibilidade com a versão do uso de digital que seu produto usa. Para obter mais informações, consulte [suporte a navegadores mais antigos](#support-older-browsers).

##### <a name="support-older-browsers"></a>Suporte a navegadores mais antigos

O `SameSite` padrão 2016 obrigatório que valores desconhecidos sejam tratados como `SameSite=Strict` valores. Consequentemente, todos os navegadores mais antigos que dão suporte ao padrão original podem ser interrompidos quando veem uma `SameSite` propriedade com um valor de `None` . Os aplicativos Web devem implementar a detecção de navegador se pretenderem dar suporte a esses navegadores antigos. ASP.NET Core não implementa a detecção de navegador para você porque `User-Agent` os valores de cabeçalho de solicitação são altamente instáveis e mudam semanalmente. Em vez disso, um ponto de extensão na política de cookie permite que você adicione `User-Agent` lógica específica.

No *Startup.cs*, adicione o seguinte código:

```csharp
private void CheckSameSite(HttpContext httpContext, CookieOptions options)
{
    if (options.SameSite == SameSiteMode.None)
    {
        var userAgent = httpContext.Request.Headers["User-Agent"].ToString();
        // TODO: Use your User Agent library of choice here.
        if (/* UserAgent doesn't support new behavior */)
        {
            options.SameSite = SameSiteMode.Unspecified;
        }
    }
}

public void ConfigureServices(IServiceCollection services)
{
    services.Configure<CookiePolicyOptions>(options =>
    {
        options.MinimumSameSitePolicy = SameSiteMode.Unspecified;
        options.OnAppendCookie = cookieContext =>
            CheckSameSite(cookieContext.Context, cookieContext.CookieOptions);
        options.OnDeleteCookie = cookieContext =>
            CheckSameSite(cookieContext.Context, cookieContext.CookieOptions);
    });
}

public void Configure(IApplicationBuilder app)
{
    // Before UseAuthentication or anything else that writes cookies.
    app.UseCookiePolicy();

    app.UseAuthentication();
    // code omitted for brevity
}
```

##### <a name="opt-out-switches"></a>Opções de recusa

A `Microsoft.AspNetCore.SuppressSameSiteNone` opção de compatibilidade permite recusar temporariamente o novo comportamento de cookie ASP.NET Core. Adicione o JSON a seguir a um *runtimeconfig.template.jsno* arquivo em seu projeto:

```json
{
  "configProperties": {
    "Microsoft.AspNetCore.SuppressSameSiteNone": "true"
  }
}
```

##### <a name="other-versions"></a>Outras versões

`SameSite`Patches relacionados estão prestes a:

* ASP.NET Core 2,1, 2,2 e 3,0
* `Microsoft.Owin` 4,1
* `System.Web` (para .NET Framework 4.7.2 e posterior)

#### <a name="category"></a>Categoria

ASP.NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Builder.CookiePolicyOptions.MinimumSameSitePolicy%2A?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Http.CookieBuilder.SameSite%2A?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite%2A?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Http.SameSiteMode?displayProperty=fullName>
- <xref:Microsoft.Net.Http.Headers.SameSiteMode?displayProperty=fullName>
- <xref:Microsoft.Net.Http.Headers.SetCookieHeaderValue.SameSite%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `Overload:Microsoft.AspNetCore.Builder.CookiePolicyOptions.MinimumSameSitePolicy`
- `Overload:Microsoft.AspNetCore.Http.CookieBuilder.SameSite`
- `Overload:Microsoft.AspNetCore.Http.CookieOptions.SameSite`
- `T:Microsoft.AspNetCore.Http.SameSiteMode`
- `T:Microsoft.Net.Http.Headers.SameSiteMode`
- `Overload:Microsoft.Net.Http.Headers.SetCookieHeaderValue.SameSite`

-->
