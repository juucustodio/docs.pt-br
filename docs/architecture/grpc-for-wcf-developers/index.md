---
title: ASP.NET Core gRPC para desenvolvedores do WCF – gRPC para desenvolvedores do WCF
description: Introdução à criação de serviços gRPCs no ASP.NET Core 5,0 para desenvolvedores do WCF
ms.date: 01/06/2021
ms.openlocfilehash: 26cce6bb784c08a5b59623ff5882fcf2fbb9e9ac
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970187"
---
# <a name="aspnet-core-grpc-for-wcf-developers"></a>ASP.NET Core gRPC para desenvolvedores do WCF

![imagem da capa](./media/cover.png)

Edição v 1.0.1-atualizado para ASP.NET Core 5,0

Consulte o [changelog](https://aka.ms/grpc-ebook-changelog) para obter as atualizações do livro e as contribuições da Comunidade.

PUBLICADO POR

Divisão de Desenvolvedores Microsoft, equipes dos produtos .NET e Visual Studio

Uma divisão da Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2021 da Microsoft Corporation

Todos os direitos reservados. Nenhuma parte do conteúdo deste guia pode ser reproduzida ou transmitida de nenhuma forma nem por nenhum meio sem a permissão por escrito do publicador.

Este livro é fornecido “no estado em que se encontra” e expressa os pontos de vista e as opiniões do autor. Os pontos de vista, as opiniões e as informações expressos neste guia, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.

 Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.

A Microsoft e as marcas listadas em <https://www.microsoft.com> na página da Web "Marcas" são marcas comerciais do grupo de empresas Microsoft.

O logotipo de redistribuição do Docker é uma marca registrada do Docker, Inc. usada pela permissão.

Todas as outras marcas e logotipos são propriedade de seus respectivos proprietários.

Autores:

> **Mark** diretor técnico de Rendle – [recódigo Visual](https://visualrecode.com)
>
> **Miranda Steiner** – autor técnico

Editor:

> **Maira Wenzel** -Sr. Content Developer-Microsoft

## <a name="introduction"></a>Introdução

o gRPC é uma estrutura moderna para a criação de serviços em rede e aplicativos distribuídos. Imagine o desempenho das associações NetTCP do Windows Communication Foundation (WCF), combinadas com a interoperabilidade entre plataformas do SOAP. o gRPC se baseia no HTTP/2 e no protocolo de codificação de mensagens Protobuf para fornecer comunicação de alto desempenho e baixa largura de banda entre aplicativos e serviços. Ele dá suporte à geração de código de servidor e cliente nas linguagens e plataformas de programação mais populares, incluindo .NET, Java, Python, Node.js, Go e C++. Com o suporte de primeira classe para gRPC no ASP.NET Core 5,0, juntamente com as ferramentas e bibliotecas existentes do gRPC para .NET Framework 4. x, é uma excelente alternativa ao WCF para equipes de desenvolvimento que buscam adotar o .NET em suas organizações.

## <a name="who-should-use-this-guide"></a>Quem deve usar este guia

Este guia foi escrito para desenvolvedores que trabalham em .NET Framework ou .NET que usavam o WCF anteriormente e que estão buscando migrar seus aplicativos para um ambiente de RPC moderno para .NET Core 3,0 e versões posteriores. Mais geralmente, se você estiver atualizando ou considerando a atualização para o .NET 5 e quiser usar as ferramentas internas do gRPC, este guia também será útil.

## <a name="how-you-can-use-this-guide"></a>Como você pode usar este guia

Esta é uma breve introdução à criação de serviços gRPCs no ASP.NET Core 5,0, com referência específica ao WCF como uma plataforma análoga. Ele explica os princípios de gRPC, relacionando cada conceito aos recursos equivalentes do WCF e oferece orientação para migrar um aplicativo WCF existente para o gRPC. Ele também é útil para desenvolvedores que têm experiência com o WCF e procuram aprender a gRPC para criar novos serviços. Você pode usar os aplicativos de exemplo como um modelo ou referência para seus próprios projetos e você é livre para copiar e reutilizar o código do livro ou de seus exemplos.

Fique à vontade para encaminhar este guia para sua equipe para ajudar a garantir um entendimento comum dessas considerações e oportunidades. Ter todos trabalhando em um conjunto comum de termos e princípios subjacentes ajuda a garantir a aplicação consistente de práticas e padrões de arquitetura.

## <a name="references"></a>Referências

- **site do gRPC**
  <https://grpc.io>
- **Escolhendo entre o .NET 5 e o .NET Framework para aplicativos de servidor**
  <https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server>

>[!div class="step-by-step"]
>[Próximo](introduction.md)
