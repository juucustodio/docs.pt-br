---
title: Cenários de implantação ao migrar para o ASP.NET Core
description: Uma visão geral das diferentes abordagens para a implantação que podem ser usadas ao portar do ASP.NET para o ASP.NET Core, permitindo migrações lado a lado e em fases.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 8a3b658c777f2243c7c63908d9d0b24822b6790e
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488402"
---
# <a name="deployment-scenarios-when-migrating-to-aspnet-core"></a>Cenários de implantação ao migrar para o ASP.NET Core

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Os aplicativos de API Web e MVC existentes do ASP.NET são executados no IIS e no Windows. Aplicativos grandes podem exigir uma abordagem em fases ou lado a lado ao portar para ASP.NET Core. Nos capítulos anteriores, você aprendeu várias estratégias para migrar grandes aplicativos de .NET Framework para ASP.NET Core em fases. Neste capítulo, você verá como diferentes cenários de implantação podem ser obtidos quando houver a necessidade de manter o aplicativo original em produção ao migrar partes dele.

## <a name="split-a-large-web-app"></a>Dividir um aplicativo Web grande

Considere o cenário comum de um aplicativo Web grande que atualmente está hospedado no IIS em um único site. Dentro do aplicativo grande, a funcionalidade é segmentada em diferentes rotas e/ou diretórios. O aplicativo é uma mistura de exibições MVC e pontos de extremidade de API. As rotas do MVC incluem muitos caminhos diferentes com base na funcionalidade e todos começam da raiz do aplicativo usando o `/{controller}/{action}/{id?}` modelo de rota padrão. Os pontos de extremidade de API seguem um padrão semelhante, mas estão todos em uma `/api` raiz.

Supondo que a tarefa de portar o aplicativo seja dividida de forma que a funcionalidade MVC ou a funcionalidade da API seja migrada para ASP.NET Core primeiro, como o site original continuaria a funcionar diretamente com o novo aplicativo ASP.NET Core em execução em outro lugar? Os usuários do sistema devem continuar a ver as mesmas URLs que faziam antes da migração, a menos que seja absolutamente necessário alterá-las.

Felizmente, o IIS é um servidor Web repleto de recursos e dois recursos que ele tinha há algum tempo são seu [módulo de reescrita de URL e Application Request Routing](https://docs.microsoft.com/iis/extensions/url-rewrite-module/reverse-proxy-with-url-rewrite-v2-and-application-request-routing). Usando esses recursos, o IIS pode atuar como um [proxy reverso](https://docs.microsoft.com/iis/extensions/url-rewrite-module/reverse-proxy-with-url-rewrite-v2-and-application-request-routing), roteando solicitações de cliente para o aplicativo Web de back-end apropriado. Para configurar o IIS como um proxy reverso, marque a caixa de seleção **habilitar proxy** no recurso Application Request Routing e, em seguida, adicione uma regra de regravação de URL como esta:

```xml
<rule name="NetCoreProxy">
  <match url="(.*)> />
  <action type="Rewrite" url="http://servername/{R:1}" />
</rule>
```

Como um proxy reverso, o IIS pode rotear o tráfego que corresponde a determinados padrões para aplicativos totalmente separados, potencialmente em servidores diferentes.

Usando apenas o módulo de reescrita de URL (talvez combinado com cabeçalhos de host), o IIS pode facilmente dar suporte a vários sites da Web, cada um potencialmente executando diferentes versões do .NET. Um aplicativo Web grande pode ser implantado como uma coleção de sites individuais, cada um respondendo a diferentes endereços IP e/ou cabeçalhos de host, ou como um único site com um ou mais subaplicativos que estão respondendo a determinados caminhos de URL (que nem mesmo exigem a regravação de URL).

> [!IMPORTANT]
> Os subdomínios normalmente se referem à parte de um domínio que precede os dois níveis superiores. Por exemplo, no domínio `api.contoso.com` , `api` é um subdomínio do `contoso.com` domínio (que, por sua vez, é composto pelo `contoso` nome de domínio e pelo `.com` domínio de nível superior ou TLD). Caminhos de URL referem-se à parte da URL que segue o nome de domínio, começando com um `/` . A URL `https://contoso.com/api` tem um caminho de `/api` .

Há prós e contras em usar os mesmos ou subdomínios (e domínios) diferentes para hospedar um único aplicativo. Recursos como cookies e comunicação entre aplicativos usando mecanismos como [CORS](https://docs.microsoft.com/aspnet/core/security/cors) podem exigir mais configuração para funcionar corretamente em aplicativos distribuídos. No entanto, os aplicativos que usam subdomínios diferentes podem usar o DNS mais facilmente para rotear solicitações para destinos de rede totalmente diferentes e, portanto, podem ser implantados com mais facilidade em vários servidores diferentes (virtuais ou de outra forma) sem a necessidade de o IIS agir como um proxy reverso.

No exemplo descrito acima, suponha que os pontos de extremidade da API sejam designados como a primeira parte do aplicativo a ser transportado para ASP.NET Core. Nesse caso, um novo aplicativo ASP.NET Core é criado e hospedado no IIS como um *aplicativo* Web separado no *site* existente do ASP.NET MVC. Como ele será adicionado como um filho do site original e será nomeado *API*, sua rota padrão não deve mais começar com `api/` . Manter isso resultará na correspondência de URLs do formulário `/api/api/endpoint` .

A Figura 5-1 mostra como o aplicativo de *api* ASP.NET Core 2,1 aparece no Gerenciador do IIS como parte do site *DotNetMvcApp* existente.

![Gerenciador do IIS mostrando aplicativo de API dentro do .NET Framework site](./media/Figure5-1.png)

**Figura 5-1**. .NET Framework site com o aplicativo .NET Core no IIS.

O site do *DotNetMvcApp* é hospedado como um aplicativo MVC 5 em execução no .NET Framework 4.7.2. Ele tem seu próprio pool de aplicativos do IIS configurado no modo integrado e executando o .NET CLR versão 4.0.30319. O aplicativo de *API* é um aplicativo ASP.NET Core em execução no .NET Framework 4.6.1 ( `net461` ). Ele foi adicionado ao *DotNetMvcApp* como um novo aplicativo IIS e configurado para usar seu próprio pool de aplicativos. Seu pool de aplicativos também está sendo executado no modo integrado, mas é configurado com uma versão .NET CLR de **nenhum código gerenciado** , pois ele será executado usando o [módulo ASP.NET Core](https://docs.microsoft.com/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-2.1&preserve-view=true). A versão do aplicativo ASP.NET Core é apenas um exemplo. Ele também pode ser configurado para ser executado no .NET Core 3,1 ou no .NET 5,0. Embora nesse ponto, não seria mais possível direcionar as bibliotecas de .NET Framework (consulte [escolher a versão correta do .NET Core](choose-net-core-version.md))

Configurado dessa maneira, a única alteração que deve ser feita para que as APIs do ASP.NET Core aplicativo sejam roteadas corretamente é alterar seu modelo de rota padrão de `[Route("[api/controller]")]` para `[Route("[controller]")]` .

Como alternativa, o aplicativo ASP.NET Core pode ser outro site de nível superior no IIS. Nesse caso, você pode configurar o site original para usar uma regra de reescrita (com a [reescrita de URL](https://www.iis.net/downloads/microsoft/url-rewrite)) que será redirecionada para o outro aplicativo se o caminho começar com `/api` . O aplicativo ASP.NET Core pode usar um cabeçalho de host diferente para sua rota para que ele não entre em conflito com o aplicativo principal, mas ainda pode responder a solicitações usando rotas baseadas em raiz.

Por exemplo, o mesmo ASP.NET Core aplicativo usado na Figura 5-1 pode ser implantado em outra pasta configurada como um site do IIS. O site deve usar um pool de aplicativos configurado da mesma forma que antes, sem **código gerenciado**. Configure suas associações para responder a um nome de host exclusivo no servidor, como `api.contoso.com` . Para configurar a regravação de URL para reescrever solicitações `/api` , basta adicionar uma nova regra de entrada no nível do servidor IIS (ou site individual). Corresponda ao padrão `^/api(.*)` e especifique um tipo de ação `Rewrite` e uma URL de regravação de `api.contoso.com/{R:1}` . A combinação de usar `(.*)` no padrão de correspondência e `{R:1}` na URL de regravação garantirá que o restante do caminho será usado com a nova URL. Com isso implementado, sites separados no mesmo servidor IIS podem coexistir em execução em versões separadas do .NET, mas eles podem ser feitos para serem exibidos na Internet como um aplicativo Web. A Figura 5-2 mostra a regra de regravação conforme configurada no IIS com o site da Web separado.

![Gerenciador do IIS mostrando regra de regravação de URL para rotear solicitações de subpasta para um site separado](./media/Figure5-2.png)

**Figura 5-2**. Reescreva a regra para regravar as solicitações de subpasta em outro site da Web.

Se seu aplicativo exigir logon único entre sites ou aplicativos diferentes no IIS, consulte a documentação sobre [como compartilhar cookies de autenticação entre aplicativos ASP.net](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/) para obter instruções detalhadas sobre como dar suporte a esse cenário.

## <a name="summary"></a>Resumo

Uma abordagem comum para portar grandes aplicativos de .NET Framework para ASP.NET Core é escolher partes individuais do aplicativo para migrar uma a uma. Como cada parte do aplicativo é portada, todo o aplicativo permanece em execução e utilizável, com algumas partes dele em execução em sua configuração original e outras partes em execução em alguma versão do .NET Core. Seguindo essa abordagem, uma migração de aplicativo grande pode ser executada incrementalmente. Essa abordagem resulta na limitação de riscos fornecendo comentários mais rápidos e reduzindo a área de superfície total envolvida no teste. Ele também permite a realização mais rápida de benefícios do .NET Core, como aumentos de desempenho. Embora os aplicativos ASP.NET Core não precisem ser hospedados no IIS, o IIS continua sendo um servidor Web muito flexível e poderoso que pode ser configurado para dar suporte a uma variedade de cenários de hospedagem que envolvem .NET Framework e ASP.NET Core aplicativos na mesma instância do IIS ou até mesmo hospedados em servidores diferentes.

## <a name="references"></a>Referências

- [Hospedar o ASP.NET Core no Windows com o IIS](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/)
- [Módulo de reescrita de URL e Application Request Routing](https://docs.microsoft.com/iis/extensions/url-rewrite-module/reverse-proxy-with-url-rewrite-v2-and-application-request-routing)
- [Regravação de URL](https://www.iis.net/downloads/microsoft/url-rewrite)
- [Módulo do ASP.NET Core](https://docs.microsoft.com/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-2.1&preserve-view=true)
- [Compartilhar cookies de autenticação entre aplicativos ASP.NET](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/)

>[!div class="step-by-step"]
>[Anterior](example-migration-eshop.md) 
> [Avançar](summary.md)
