---
title: .NET Framework tecnologias não disponíveis no .NET Core e no .NET 5 +
titleSuffix: ''
description: Saiba mais sobre as tecnologias .NET Framework que não estão disponíveis no .NET Core e no .NET 5,0 e versões posteriores.
author: cartermp
ms.date: 01/26/2021
ms.openlocfilehash: d5926d2c0cfe6d2073ac6ad74046ca48b9cb18f1
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98898769"
---
# <a name="net-framework-technologies-unavailable-on-net-core-and-net-5"></a>.NET Framework tecnologias não disponíveis no .NET Core e no .NET 5 +

Várias tecnologias disponíveis para .NET Framework bibliotecas não estão disponíveis para uso com o .NET Core e o .NET 5,0 e versões posteriores, como domínios de aplicativo, comunicação remota e CAS (segurança de acesso a código). Se suas bibliotecas dependem de uma ou mais das tecnologias listadas nesta página, considere as abordagens alternativas que são mencionadas.

Para obter mais informações sobre compatibilidade de API, consulte [alterações significativas no .net](../compatibility/breaking-changes.md).

## <a name="application-domains"></a>Domínios de aplicativo

Os domínios do aplicativo (AppDomains) isolam os aplicativos uns dos outros. Os AppDomains exigem suporte em tempo de execução e são geralmente caros. Não há suporte para a criação de domínios de aplicativo adicionais, e não há planos para adicionar esse recurso no futuro. Para o isolamento de código, use processos ou contêineres separados como alternativa. Para carregar dinamicamente os assemblies, use a <xref:System.Runtime.Loader.AssemblyLoadContext> classe.

Para tornar a migração de código de .NET Framework mais fácil, o .NET 5 + expõe parte da <xref:System.AppDomain> superfície da API. Algumas das APIs funcionam normalmente (por exemplo, <xref:System.AppDomain.UnhandledException?displayProperty=nameWithType>), alguns membros não fazem nada (por exemplo, <xref:System.AppDomain.SetCachePath%2A>) e alguns geram <xref:System.PlatformNotSupportedException> (por exemplo, <xref:System.AppDomain.CreateDomain%2A>). Verifique os tipos usados em relação à [ `System.AppDomain` origem de referência](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Private.CoreLib/src/System/AppDomain.cs) no [repositório do GitHub dotnet/tempo de execução](https://github.com/dotnet/runtime). Certifique-se de selecionar a ramificação que corresponde à sua versão implementada.

## <a name="remoting"></a>Comunicação remota

A comunicação remota do .NET foi identificada como uma arquitetura problemática. Ele é usado para se comunicar entre domínios de aplicativo, que não têm mais suporte. Além disso, a comunicação remota requer suporte a tempo de execução, o que é caro para manter. Por esses motivos, o .NET Remoting não tem suporte no .NET Core e no .NET 5 +, e não planejamos adicionar suporte para ele no futuro.

Para a comunicação entre processos, considere os mecanismos IPC (comunicação entre processos) como uma alternativa à comunicação remota, como a <xref:System.IO.Pipes> classe ou a <xref:System.IO.MemoryMappedFiles.MemoryMappedFile> classe.

Entre computadores, use uma solução baseada em rede como alternativa. De preferência, use um protocolo de texto sem formatação de sobrecarga baixa, como HTTP. O [servidor Web Kestrel](/aspnet/core/fundamentals/servers/kestrel), que é o servidor Web usado pelo ASP.NET Core, é uma opção aqui. Além disso, considere o uso <xref:System.Net.Sockets> de cenários de máquina cruzada e baseados em rede. Para ter mais opções, veja [.NET Open Source Developer Projects: Messaging](https://github.com/Microsoft/dotnet/blob/master/dotnet-developer-projects.md#messaging).

## <a name="code-access-security-cas"></a>CAS (Segurança de Acesso do Código)

A área restrita, que se baseia no tempo de execução ou na estrutura para restringir quais recursos um aplicativo ou uma biblioteca gerenciada usa ou executa, [não tem suporte no .NET Framework](../../framework/misc/code-access-security.md) e, portanto, também não tem suporte no .NET Core e no .NET 5 +. Há muitos casos no .NET Framework e no runtime em que ocorre uma elevação de privilégios para continuar a tratar a CAS como um limite de segurança. Além disso, a CAS complica mais a implementação e geralmente tem implicações de desempenho de exatidão em aplicativos que não pretendem usá-la.

Use limites de segurança fornecidos pelo sistema operacional, como virtualização, contêineres ou contas de usuário, para executar processos com o conjunto mínimo de privilégios.

## <a name="security-transparency"></a>Transparência de segurança

Semelhante ao CAS, a transparência de segurança separa o código em área restrita do código crítico de segurança de maneira declarativa, mas [não tem mais suporte como um limite de segurança](../../framework/misc/security-transparent-code.md). Esse recurso é amplamente usado pelo Silverlight.

Use limites de segurança fornecidos pelo sistema operacional, como virtualização, contêineres ou contas de usuário, para executar processos com o menor conjunto de privilégios.

## <a name="systementerpriseservices"></a>System.EnterpriseServices

<xref:System.EnterpriseServices?displayProperty=fullName> (COM+) não tem suporte no .NET Core e no .NET 5 +.

## <a name="workflow-foundation-and-wcf"></a>Workflow Foundation e WCF

Não há suporte para Windows Workflow Foundation (WF) e Windows Communication Foundation (WCF) no .NET 5 + (incluindo o .NET Core). Para obter alternativas, consulte [CoreWF](https://github.com/UiPath/corewf) e [CoreWCF](https://github.com/CoreWCF/CoreWCF).

## <a name="see-also"></a>Confira também

- [Visão geral da portabilidade do .NET Framework para o .NET Core](index.md)
