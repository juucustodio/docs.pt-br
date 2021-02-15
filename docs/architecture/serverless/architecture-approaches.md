---
title: Abordagens de arquitetura-aplicativos sem servidor
description: Uma introdução às abordagens de arquitetura para a criação de aplicativos empresariais baseados em nuvem, desde arquiteturas de N camadas até servidores.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 0ab84d1f3425c1fda787756b73fd8315fe6d4231
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171969"
---
# <a name="architecture-approaches"></a>Abordagens de arquitetura

Entender as abordagens existentes para arquitetar aplicativos empresariais ajuda a esclarecer a função desempenhada por servidor. Há muitas abordagens e padrões que evoluíram mais de décadas de desenvolvimento de software, e todos têm seus próprios prós e contras. Em muitos casos, a solução definitiva pode não envolver a decisão de uma única abordagem, mas pode integrar várias abordagens. Cenários de migração geralmente envolvem a mudança de uma abordagem de arquitetura para outra por meio de uma abordagem híbrida.

Este capítulo fornece uma visão geral dos padrões de arquitetura física e lógica para aplicativos empresariais.

## <a name="architecture-patterns"></a>Padrões de arquitetura

Os aplicativos de negócios modernos seguem uma variedade de padrões de arquitetura. Esta seção representa uma pesquisa de padrões comuns. Os padrões listados aqui não são necessariamente todas as práticas recomendadas, mas ilustram abordagens diferentes.

Para obter mais informações, consulte [Guia de arquitetura do aplicativo do Azure](/azure/architecture/guide/).

## <a name="monoliths"></a>Monolitos

Muitos aplicativos de negócios seguem um padrão monolítico. Os aplicativos herdados são frequentemente implementados como monolíticos. No padrão monolítico, todas as preocupações do aplicativo estão contidas em uma única implantação. Tudo, desde a interface do usuário até chamadas de banco de dados, está incluído na mesma base de código.

![Arquitetura monolítica](./media/monolith-architecture.png)

Há várias vantagens para a abordagem monolítica. Geralmente, é fácil puxar uma única base de código e começar a trabalhar. O tempo de crescimento pode ser menor, e a criação de ambientes de teste é tão simples quanto fornecer uma nova cópia. O monolítico pode ser projetado para incluir vários componentes e aplicativos.

Infelizmente, o padrão monolítico tende a dividir em escala. As principais desvantagens da abordagem monolítica incluem:

- Difícil de trabalhar em paralelo na mesma base de código.
- Qualquer alteração, independentemente de como o trivial, exige a implantação de uma nova versão de todo o aplicativo.
- A refatoração afeta potencialmente o aplicativo inteiro.
- Geralmente, a única solução a ser dimensionada é criar várias cópias com uso intensivo de recursos do monolítico.
- À medida que os sistemas expandem ou outros sistemas são adquiridos, a integração pode ser difícil.
- Pode ser difícil testar devido à necessidade de configurar todo o monolítico.
- A reutilização de código é desafiadora e, muitas vezes, outros aplicativos acabam tendo suas próprias cópias de código.

Muitas empresas procuram a nuvem como uma oportunidade de migrar aplicativos monolíticos e, ao mesmo tempo, refatorá-los para padrões mais utilizáveis. É comum dividir os aplicativos e componentes individuais para permitir que eles sejam mantidos, implantados e dimensionados separadamente.

## <a name="n-layer-applications"></a>Aplicativos de N camadas

Lógica de aplicativo de partição de aplicativo de N camadas em camadas específicas. As camadas mais comuns incluem:

- Interface do usuário
- Lógica de negócios
- Acesso de dados

Outras camadas podem incluir middleware, processamento em lotes e API. É importante observar que as camadas são lógicas. Embora eles sejam desenvolvidos isoladamente, eles podem ser implantados na mesma plataforma de destino.

![Arquitetura de N camadas](./media/n-layer-architecture.png)

Há várias vantagens na abordagem de N camadas, incluindo:

- A refatoração é isolada em uma camada.
- As equipes podem criar, testar, implantar e manter camadas separadas de forma independente.
- As camadas podem ser trocadas, por exemplo, a camada de dados pode acessar vários bancos de dado sem a necessidade de alterações na camada da interface do usuário.

Sem servidor pode ser usado para implementar uma ou mais camadas.

## <a name="microservices"></a>Microsserviços

As arquiteturas de **[microserviços](/azure/architecture/guide/architecture-styles/microservices)** contêm características comuns que incluem:

- Os aplicativos são compostos por vários serviços pequenos.
- Cada serviço é executado em seu próprio processo.
- Os serviços são alinhados em relação a domínios de negócios.
- Os serviços se comunicam por meio de APIs leves, normalmente usando HTTP como transporte.
- Os serviços podem ser implantados e atualizados de forma independente.
- Os serviços não são dependentes de um único repositório de dados.
- O sistema foi projetado com falha em mente e o aplicativo ainda pode ser executado mesmo quando determinados serviços falham.

Os microserviços não precisam ser mutuamente exclusivos a outras abordagens de arquitetura. Por exemplo, uma arquitetura de N camadas pode usar microserviços para a camada intermediária. Também é possível implementar os microserviços de várias maneiras, desde diretórios virtuais em hosts IIS até contêineres. As características dos microserviços os tornam especialmente ideais para implementações sem servidor.

![Arquitetura de microsserviços](./media/microservices-architecture.png)

Os prós de arquiteturas de microserviço incluem:

- A refatoração geralmente é isolada para um único serviço.
- Os serviços podem ser atualizados independentemente um do outro.
- Resiliência e elasticidade podem ser ajustadas às demandas de serviços individuais.
- O desenvolvimento pode ocorrer em paralelo em diferentes equipes e plataformas.
- É mais fácil escrever testes abrangentes para serviços isolados.

Os microserviços vêm com seus próprios desafios, incluindo:

- Determinar quais serviços estão disponíveis e como chamá-los.
- Gerenciando o ciclo de vida dos serviços.
- Entender como os serviços se integram no aplicativo geral.
- Teste completo do sistema de chamadas feitas em diferentes serviços.

Por fim, há soluções para lidar com todos esses desafios, incluindo o aproveitamento dos benefícios do sem servidor que são discutidos posteriormente.

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](architecture-deployment-approaches.md)
