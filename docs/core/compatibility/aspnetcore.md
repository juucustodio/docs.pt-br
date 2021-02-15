---
title: Alterações interruptivas do ASP.NET Core
titleSuffix: ''
description: Lista as alterações interruptivas no ASP.NET Core 3.0 e 3.1.
ms.date: 11/03/2020
author: scottaddie
ms.author: scaddie
ms.openlocfilehash: 40dfda77dd51ed46366ec6cd8f6598070e8ce846
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "96032223"
---
# <a name="aspnet-core-breaking-changes-for-versions-30-and-31"></a>Alterações interruptivas no ASP.NET Core para as versões 3.0 e 3.1

ASP.NET Core fornece os recursos de desenvolvimento de aplicativo Web usados pelo .NET Core.

Selecione um dos seguintes links para alterações interruptivas em uma versão específica:

* [ASP.NET Core 3,1](#aspnet-core-31)
* [ASP.NET Core 3,0](#aspnet-core-30)

As seguintes alterações interruptivas no ASP.NET Core 3.0 e 3.1 estão documentadas nesta página:

- [APIs antifalsificação obsoletas, CORS, diagnóstico, MVC e roteamento removidas](#obsolete-antiforgery-cors-diagnostics-mvc-and-routing-apis-removed)
- [Autenticação: Google + substituição](#authentication-google-deprecated-and-replaced)
- [Autenticação: Propriedade HttpContext. Authentication removida](#authentication-httpcontextauthentication-property-removed)
- [Autenticação: Newtonsoft.Jsem tipos substituídos](#authentication-newtonsoftjson-types-replaced)
- [Autenticação: assinatura OAuthHandler ExchangeCodeAsync alterada](#authentication-oauthhandler-exchangecodeasync-signature-changed)
- [Autorização: sobrecarga de addautoria movida para um assembly diferente](#authorization-addauthorization-overload-moved-to-different-assembly)
- [Autorização: IAllowAnonymous removido de AuthorizationFilterContext. Filters](#authorization-iallowanonymous-removed-from-authorizationfiltercontextfilters)
- [Autorização: implementações de IAuthorizationPolicyProvider exigem novo método](#authorization-iauthorizationpolicyprovider-implementations-require-new-method)
- [Caching: Propriedade CompactOnMemoryPressure removida](#caching-compactonmemorypressure-property-removed)
- [Caching: o Microsoft. Extensions. Caching. SqlServer usa o novo pacote SqlClient](#caching-microsoftextensionscachingsqlserver-uses-new-sqlclient-package)
- [Proteção de dados: dataprotegetion. BLOBs usa novas APIs de armazenamento do Azure](#data-protection-dataprotectionblobs-uses-new-azure-storage-apis)
- [Hospedagem: AspNetCoreModule v1 removido do pacote de hospedagem do Windows](#hosting-aspnetcoremodule-v1-removed-from-windows-hosting-bundle)
- [Hospedagem: host genérico restringe injeção de construtor de inicialização](#hosting-generic-host-restricts-startup-constructor-injection)
- [Hospedagem: redirecionamento de HTTPS habilitado para aplicativos fora do processo do IIS](#hosting-https-redirection-enabled-for-iis-out-of-process-apps)
- [Hospedagem: tipos IHostingEnvironment e IApplicationLifetime substituídos](#hosting-ihostingenvironment-and-iapplicationlifetime-types-marked-obsolete-and-replaced)
- [Hospedagem: objectpoolprovider removido de dependências WebHostBuilder](#hosting-objectpoolprovider-removed-from-webhostbuilder-dependencies)
- [HTTP: navegador SameSite alterações de impacto na autenticação](#http-browser-samesite-changes-impact-authentication)
- [HTTP: extensibilidade defaulthttpcontext removida](#http-defaulthttpcontext-extensibility-removed)
- [Campos HTTP: Headernames alterados para static readonly](#http-headernames-constants-changed-to-static-readonly)
- [HTTP: alterações de infraestrutura de corpo de resposta](#http-response-body-infrastructure-changes)
- [HTTP: alguns SameSite de cookie foram alterados valores padrão](#http-some-cookie-samesite-defaults-changed-to-none)
- [HTTP: e/s síncrona desabilitada por padrão](#http-synchronous-io-disabled-in-all-servers)
- [Identidade: sobrecarga do método AddDefaultUI removida](#identity-adddefaultui-method-overload-removed)
- [Identidade: alteração da versão de inicialização da interface do usuário](#identity-default-bootstrap-version-of-ui-changed)
- [Identidade: o SignInAsync gera uma exceção para a identidade não autenticada](#identity-signinasync-throws-exception-for-unauthenticated-identity)
- [Identity: o Construtor SignInManager aceita o novo parâmetro](#identity-signinmanager-constructor-accepts-new-parameter)
- [Identidade: a interface do usuário usa o recurso de ativos da Web estáticos](#identity-ui-uses-static-web-assets-feature)
- [Kestrel: adaptadores de conexão removidos](#kestrel-connection-adapters-removed)
- [Kestrel: assembly HTTPS vazio removido](#kestrel-empty-https-assembly-removed)
- [Kestrel: Solicitar cabeçalhos de trailer movidos para nova coleção](#kestrel-request-trailer-headers-moved-to-new-collection)
- [Kestrel: alterações na camada de abstração de transporte](#kestrel-transport-abstractions-removed-and-made-public)
- [Localização: APIs marcadas como obsoletas](#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)
- [Log: classe DebugLogger criada internamente](#logging-debuglogger-class-made-internal)
- [MVC: sufixo assíncrono de ação do controlador removido](#mvc-async-suffix-trimmed-from-controller-action-names)
- [MVC: JsonResult movido para Microsoft. AspNetCore. Mvc. Core](#mvc-jsonresult-moved-to-microsoftaspnetcoremvccore)
- [MVC: ferramenta de pré-compilação preterida](#mvc-precompilation-tool-deprecated)
- [MVC: tipos alterados para interno](#mvc-pubternal-types-changed-to-internal)
- [MVC: Shim de compatibilidade da API Web removido](#mvc-web-api-compatibility-shim-removed)
- [Razor: API RazorTemplateEngine removida](#razor-razortemplateengine-api-removed)
- [Razor: compilação de tempo de execução movida para um pacote](#razor-runtime-compilation-moved-to-a-package)
- [Estado da sessão: APIs obsoletas removidas](#session-state-obsolete-apis-removed)
- [Estrutura compartilhada: remoção de assembly do Microsoft. AspNetCore. app](#shared-framework-assemblies-removed-from-microsoftaspnetcoreapp)
- [Estrutura compartilhada: Microsoft. AspNetCore. All removidas](#shared-framework-removed-microsoftaspnetcoreall)
- [Signalr: HandshakeProtocol. SuccessHandshakeData substituído](#signalr-handshakeprotocolsuccesshandshakedata-replaced)
- [Signalr: métodos HubConnection removidos](#signalr-hubconnection-resetsendping-and-resettimeout-methods-removed)
- [Signalr: construtores HubConnectionContext alterados](#signalr-hubconnectioncontext-constructors-changed)
- [Signalr: alteração de nome de pacote de cliente JavaScript](#signalr-javascript-client-package-name-changed)
- [Signalr: APIs obsoletas](#signalr-usesignalr-and-useconnections-methods-marked-obsolete)
- [SPAs: SpaServices e Nodeservices console agente de fallback alterar padrão](#spas-spaservices-and-nodeservices-no-longer-fall-back-to-console-logger)
- [SPAs: SpaServices e Nodeservices marcados como obsoletos](#spas-spaservices-and-nodeservices-marked-obsolete)
- [Estrutura de destino: .NET Framework sem suporte](#target-framework-net-framework-support-dropped)

## <a name="aspnet-core-31"></a>ASP.NET Core 3,1

[!INCLUDE[HTTP: Browser SameSite changes impact authentication](~/includes/core-changes/aspnetcore/3.1/http-cookie-samesite-authn-impacts.md)]

***

## <a name="aspnet-core-30"></a>ASP.NET Core 3,0

[!INCLUDE[Obsolete Antiforgery, CORS, Diagnostics, MVC, and Routing APIs removed](~/includes/core-changes/aspnetcore/3.0/obsolete-apis-removed.md)]

**_

[!INCLUDE[Authentication: Google+ deprecation](~/includes/core-changes/aspnetcore/3.0/authn-google-plus-authn-changes.md)]

_*_

[!INCLUDE[Authentication: HttpContext.Authentication property removed](~/includes/core-changes/aspnetcore/3.0/authn-httpcontext-property-removed.md)]

_*_

[!INCLUDE[Authentication: Newtonsoft.Json types replaced](~/includes/core-changes/aspnetcore/3.0/authn-apis-json-types.md)]

_*_

[!INCLUDE[Authentication: OAuthHandler ExchangeCodeAsync signature changed](~/includes/core-changes/aspnetcore/3.0/authn-exchangecodeasync-signature-change.md)]

_*_

[!INCLUDE[Authorization: AddAuthorization overload assembly change](~/includes/core-changes/aspnetcore/3.0/authz-assembly-change.md)]

_*_

[!INCLUDE[Authorization: IAllowAnonymous removed from AuthorizationFilterContext.Filters](~/includes/core-changes/aspnetcore/3.0/authz-iallowanonymous-removed-from-collection.md)]

_*_

[!INCLUDE[Authorization: IAuthorizationPolicyProvider implementations require new method](~/includes/core-changes/aspnetcore/3.0/authz-iauthzpolicyprovider-new-method.md)]

_*_

[!INCLUDE[Caching: CompactOnMemoryPressure property removed](~/includes/core-changes/aspnetcore/3.0/caching-memory-property-removed.md)]

_*_

[!INCLUDE[Caching: Microsoft.Extensions.Caching.SqlServer uses new SqlClient package](~/includes/core-changes/aspnetcore/3.0/caching-new-sqlclient-package.md)]

_*_

[!INCLUDE[Caching: ResponseCaching types changed to internal](~/includes/core-changes/aspnetcore/3.0/caching-response-pubternal-to-internal.md)]

_*_

[!INCLUDE[Data Protection: DataProtection.AzureStorage uses new Azure Storage APIs](~/includes/core-changes/aspnetcore/3.0/dataprotection-azstorage-using-azstorage-apis.md)]

_*_

[!INCLUDE[Hosting: ANCM version 1 removed from hosting bundle](~/includes/core-changes/aspnetcore/3.0/hosting-ancmv1-hosting-bundle-removal.md)]

_*_

[!INCLUDE[Hosting: Generic host restriction on Startup constructor injection](~/includes/core-changes/aspnetcore/3.0/hosting-generic-host-startup-ctor-restriction.md)]

_*_

[!INCLUDE[Hosting: HTTPS redirection enabled for IIS OutOfProcess](~/includes/core-changes/aspnetcore/3.0/hosting-https-redirection-iis-outofprocess.md)]

_*_

[!INCLUDE[Hosting: IHostingEnvironment and IApplicationLifetime types replaced](~/includes/core-changes/aspnetcore/3.0/hosting-ihostingenv-iapplifetime-types-replaced.md)]

_*_

[!INCLUDE[Hosting: ObjectPoolProvider removed from WebHostBuilder dependencies](~/includes/core-changes/aspnetcore/3.0/hosting-objectpoolprovider-webhostbuilder-dependencies.md)]

_*_

[!INCLUDE[HTTP: DefaultHttpContext extensibility removed](~/includes/core-changes/aspnetcore/3.0/http-defaulthttpcontext-extensibility-removed.md)]

_*_

[!INCLUDE[HTTP: HeaderNames fields changed to static readonly](~/includes/core-changes/aspnetcore/3.0/http-headernames-constants-staticreadonly.md)]

_*_

[!INCLUDE[HTTP: Response body infrastructure changes](~/includes/core-changes/aspnetcore/3.0/http-response-body-changes.md)]

_*_

[!INCLUDE[HTTP: Some cookie SameSite default values changed](~/includes/core-changes/aspnetcore/3.0/http-cookie-samesite-defaults-change.md)]

_*_

[!INCLUDE[HTTP: Synchronous IO disabled by default](~/includes/core-changes/aspnetcore/3.0/http-synchronous-io-disabled.md)]

_*_

[!INCLUDE[Identity: AddDefaultUI method overload removed](~/includes/core-changes/aspnetcore/3.0/identity-ui-adddefaultui-overload-removed.md)]

_*_

[!INCLUDE[Identity: UI Bootstrap version change](~/includes/core-changes/aspnetcore/3.0/identity-ui-bootstrap-version.md)]

_*_

[!INCLUDE[Identity: SignInAsync throws exception for unauthenticated identity](~/includes/core-changes/aspnetcore/3.0/identity-signinasync-throws-exception.md)]

_*_

[!INCLUDE[Identity: SignInManager constructor accepts new parameter](~/includes/core-changes/aspnetcore/3.0/identity-signinmanager-ctor-parameter.md)]

_*_

[!INCLUDE[Identity: UI uses static web assets feature](~/includes/core-changes/aspnetcore/3.0/identity-ui-static-web-assets.md)]

_*_

[!INCLUDE[Kestrel: Connection adapters removed](~/includes/core-changes/aspnetcore/3.0/kestrel-connection-adapters-removed.md)]

_*_

[!INCLUDE[Kestrel: Empty HTTPS assembly removed](~/includes/core-changes/aspnetcore/3.0/kestrel-empty-assembly-removed.md)]

_*_

[!INCLUDE[Kestrel: Request trailer headers moved to new collection](~/includes/core-changes/aspnetcore/3.0/kestrel-request-trailer-headers.md)]

_*_

[!INCLUDE[Kestrel: Transport abstraction layer changes](~/includes/core-changes/aspnetcore/3.0/kestrel-transport-abstractions.md)]

_*_

[!INCLUDE[Localization: APIs marked obsolete](~/includes/core-changes/aspnetcore/3.0/localization-apis-marked-obsolete.md)]

_*_

[!INCLUDE[Logging: DebugLogger class made internal](~/includes/core-changes/aspnetcore/3.0/logging-debuglogger-to-internal.md)]

_*_

[!INCLUDE[MVC: Controller action Async suffix removed](~/includes/core-changes/aspnetcore/3.0/mvc-action-async-suffix-trimmed.md)]

_*_

[!INCLUDE[MVC: JsonResult moved to Microsoft.AspNetCore.Mvc.Core](~/includes/core-changes/aspnetcore/3.0/mvc-jsonresult-moved.md)]

_*_

[!INCLUDE[MVC: Precompilation tool deprecated](~/includes/core-changes/aspnetcore/3.0/mvc-precompilation-tool-deprecated.md)]

_*_

[!INCLUDE[MVC: Types changed to internal](~/includes/core-changes/aspnetcore/3.0/mvc-pubternal-to-internal.md)]

_*_

[!INCLUDE[MVC: Web API compatibility shim removed](~/includes/core-changes/aspnetcore/3.0/mvc-webapi-compat-shim-removed.md)]

_*_

[!INCLUDE[Razor: RazorTemplatEengine API removed](~/includes/core-changes/aspnetcore/3.0/razor-razortemplateengine-api-removed.md)]

_*_

[!INCLUDE[Razor: Runtime compilation moved to a package](~/includes/core-changes/aspnetcore/3.0/razor-runtime-compilation-package.md)]

_*_

[!INCLUDE[Session state: Obsolete APIs removed](~/includes/core-changes/aspnetcore/3.0/session-obsolete-apis-removed.md)]

_*_

[!INCLUDE[Shared framework: Assembly removal from Microsoft.AspNetCore.App](~/includes/core-changes/aspnetcore/3.0/sharedfx-app-shared-framework-assemblies.md)]

_*_

[!INCLUDE[Shared framework: Microsoft.AspNetCore.All removed](~/includes/core-changes/aspnetcore/3.0/sharedfx-all-framework-removed.md)]

_*_

[!INCLUDE[SignalR: HandshakeProtocol.SuccessHandshakeData replaced](~/includes/core-changes/aspnetcore/3.0/signalr-successhandshakedata-replaced.md)]

_*_

[!INCLUDE[SignalR: HubConnection methods removed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnection-methods-removed.md)]

_*_

[!INCLUDE[SignalR: HubConnectionContext constructors changed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnectioncontext-ctors.md)]

_*_

[!INCLUDE[SignalR: JavaScript client package name change](~/includes/core-changes/aspnetcore/3.0/signalr-js-client-package-name.md)]

_*_

[!INCLUDE[SignalR: Obsolete APIs](~/includes/core-changes/aspnetcore/3.0/signalr-obsolete-apis.md)]

_*_

[!INCLUDE[SPAs: SpaServices and NodeServices marked obsolete](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-obsolete.md)]

_*_

[!INCLUDE[SPAs: SpaServices and NodeServices console logger fallback default change](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-fallback.md)]

_*_

[!INCLUDE[Target framework: .NET Framework not supported](~/includes/core-changes/aspnetcore/3.0/targetfx-netfx-tfm-support.md)]

_**
