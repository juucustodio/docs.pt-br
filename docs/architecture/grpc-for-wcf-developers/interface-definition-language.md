---
title: Linguagem de definição de interface-gRPC para desenvolvedores do WCF
description: Apresentando os buffers de protocolo IDL.
ms.date: 12/15/2020
ms.openlocfilehash: 60cedd9b7c29bf54165b15f512c0b2159cb5dda9
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938072"
---
# <a name="interface-definition-language"></a>Linguagem IDL

Com o Windows Communication Foundation (WCF), os serviços podem expor metadados de descrição usando o WSDL (Web Service Definition Language). O WSDL é gerado dinamicamente usando a reflexão do .NET em tempo de execução. Os desenvolvedores podem usar esses metadados para gerar clientes para esses serviços, potencialmente em outras linguagens se estiverem usando uma associação neutra de plataforma, como SOAP sobre HTTP.

gRPC usa o IDL (Interface Definition Language) dos buffers de protocolo. Os buffers de protocolo IDL são uma linguagem personalizada de plataforma neutra com uma especificação aberta. Os desenvolvedores criam `.proto` arquivos para descrever serviços, juntamente com suas entradas e saídas. Esses `.proto` arquivos podem então ser usados para gerar stubs específicos de idioma ou de plataforma para clientes e servidores, permitindo que várias plataformas diferentes se comuniquem. Ao compartilhar `.proto` arquivos, as equipes podem gerar código para usar os serviços de cada um, sem a necessidade de assumir uma dependência de código.

Uma das vantagens do Protobuf IDL é que, como uma linguagem personalizada, ele permite que o gRPC seja completamente independente de linguagem e plataforma, não favorecendo nenhuma tecnologia sobre outra.

O Protobuf IDL também é projetado para os seres humanos para leitura e gravação, enquanto o WSDL é destinado a um formato legível por máquina/gravável. A alteração do WSDL de um serviço WCF normalmente requer a alteração do serviço, a execução do serviço e a regeneração do arquivo WSDL a partir do servidor. Por outro lado, com um `.proto` arquivo, as alterações são simples de se aplicar a um editor de texto e fluir automaticamente pelo código gerado. O Visual Studio 2019 compila `.proto` arquivos em segundo plano quando eles são salvos. Com outros editores, como VS Code, as alterações são aplicadas quando o projeto é compilado.

Quando comparado com XML e particularmente SOAP, mensagens codificadas usando Protobuf têm muitas vantagens. As mensagens Protobuf tendem a ser menores do que os mesmos dados serializados como XML SOAP, e codificar, decodificar e transmiti-los por uma rede pode ser mais rápido.

A desvantagem potencial do Protobuf em comparação com o SOAP é que, como as mensagens não são legíveis por humanos, ferramentas adicionais são necessárias para depurar o conteúdo da mensagem.

> [!TIP]
> *o* gRPC oferece suporte à reflexão de servidor para acessar serviços dinamicamente sem stubs pré-compilados, embora ele seja mais destinado a ferramentas de finalidade geral do que clientes específicos do aplicativo. Para obter mais informações, consulte [protocolo de reflexão do GRPC Server](https://github.com/grpc/grpc/blob/master/doc/server-reflection.md) no github.

> [!NOTE]
> O formato binário do WCF, usado com a associação NetTCP, é muito mais próximo de Protobuf em termos de compactação e desempenho. Mas o NetTCP só é utilizável entre clientes e servidores .NET, enquanto o Protobuf é uma solução de plataforma cruzada.

>[!div class="step-by-step"]
>[Anterior](approach.md) 
> [Avançar](network-protocols.md)
