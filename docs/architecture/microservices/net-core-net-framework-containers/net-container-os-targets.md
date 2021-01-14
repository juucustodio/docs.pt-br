---
title: Para qual sistema operacional direcionar com os contêineres do .NET
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Para qual sistema operacional direcionar com os contêineres do .NET
ms.date: 01/13/2021
ms.openlocfilehash: 1b914d9afca9ade37f13e639f73001b91f338d26
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98187971"
---
# <a name="what-os-to-target-with-net-containers"></a>Para qual sistema operacional direcionar com os contêineres do .NET

Considerando a diversidade de sistemas operacionais com suporte pelo Docker e as diferenças entre .NET Framework e o .NET 5, você deve direcionar um sistema operacional específico e versões específicas, dependendo da estrutura que você está usando.

Para o Windows, é possível usar o Windows Server Core ou o Windows Nano Server. Essas versões do Windows fornecem características diferentes (IIS no Windows Server Core versus um servidor Web autohospedado, como o Kestrel no nano Server) que pode ser necessário para o .NET Framework ou o .NET 5, respectivamente.

Para Linux, várias distribuições estão disponíveis e há compatibilidade com elas nas imagens oficiais do .NET Docker (como Debian).

Na Figura 3-1, você pode ver a possível versão do sistema operacional dependendo do .NET Framework usado.

![Diagrama que mostra o sistema operacional a ser usado com os contêineres .NET.](./media/net-container-os-targets/targeting-operating-systems.png)

**Figura 3-1.** Sistemas operacionais a serem direcionados dependendo das versões do .NET Framework

Ao implantar aplicativos .NET Framework herdados, você precisa ter como alvo o Windows Server Core, compatível com aplicativos herdados e o IIS, mas tem uma imagem maior. Ao implantar aplicativos do .NET 5, você pode direcionar o Windows nano Server, que é otimizado para a nuvem, usa Kestrel e é menor e começa mais rapidamente. Você também pode ter como alvo o Linux, com suporte para Debian, Alpine e outros. O também usa Kestrel, é menor e é iniciado mais rapidamente.

Também é possível criar sua própria imagem do Docker em casos em que você deseja usar uma distribuição diferente do Linux ou em que você quer uma imagem com versões não fornecidas pela Microsoft. Por exemplo, você pode criar uma imagem com o ASP.NET Core em execução no .NET Framework tradicional e no Windows Server Core, que é um cenário não tão comum para Docker.

> [!IMPORTANT]
> Ao usar imagens do Windows Server Core, você pode achar que algumas DLLs estão ausentes, quando comparadas com imagens completas do Windows. Você pode resolver esse problema criando uma imagem personalizada de núcleo do servidor, adicionando os arquivos ausentes no momento da compilação da imagem, conforme mencionado neste [Comentário do GitHub](https://github.com/microsoft/dotnet-framework-docker/issues/299#issuecomment-511537448).

Ao adicionar o nome de imagem ao seu arquivo Dockerfile, é possível selecionar o sistema operacional e a versão dependendo da marcação usada, como nos seguintes exemplos:

| Imagem | Comentários |
|-------|----------|
| mcr.microsoft.com/dotnet/runtime:5.0 | Múltiplas arquiteturas do .NET 5: oferece suporte ao Linux e ao Windows nano Server dependendo do host do Docker. |
| mcr.microsoft.com/dotnet/aspnet:5.0 | ASP.NET Core várias arquiteturas 5,0: dá suporte ao Linux e ao Windows nano Server dependendo do host do Docker. <br/> A imagem aspnetcore tem algumas otimizações para ASP.NET Core. |
| mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim | Tempo de execução do .NET 5 somente no Linux Debian distribuição |
| mcr.microsoft.com/dotnet/aspnet:5.0-nanoserver-1809 | Somente em tempo de execução do .NET 5 no Windows nano Server (Windows Server versão 1809) |

## <a name="additional-resources"></a>Recursos adicionais

- **BitmapDecoder falha devido a WindowsCodecsExt.dll ausente (problema do GitHub)**  
  <https://github.com/microsoft/dotnet-framework-docker/issues/299>

> [!div class="step-by-step"]
> [Anterior](container-framework-choice-factors.md) 
>  [Avançar](official-net-docker-images.md)
