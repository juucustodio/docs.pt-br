---
title: Princípios de arquitetura
description: Projetar aplicativos Web modernos com o ASP.NET Core e o Azure | Princípios de arquitetura
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: f4079e0409c1675e8f8a3e494303683daeef29c1
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851406"
---
# <a name="architectural-principles"></a>Princípios de arquitetura

> "Se os construtores construíssem edifícios da maneira como os programadores escrevem programas, o primeiro pica-pau que surgisse destruiria a civilização."  
> _\- Gerald Weinberg_

Você deve projetar e criar soluções de software com a facilidade de manutenção em mente. Os princípios descritos nesta seção podem ajudar a orientá-lo em direção à tomada de decisões de arquitetura que resultarão em aplicativos limpos e de fácil manutenção. Em geral, esses princípios orientarão você para a criação de aplicativos fora de componentes discretos que não têm um acoplamento rígido com outras partes do aplicativo, mas que, em vez disso, se comunicam por meio de interfaces explícitas ou sistemas de mensagens.

## <a name="common-design-principles"></a>Princípios comuns de design

### <a name="separation-of-concerns"></a>Separação de interesses

Um princípio norteador durante o desenvolvimento é o da **Separação de Interesses**. Esse princípio declara que o software deve ser separado de acordo com os tipos de trabalho que ele executa. Por exemplo, considere um aplicativo que inclua uma lógica para identificar itens importantes a serem exibidos ao usuário, e que formata esses itens de uma maneira específica para torná-los mais perceptíveis. O comportamento responsável por escolher os itens a serem formatados deve ser mantido separado do comportamento responsável por formatar os itens, uma vez que esses comportamentos são questões separadas que são relacionadas apenas coincidentes entre si.

Em termos de arquitetura, os aplicativos podem ser logicamente criados para seguir esse princípio, separando o comportamento principal de negócios da infraestrutura e da lógica da interface do usuário. O ideal é que a lógica e as regras de negócio residam em um projeto separado, que não deve depender de outros projetos no aplicativo. Essa separação ajuda a garantir que o modelo de negócios seja fácil de testar e possa evoluir sem estar rigidamente acoplado a detalhes de implementação de baixo nível. A separação de interesses é uma consideração fundamental por trás do uso de camadas em arquiteturas de aplicativo.

### <a name="encapsulation"></a>Encapsulamento

Diferentes partes de um aplicativo devem usar o **encapsulamento** para isolá-las de outras partes do aplicativo. As camadas e os componentes do aplicativo devem poder ajustar sua implementação interna sem dividir seus colaboradores, desde que contratos externos não sejam violados. O uso adequado do encapsulamento ajuda a obter um acoplamento flexível e uma modularidade nos designs do aplicativo, pois os objetos e os pacotes podem ser substituídos por implementações alternativas, desde que a mesma interface seja mantida.

Nas classes, o encapsulamento é obtido por meio da limitação do acesso externo ao estado interno da classe. Se um ator externo desejar manipular o estado do objeto, ele deverá fazer isso por meio de uma função bem definida (ou um setter de propriedade), em vez de ter acesso direto ao estado particular do objeto. Da mesma forma, os componentes do aplicativo e os próprios aplicativos devem expor interfaces bem definidas para uso de seus colaboradores, em vez de permitir que seu estado seja modificado diretamente. Essa abordagem libera o design interno do aplicativo para evoluir ao longo do tempo sem se preocupar que isso fará com que os colaboradores quebrem, desde que os contratos públicos sejam mantidos.

### <a name="dependency-inversion"></a>Inversão de dependência

A direção da dependência dentro do aplicativo deve ser na direção de abstração, não os detalhes de implementação. A maioria dos aplicativos é escrita de forma que os fluxos de dependência de tempo de compilação estejam na direção da execução do tempo de execução, produzindo um grafo de dependência direta. Ou seja, se o módulo A chamar uma função no módulo B, que chama uma função no módulo C, em seguida, no momento da compilação, um dependerá de B, que dependerá de C, como mostra a Figura 4-1.

![Grafo de dependência direta](./media/image4-1.png)

**Figura 4-1.** Grafo de dependência direta.

A aplicação do princípio da inversão de dependência permite que A chame métodos em uma abstração implementada por B, possibilitando que A chame B em runtime, mas que B dependa de uma interface controlada por A em tempo de compilação (*invertendo*, portanto, a dependência típica em tempo de compilação). Em tempo de execução, o fluxo da execução do programa permanece inalterado, mas a introdução de interfaces significa que diferentes implementações dessas interfaces podem ser conectadas com facilidade.

![Grafo de dependência invertido](./media/image4-2.png)

**Figura 4-2.** Grafo de dependência invertida.

A **inversão de dependência** é uma parte fundamental da criação de aplicativos menos rígidos, já que os detalhes da implementação podem ser escritos para depender e implementar abstrações de nível superior, em vez do contrário. Como resultado, os aplicativos resultantes são mais testáveis, modulares e de manutenção mais fácil. A prática da *injeção de dependência* se tornou possível pela observância do princípio da inversão de dependência.

### <a name="explicit-dependencies"></a>Dependências explícitas

**Métodos e classes devem exigir explicitamente os objetos de colaboração de que precisam para funcionarem corretamente.** Os construtores de classe oferecem uma oportunidade para que as classes identifiquem os itens necessários para que estejam em um estado válido e funcionem corretamente. Se você definir classes que podem ser construídas e chamadas, mas que só funcionarão corretamente se determinados componentes globais ou de infraestrutura estiverem em vigor, essas classes serão *desonestos* com seus clientes. O contrato do construtor informa o cliente de que ele precisa apenas dos itens especificados (possivelmente nada se a classe estiver usando apenas um construtor sem parâmetros), mas, em seguida, em runtime, acontece que o objeto realmente precisou de outra coisa.

Seguindo o princípio da dependência explícita, os métodos e as classes estão sendo honestos com seus clientes sobre o que precisam para funcionar. Seguir o princípio torna seu código mais autodocumentado e seus contratos de codificação mais amigáveis, já que os usuários vão confiar que, desde que forneçam o que é necessário na forma de parâmetros de método ou construtor, os objetos com os quais eles estão trabalhando se comportarão corretamente no tempo de execução.

### <a name="single-responsibility"></a>Responsabilidade única

O princípio da responsabilidade única se aplica ao design orientado a objeto, mas também pode ser considerado um princípio de arquitetura semelhante à separação de interesses. Ele informa que os objetos devem ter apenas uma responsabilidade e que devem ter apenas uma única razão para serem alterados. Especificamente, a única situação na qual o objeto deve ser alterado é se a maneira na qual ele executa sua responsabilidade única precisa ser atualizada. Seguir esse princípio ajuda a produzir sistemas mais rígidos e modulares, já que muitos tipos de novo comportamento podem ser implementados como novas classes, em vez de adicionar responsabilidade adicional às classes existentes. A adição de novas classes sempre é mais segura do que a alteração das classes existentes, pois nenhum código ainda depende das novas classes.

Em um aplicativo monolítico, podemos aplicar o princípio da responsabilidade única em um alto nível às camadas do aplicativo. A responsabilidade de apresentação deve permanecer no projeto de interface do usuário, enquanto a responsabilidade de acesso a dados deve ser mantida em um projeto de infraestrutura. A lógica de negócios deve ser mantida no projeto de núcleo do aplicativo, no qual ela pode ser testada com facilidade e pode evoluir de maneira independente das outras responsabilidades.

Quando esse princípio é aplicado à arquitetura do aplicativo e levado ao seu ponto de extremidade lógico, você obtém os microserviços. Um microsserviço específico deve ter uma única responsabilidade. Caso você precise estender o comportamento de um sistema, será melhor fazer isso adicionando outros microsserviços, em vez de pela adição de responsabilidade a um existente.

[Saiba mais sobre a arquitetura de microsserviços](https://aka.ms/MicroservicesEbook)

### <a name="dont-repeat-yourself-dry"></a>DRY (Don't Repeat Yourself)

O aplicativo deve evitar a especificação de um comportamento relacionado a um conceito específico em vários lugares, pois essa prática é uma fonte de erros frequente. Em algum momento, uma alteração nos requisitos exigirá a alteração desse comportamento. É provável que pelo menos uma instância do comportamento não seja atualizada, e o sistema se comportará de forma inconsistente.

Em vez de duplicar a lógica, encapsule-a em um constructo de programação. Torne esse constructo a autoridade única sobre esse comportamento e imponha o uso desse novo constructo a qualquer outra parte do aplicativo que exija esse comportamento.

> [!NOTE]
> Evite associar um comportamento que é apenas coincidentemente repetitivo. Por exemplo, só porque duas constantes diferentes têm o mesmo valor, isso não significa que você deve ter apenas uma constante, caso elas estejam se referindo a coisas diferentes conceitualmente.

### <a name="persistence-ignorance"></a>Ignorância de persistência

A **PI** (ignorância de persistência) refere-se aos tipos que precisam ser persistidos, mas cujo código não é afetado pela opção de tecnologia de persistência. Esses tipos no .NET são, às vezes, chamados de POCOs (Objetos CRL Básicos), pois não precisam herdar de uma classe base específica nem implementar uma interface específica. A ignorância de persistência é importante porque permite que o mesmo modelo de negócios seja persistente de várias maneiras, oferecendo flexibilidade adicional ao aplicativo. As opções de persistência podem mudar ao longo do tempo, de uma tecnologia de banco de dados para outra, ou outras formas de persistência podem ser necessárias além de qualquer coisa com que o aplicativo foi iniciado (por exemplo, usando um cache Redis ou Azure Cosmos DB além de um banco de dados relacional).

Alguns exemplos de violações desse princípio incluem:

- Uma classe base necessária.

- Uma implementação de interface necessária.

- Classes responsáveis por salvar a si mesmas (como o padrão de Registro Ativo).

- Construtor sem parâmetros necessário.

- Propriedades que exigem uma palavra-chave virtual.

- Atributos necessário específicos da persistência.

O requisito de que as classes tenham um dos recursos ou comportamentos acima adiciona um acoplamento entre os tipos a serem persistidos e a opção de tecnologia de persistência, dificultando a adoção de novas estratégias de acesso a dados no futuro.

### <a name="bounded-contexts"></a>Contextos limitados

**Contextos limitados** são um padrão central no Design Controlado por Domínio. Eles fornecem uma maneira de lidar com a complexidade de aplicativos ou organizações grandes dividindo-os em módulos conceituais separados. Cada módulo conceitual representa um contexto que é separado de outros contextos (portanto, limitado) e pode evoluir de forma independente. Cada contexto limitado deve ser, de preferência, livre para escolher seus próprios nomes para conceitos dentro dele e deve ter acesso exclusivo ao seu próprio repositório de persistência.

No mínimo, os aplicativos Web individuais devem tentar ser seu próprio contexto limitado, com seu próprio repositório de persistência para seu modelo de negócios, em vez de compartilhar um banco de dados com outros aplicativos. A comunicação entre contextos limitados ocorre por meio de interfaces programáticas, em vez de por meio de um banco de dados compartilhado, o que permite que a lógica de negócios e os eventos ocorram em resposta às alterações feitas. Os contextos limitados são mapeados estreitamente aos microsserviços, que também são idealmente implementados como seus próprios contextos limitados individuais.

## <a name="additional-resources"></a>Recursos adicionais

- [Padrões de design JAVA: princípios](https://java-design-patterns.com/principles/)
- [Contexto limitado](https://martinfowler.com/bliki/BoundedContext.html)

>[!div class="step-by-step"]
>[Anterior](choose-between-traditional-web-and-single-page-apps.md) 
> [Avançar](common-web-application-architectures.md)
