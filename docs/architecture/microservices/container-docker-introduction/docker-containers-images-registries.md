---
title: Registros, imagens e contêineres do Docker
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Registros, imagens e contêineres do Docker
ms.date: 01/13/2021
ms.openlocfilehash: 0dfde34cd9dab1ef47237746ca6ac2ed75379635
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189363"
---
# <a name="docker-containers-images-and-registries"></a>Registros, imagens e contêineres do Docker

Ao usar o Docker, um desenvolvedor cria um aplicativo ou serviço e empacota a ele e suas dependências em uma imagem de contêiner. Uma imagem é uma representação estática do aplicativo ou do serviço e de sua configuração e dependências.

Para executar o aplicativo ou o serviço, uma instância da imagem do aplicativo é criada para criar um contêiner, que estará em execução no host do Docker. Inicialmente, os contêineres são testados em um ambiente de desenvolvimento ou em um computador.

Os desenvolvedores devem armazenar imagens em um Registro, que funciona como uma biblioteca de imagens e é necessário ao implantar em orquestradores de produção. O Docker mantém um Registro público por meio do [Hub do Docker](https://hub.docker.com/); outros fornecedores fornecem os Registros para diferentes coleções de imagens, incluindo [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry/). Como alternativa, as empresas podem ter um Registro privado local para suas próprias imagens do Docker.

A Figura 2-4 mostra como imagens e Registros no Docker se relacionam com outros componentes. Ela também mostra as várias ofertas de Registro dos fornecedores.

![Um diagrama que mostra a taxonomia básica no Docker.](./media/docker-containers-images-registries/taxonomy-of-docker-terms-and-concepts.png)

**Figura 2-4**. Taxonomia de termos e conceitos do Docker

o Registro é como uma estante de livros em que as imagens são armazenadas e ficam disponíveis para serem retiradas para a criação de contêineres para executar os serviços ou aplicativos Web. Há registros do Docker privados locais e na nuvem pública. O Hub do Docker é um registro público mantido pelo Docker, junto com o Registro Confiável do Docker, uma solução empresarial, o Azure oferece ao Registro de Contêiner do Azure. AWS, Google e outros também têm registros de contêiner.

Colocar imagens em um Registro permite a você armazenar os bits de aplicativo estáticos e imutáveis, incluindo todas as suas dependências em um nível de estrutura. A versão dessas imagens podem ser controladas e elas podem ser implantadas em vários ambientes e, portanto, fornecem uma unidade de implantação consistente.

Registros de imagem privados, hospedados localmente ou na nuvem, são recomendados quando:

- Suas imagens não devem ser compartilhadas publicamente devido à confidencialidade.

- Você deseja ter latência de rede mínima entre suas imagens e o ambiente de implantação escolhido. Por exemplo, se o ambiente de produção for uma nuvem do Azure, você provavelmente desejará armazenar as imagens no [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry/) para que a latência de rede seja mínima. De maneira semelhante, se seu ambiente de produção for local, tenha um Registro Confiável do Docker local disponível na mesma rede local.

>[!div class="step-by-step"]
>[Anterior](docker-terminology.md) 
> [Avançar](../net-core-net-framework-containers/index.md)
