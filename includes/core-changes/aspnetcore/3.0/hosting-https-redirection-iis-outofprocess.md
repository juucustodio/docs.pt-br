---
ms.openlocfilehash: eb3fa768a491f6c0ff4b15479beabd71b0670338
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032238"
---
### <a name="hosting-https-redirection-enabled-for-iis-out-of-process-apps"></a>Hospedagem: redirecionamento de HTTPS habilitado para aplicativos fora do processo do IIS

A versão 13.0.19218.0 do [módulo de ASP.NET Core (ANCM)](/aspnet/core/host-and-deploy/aspnet-core-module) para hospedagem via IIS fora do processo habilita um recurso de redirecionamento de HTTPS existente para aplicativos ASP.NET Core 3,0 e 2,2.

Para obter uma discussão, consulte [dotnet/AspNetCore # 15243](https://github.com/dotnet/AspNetCore/issues/15243).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

O modelo de projeto ASP.NET Core 2,1 introduziu primeiro o suporte para métodos de middleware HTTPS como <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection%2A> e <xref:Microsoft.AspNetCore.Builder.HstsBuilderExtensions.UseHsts%2A> . Habilitar o redirecionamento de HTTPS exigiu a adição de configuração, já que os aplicativos em desenvolvimento não usam a porta padrão de 443. A [HSTS (segurança de transporte estrito) http](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html) estará ativa somente se a solicitação já estiver usando HTTPS. O localhost é ignorado por padrão.

#### <a name="new-behavior"></a>Novo comportamento

No ASP.NET Core 3,0, o cenário HTTPS do IIS foi [aprimorado](https://github.com/dotnet/AspNetCore/pull/4685). Com o aprimoramento, um aplicativo poderia descobrir as portas HTTPS do servidor e tornar o `UseHttpsRedirection` trabalho por padrão. O componente em processo realizou a descoberta de porta com o `IServerAddresses` recurso, que afeta apenas ASP.NET Core aplicativos 3,0 porque a biblioteca em processo tem controle de versão com a estrutura. O componente fora do processo foi alterado para adicionar automaticamente a `ASPNETCORE_HTTPS_PORT` variável de ambiente. Essa alteração afetou os aplicativos ASP.NET Core 2,2 e 3,0 porque o componente fora do processo é compartilhado globalmente. ASP.NET Core aplicativos 2,1 não são afetados porque usam uma versão anterior do ANCM por padrão.

O comportamento anterior foi modificado no ASP.NET Core 3.0.1 e no 3.1.0 Preview 3 para reverter as alterações de comportamento no ASP.NET Core 2. x. Essas alterações afetam apenas os aplicativos fora do processo do IIS.

Conforme detalhado acima, instalar ASP.NET Core 3.0.0 tinha o efeito colateral de também ativar o `UseHttpsRedirection` middleware em aplicativos ASP.NET Core 2. x. Foi feita uma alteração no ANCM no ASP.NET Core 3.0.1 e no 3.1.0 Preview 3, de forma que instalá-los não tenha mais esse efeito em aplicativos ASP.NET Core 2. x. A `ASPNETCORE_HTTPS_PORT` variável de ambiente que o ANCM populau em ASP.NET Core 3.0.0 foi alterada para `ASPNETCORE_ANCM_HTTPS_PORT` no ASP.NET Core 3.0.1 e 3.1.0 Preview 3. `UseHttpsRedirection` também foi atualizado nessas versões para entender as variáveis novas e antigas. O ASP.NET Core 2. x não será atualizado. Como resultado, ele reverte para o comportamento anterior de ser desabilitado por padrão.

#### <a name="reason-for-change"></a>Motivo da alteração

Funcionalidade do ASP.NET Core 3,0 aprimorada.

#### <a name="recommended-action"></a>Ação recomendada

Nenhuma ação será necessária se você quiser que todos os clientes usem HTTPS. Para permitir que alguns clientes usem HTTP, execute uma das seguintes etapas:

* Remova as chamadas de `UseHttpsRedirection` e para `UseHsts` o método do projeto `Startup.Configure` e reimplante o aplicativo.
* No arquivo *web.config* , defina a `ASPNETCORE_HTTPS_PORT` variável de ambiente como uma cadeia de caracteres vazia. Essa alteração pode ocorrer diretamente no servidor sem reimplantar o aplicativo. Por exemplo:

    ```xml
    <aspNetCore processPath="dotnet" arguments=".\WebApplication3.dll" stdoutLogEnabled="false" stdoutLogFile="\\?\%home%\LogFiles\stdout" >
        <environmentVariables>
        <environmentVariable name="ASPNETCORE_HTTPS_PORT" value="" />
        </environmentVariables>
    </aspNetCore>
    ```

`UseHttpsRedirection` ainda pode ser:

* Ativado manualmente no ASP.NET Core 2. x definindo a `ASPNETCORE_HTTPS_PORT` variável de ambiente para o número de porta apropriado (443 na maioria dos cenários de produção).
* Desativado no ASP.NET Core 3. x definindo `ASPNETCORE_ANCM_HTTPS_PORT` com um valor de cadeia de caracteres vazia. Esse valor é definido da mesma maneira que o exemplo anterior `ASPNETCORE_HTTPS_PORT` .

Máquinas que executam ASP.NET Core aplicativos 3.0.0 devem instalar o ASP.NET Core 3.0.1 Runtime antes de instalar o ASP.NET Core 3.1.0 Preview 3 ANCM. Isso garante que `UseHttpsRedirection` o Continue a operar conforme o esperado para os aplicativos ASP.NET Core 3,0.

No Azure App Service, o ANCM é implantado em um agendamento separado do tempo de execução devido à sua natureza global. O ANCM foi implantado no Azure com essas alterações após a implantação do ASP.NET Core 3.0.1 e do 3.1.0.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection(Microsoft.AspNetCore.Builder.IApplicationBuilder)?displayProperty=nameWithType>

<!-- 

#### Affected APIs

`M:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection(Microsoft.AspNetCore.Builder.IApplicationBuilder)`

-->
