---
title: Resumo
description: Um resumo das principais conclusões da arquitetura Cloud-Native aplicativos .NET para o guia do Azure/livro eletrônico.
ms.date: 05/13/2020
ms.openlocfilehash: e0325b1bb6961c865e904779496950031db8db0b
ms.sourcegitcommit: 6d1ae17e60384f3b5953ca7b45ac859ec6d4c3a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94982349"
---
# <a name="summary"></a>Resumo

Em resumo, aqui estão as conclusões importantes deste guia:

- **A nuvem nativa** é sobre o design de aplicativos modernos que adotam alteração rápida, grande escala e resiliência, em ambientes modernos e dinâmicos, como nuvens públicas, privadas e híbridas.

- A **CNCF ( [nuvem Native Computing Foundation](https://www.cncf.io/) )** é um consórcio de código aberto influente de mais de 300 corporações principais. É responsável por conduzir a adoção de computação nativa de nuvem em pilhas de tecnologia e nuvem.

- As **diretrizes de CNCF** recomendam que os aplicativos nativos de nuvem adotem seis pilares importantes, como mostra a Figura 11-1:

  ![Pilares básicos nativos da nuvem](./media/cloud-native-foundational-pillars.png)

  **Figura 11-1**. Pilares básicos nativos da nuvem

- Esses pilares nativos de nuvem incluem:
  - A nuvem e seu modelo de serviço subjacente
  - Princípios de design modernos
  - Microsserviços
  - Contêinerização e orquestração de contêiner
  - Serviços de backup baseados em nuvem, como bancos de dados e agentes de mensagens
  - Automação, incluindo infraestrutura como código e implantação de código

- **Kubernetes** é o ambiente de Hospedagem de sua escolha para a maioria dos aplicativos nativos de nuvem. Os serviços menores e simples são, às vezes, hospedados em plataformas sem servidor, como Azure Functions. Entre muitos dos principais recursos de automação, ambos os ambientes fornecem dimensionamento automático para lidar com volumes de carga de trabalho flutuantes.

- A **comunicação do serviço** se torna uma decisão de design significativa ao construir um aplicativo nativo de nuvem. Os aplicativos normalmente expõem um gateway de API para gerenciar a comunicação de cliente de front-end. Em seguida, os microserviços de back-end buscam se comunicar entre si, implementando padrões de comunicação assíncrona, quando possível.

- o **gRPC** é uma estrutura moderna de alto desempenho que evolui o Protocolo RPC (chamada de procedimento remoto) antigo. Os aplicativos nativos de nuvem geralmente adotam o gRPC para simplificar o sistema de mensagens entre serviços de back-end. gRPC usa HTTP/2 para seu protocolo de transporte. Pode ser até 8x mais rápido do que a serialização JSON com tamanhos de mensagem 60-80% menores. o gRPC é de software livre e é gerenciado pela CNCF (nuvem Native Computing Foundation).

- **Os dados distribuídos** são um modelo geralmente implementado por aplicativos nativos de nuvem. Os aplicativos segregam a funcionalidade de negócios em microserviços pequenos e independentes. Cada microserviço encapsula suas próprias dependências, dados e estado. O modelo de banco de dados compartilhado clássico evolui em um dos muitos bancos de dados menores, cada um alinhado a um microserviço. Quando a fumaça é nítida, surgemos um design que expõe um `database-per-microservice` modelo.

- **Os bancos de dados não-SQL** se referem a armazenamentos não relacionais de alto desempenho. Eles se destacam em suas características de facilidade de uso, escalabilidade, resiliência e disponibilidade. Serviços de alto volume que exigem tempo de resposta de subsegundo favorecem armazenamentos de bancos de serviços NoSQL. A proliferação de tecnologias NoSQL para sistemas nativos de nuvem distribuída não pode ser sobredimensionada.

- O **NewSQL** é uma tecnologia de banco de dados emergente que combina a escalabilidade distribuída do NoSQL e as garantias acid de um banco de dados relacional. Os bancos de dados NewSQL visam sistemas de negócios que devem processar altos volumes de data, em ambientes distribuídos, com conformidade transacional/ACID completa. A CNCF (nuvem Native Computing Foundation) apresenta vários projetos de banco de dados NewSQL.

- A **resiliência** é a capacidade do seu sistema de reagir à falha e ainda continuar funcionando. Os sistemas nativos de nuvem adotam a arquitetura distribuída onde a falha é inevitável. Os aplicativos devem ser construídos para responder de forma elegante à falha e retornar rapidamente a um estado totalmente funcional.

- As **malhas de serviço** são uma camada de infraestrutura configurável com recursos internos para lidar com a comunicação do serviço e com outros desafios abrangentes. Eles descombinam responsabilidades de seu código comercial. Essas responsabilidades se movem para um proxy de serviço. Conhecido como o `Sidecar pattern` , o proxy é implantado em um processo separado para fornecer isolamento do seu código comercial.

- A **Observação** é uma consideração de design importante para aplicativos nativos de nuvem. À medida que os serviços são distribuídos em um cluster de nós, o registro em log centralizado, o monitoramento e os alertas tornam-se obrigatórios. Azure Monitor é uma coleção de ferramentas baseadas em nuvem projetadas para fornecer visibilidade do estado do seu sistema.

- A **Infraestrutura como código** é uma prática amplamente aceita que automatiza o provisionamento de plataforma. Sua infraestrutura e implantações são automatizadas, consistentes e reproduzíveis. Ferramentas como Azure Resource Manager, Terraform e o CLI do Azure, permitem que você declarate o script de infraestrutura de nuvem de forma declarativa.

- A **automação de código** é um requisito para aplicativos nativos de nuvem. Os sistemas de CI/CD modernos ajudam a atender a esse princípio. Eles fornecem etapas de compilação e implantação separadas que ajudam a garantir o código consistente e de qualidade. O estágio de compilação transforma o código em um artefato binário. O estágio de lançamento pega o artefato binário, aplica a configuração de ambiente externo e o implanta em um ambiente especificado. O Azure DevOps e o GitHub são ambientes de DevOps com recursos completos.

>[!div class="step-by-step"]
>[Anterior](application-bundles.md)
