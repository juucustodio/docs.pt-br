---
description: 'Saiba mais sobre: alterações na autenticação NTLM para HttpWebRequest na versão 3,5 SP1'
title: Alterações na autenticação NTLM para HttpWebRequest na versão 3.5 SP1
ms.date: 03/30/2017
ms.assetid: 8bf0b428-5a21-4299-8d6e-bf8251fd978a
ms.openlocfilehash: cdb17317dbafc167cce7a9b2785be68a35d3bd5b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791628"
---
# <a name="changes-to-ntlm-authentication-for-httpwebrequest-in-version-35-sp1"></a>Alterações na autenticação NTLM para HttpWebRequest na versão 3.5 SP1

Foram feitas alterações de segurança no .NET Framework versão 3.5 SP1 que afetam a maneira como a autenticação integrada do Windows é manipulada por <xref:System.Net.HttpWebRequest>, <xref:System.Net.HttpListener>, <xref:System.Net.Security.NegotiateStream> e por classes relacionadas no namespace System.Net. Essas alterações podem afetar os aplicativos que usam essas classes para fazer solicitações da Web e receber respostas em que a autenticação integrada do Windows baseada no NTLM é usada. Essa alteração pode afetar os servidores Web e aplicativos cliente configurados para usar a autenticação integrada do Windows.

## <a name="overview"></a>Visão geral

O design da autenticação integrada do Windows permite que algumas respostas de credencial sejam universais, o que significa que elas podem ser reutilizadas ou encaminhadas. Se esse recurso de design específico não for necessário, os protocolos de autenticação deverão conter informações específicas ao destino, bem como informações específicas ao canal. Em seguida, os serviços podem fornecer proteção estendida para garantir que as respostas de credencial contenham informações específicas ao serviço, como um SPN (Nome da Entidade de Serviço). Com essas informações nas trocas de credenciais, os serviços podem proteger melhor contra o uso mal intencionado de respostas de credencial que podem ter sido obtidas indevidamente.

Vários componentes nos namespaces <xref:System.Net> e <xref:System.Net.Security> executam a autenticação integrada do Windows em nome de um aplicativo de chamada. Esta seção descreve as alterações nos componentes do System.Net para adicionar a proteção estendida no uso que eles fazem da autenticação integrada do Windows.

## <a name="changes"></a>Alterações

O processo de autenticação NTLM usado com a autenticação integrada do Windows inclui um desafio emitido pelo computador de destino e enviado novamente para o computador cliente. Quando um computador recebe um desafio que ele próprio gerou, a autenticação falhará, a menos que a conexão seja uma conexão de loopback (endereço IPv4 127.0.0.1, por exemplo).

Ao acessar um serviço executado em um servidor Web interno, é comum acessar o serviço usando uma URL semelhante a `http://contoso/service` ou `https://contoso/service`. O nome “contoso” geralmente não é o nome do computador no qual o serviço é implantado. O <xref:System.Net> e os namespaces relacionados dão suporte ao uso do Active Directory, DNS, NetBIOS, o arquivo de hosts do computador local (geralmente, WINDOWS\system32\drivers\etc\hosts, por exemplo) ou o arquivo lmhosts do computador local (geralmente, WINDOWS\system32\drivers\etc\lmhosts, por exemplo) para resolver nomes em endereços. O nome “contoso” é resolvido para que as solicitações enviadas para “contoso” sejam enviadas para o computador do servidor apropriado.

Quando configurado para implantações grandes, também é comum que um único nome do servidor virtual seja fornecido à implantação com os nomes de computador subjacentes nunca usados pelos aplicativos cliente e usuários finais. Por exemplo, você pode chamar o servidor `www.contoso.com`, mas em uma rede interna, basta usar "contoso". Esse nome é chamado de cabeçalho de Host na solicitação da Web do cliente. Conforme especificado pelo protocolo HTTP, o campo de cabeçalho da solicitação Host especifica o número da porta e o host da Internet do recurso solicitado. Essas informações são obtidas do URI original fornecido pelo usuário ou pelo recurso de referência (geralmente uma URL HTTP). No .NET Framework versão 4, essas informações também podem ser definidas pelo cliente usando a nova propriedade <xref:System.Net.HttpWebRequest.Host%2A>.

A classe <xref:System.Net.AuthenticationManager> controla os componentes de autenticação gerenciada (“módulos”) que são usados pelas classes derivadas <xref:System.Net.WebRequest> e pela classe <xref:System.Net.WebClient>. A classe <xref:System.Net.AuthenticationManager> fornece uma propriedade que expõe um objeto <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A?displayProperty=nameWithType>, indexado por uma cadeia de caracteres do URI, de aplicativos para fornecer uma cadeia de caracteres do SPN personalizada a ser usada durante a autenticação.

A versão 3.5 SP1 agora usa como padrão a especificação do nome do host usado na URL da solicitação no SPN da troca de autenticação NTLM (NT LAN Manager) quando a propriedade <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A> não está definida. O nome do host usado na URL da solicitação pode ser diferente do cabeçalho de Host especificado na <xref:System.Net.HttpRequestHeader?displayProperty=nameWithType> na solicitação do cliente. O nome do host usado na URL de solicitação pode ser diferente do nome do host real do servidor, do nome do computador do servidor, do endereço IP do computador ou do endereço de loopback. Nesses casos, o Windows falhará a solicitação de autenticação. Para resolver o problema, é necessário notificar o Windows de que o nome do host usado na URL da solicitação na solicitação do cliente (“contoso”, por exemplo) é realmente um nome alternativo para o computador local.

Há vários métodos possíveis para que um aplicativo para servidores resolva essa alteração. A abordagem recomendada é mapear o nome do host usado na URL da solicitação para a chave `BackConnectionHostNames` do Registro no servidor. A chave do Registro `BackConnectionHostNames` é normalmente usada para mapear um nome do host para um endereço de loopback. As etapas são listadas abaixo.

Para especificar os nomes do host que são mapeados para o endereço de loopback e que podem se conectar a sites em um computador local, siga estas etapas:

1. Clique em Iniciar, clique em Executar, digite regedit e, em seguida, clique em OK.

2. No Editor do Registro, localize e, em seguida, clique na seguinte chave do Registro:

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\MSV1_0`

3. Clique com o botão direito do mouse em MSV1_0, aponte para Novo e, em seguida, clique em Valor de Cadeia de Caracteres Múltipla.

4. Digite `BackConnectionHostNames` e pressione ENTER.

5. Clique com o botão direito do mouse em `BackConnectionHostNames` e, em seguida, clique em Modificar.

6. Na caixa de dados Valor, digite o nome do host ou os nomes do host dos sites (o nome do host usado na URL da solicitação) que estão no computador local e, em seguida, clique em OK.

7. Encerre o Editor do Registro e, em seguida, reinicie o serviço IISAdmin e execute IISReset.

Uma solução alternativa menos segura é desabilitar a verificação de loopback, conforme descrito em <https://support.microsoft.com/kb/896861>. Isso desabilita a proteção contra ataques de reflexão. Portanto, é melhor restringir o conjunto de nomes alternativos somente àqueles que você espera que sejam usados pelo computador.

## <a name="see-also"></a>Confira também

- <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A?displayProperty=nameWithType>
- <xref:System.Net.HttpRequestHeader?displayProperty=nameWithType>
- <xref:System.Net.HttpWebRequest.Host%2A?displayProperty=nameWithType>
