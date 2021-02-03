---
title: Como registrar em log com a pilha elástica
description: Registro em log usando Stack elástico, Logstash e Kibana
ms.date: 01/19/2021
ms.openlocfilehash: ebe7eef16d3b1a73d0fd3a010a509bbaf7be3fd5
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505811"
---
# <a name="logging-with-elastic-stack"></a>Como registrar em log com a pilha elástica

Há muitas boas ferramentas de registro em log centralizadas e elas variam de acordo com as ferramentas gratuitas de software livre, até opções mais caras. Em muitos casos, as ferramentas gratuitas são tão boas ou melhores do que as ofertas pagas. Uma dessas ferramentas é uma combinação de três componentes de código-fonte aberto: pesquisa elástica, Logstash e Kibana.

Coletivamente, essas ferramentas são conhecidas como pilha elástica ou pilha ELK.

## <a name="elastic-stack"></a>Pilha elástica

A pilha elástica é uma opção avançada para coletar informações de um cluster kubernetes. O kubernetes dá suporte ao envio de logs para um ponto de extremidade Elasticsearch e, na [maioria das vezes](https://kubernetes.io/docs/tasks/debug-application-cluster/logging-elasticsearch-kibana/), tudo o que você precisa para começar é definir as variáveis de ambiente, conforme mostrado na Figura 7-5:

```kubernetes
KUBE_LOGGING_DESTINATION=elasticsearch
KUBE_ENABLE_NODE_LOGGING=true
```

**Figura 7-5**. Variáveis de configuração para kubernetes

Esta etapa instalará o Elasticsearch no cluster e o destino enviando todos os logs de cluster para ele.

![Um exemplo de um painel de Kibana mostrando os resultados de uma consulta em relação a logs ingeridos da ](./media/kibana-dashboard.png)
 **figura kubernetes 7-6**. Um exemplo de um painel de Kibana que mostra os resultados de uma consulta em relação aos logs que são ingeridos do kubernetes

## <a name="what-are-the-advantages-of-elastic-stack"></a>Quais são as vantagens da pilha elástica?

A pilha elástica fornece registro em log centralizado de maneira econômica, escalonável e fácil de ser compatível com a nuvem. Sua interface do usuário simplifica a análise de dados para que você possa passar o seu tempo coletando informações de seus dados em vez de combater uma interface desajeitado. Ele dá suporte a uma ampla variedade de entradas, de forma que o aplicativo distribuído se estenda por mais e tipos diferentes de serviços, você pode esperar continuar a poder alimentar o log e os dados de métrica no sistema. A pilha elástica também dá suporte a pesquisas rápidas mesmo em grandes conjuntos de dados, o que possibilita até que aplicativos grandes registrem dados detalhados e ainda possam ter visibilidade dele de forma eficaz.

## <a name="logstash"></a>Logstash

O primeiro componente é [Logstash](https://www.elastic.co/products/logstash). Essa ferramenta é usada para coletar informações de log de uma grande variedade de fontes diferentes. Por exemplo, Logstash pode ler logs do disco e também receber mensagens de bibliotecas de log, como [Serilog](https://serilog.net/). O Logstash pode fazer alguma filtragem básica e expansão nos logs à medida que eles chegam. Por exemplo, se os logs contiverem endereços IP, Logstash poderá ser configurado para fazer uma pesquisa geográfica e obter um país ou até mesmo uma cidade de origem para essa mensagem.

Serilog é uma biblioteca de registro em log para linguagens .NET, que permite o registro em log com parâmetros. Em vez de gerar uma mensagem de log textual que incorpore campos, os parâmetros são mantidos separados. Essa biblioteca permite a filtragem e a pesquisa mais inteligentes. Uma configuração de Serilog de exemplo para gravação em Logstash aparece na Figura 7-7.

```csharp
var log = new LoggerConfiguration()
         .WriteTo.Http("http://localhost:8080")
         .CreateLogger();
```

**Figura 7-7**. Configuração de Serilog para gravar informações de log diretamente no logstash sobre HTTP

Logstash usaria uma configuração como a mostrada na Figura 7-8.

```
input {
    http {
        #default host 0.0.0.0:8080
        codec => json
    }
}

output {
    elasticsearch {
        hosts => "elasticsearch:9200"
        index=>"sales-%{+xxxx.ww}"
    }
}
```

**Figura 7-8**. Uma configuração do Logstash para o consumo de logs do Serilog

Para cenários em que a manipulação de log extensa não é necessária, há uma alternativa ao Logstash conhecido como [batidas](https://www.elastic.co/products/beats). Os batidas são uma família de ferramentas que podem reunir uma grande variedade de dados de logs para dados de rede e informações de tempo de atividade. Muitos aplicativos usarão Logstash e batidas.

Depois que os logs forem coletados pelo Logstash, ele precisará de algum lugar para colocá-los. Embora o Logstash dê suporte a muitas saídas diferentes, um dos mais empolgantes é a pesquisa elástica.

## <a name="elastic-search"></a>Pesquisa elástica

A pesquisa elástica é um mecanismo de pesquisa poderoso que pode indexar logs à medida que eles chegam. Ele faz as consultas em execução nos logs rapidamente. A pesquisa elástica pode lidar com enormes quantidades de logs e, em casos extremos, pode ser dimensionada horizontalmente em vários nós.

As mensagens de log que foram criadas para conter parâmetros ou que tiveram parâmetros divididos por meio deles por meio do processamento de Logstash podem ser consultadas diretamente à medida que Elasticsearch preserva essas informações.

Uma consulta que pesquisa as 10 principais páginas visitadas por `jill@example.com` , aparece na figura 7-9.

```json
"query": {
    "match": {
      "user": "jill@example.com"
    }
  },
  "aggregations": {
    "top_10_pages": {
      "terms": {
        "field": "page",
        "size": 10
      }
    }
  }
```

**Figura 7-9**. Uma consulta Elasticsearch para localizar as 10 páginas principais visitadas por um usuário

## <a name="visualizing-information-with-kibana-web-dashboards"></a>Visualizando informações com painéis da Web do Kibana

O componente final da pilha é Kibana. Essa ferramenta é usada para fornecer visualizações interativas em um painel da Web. Os painéis podem ser criados mesmo por usuários que não são técnicos. A maioria dos dados residentes no índice Elasticsearch pode ser incluída nos painéis do Kibana. Usuários individuais podem ter diferentes desejos de Dashboard e o Kibana permite essa personalização por meio da permissão de painéis específicos do usuário.

## <a name="installing-elastic-stack-on-azure"></a>Instalando a pilha elástica no Azure

A pilha elástica pode ser instalada no Azure de várias maneiras. Como sempre, é possível [provisionar máquinas virtuais e instalar a pilha elástica diretamente](/azure/virtual-machines/linux/tutorial-elasticsearch)nelas. Essa opção é preferida por alguns usuários experientes, pois oferece o mais alto grau de personalização. A implantação na infraestrutura como um serviço introduz uma sobrecarga de gerenciamento significativa, forçando aqueles que tomam esse caminho para apropriar-se de todas as tarefas associadas à infraestrutura como um serviço, como proteger os computadores e manter-se atualizado com os patches.

Uma opção com menos sobrecarga é fazer uso de um dos muitos contêineres do Docker nos quais a pilha elástica já foi configurada. Esses contêineres podem ser descartados em um cluster kubernetes existente e executados junto com o código do aplicativo. O contêiner [sebp/Elk](https://elk-docker.readthedocs.io/) é um contêiner de pilha elástico bem documentado e testado.

Outra opção é uma [oferta Elk como serviço anunciada recentemente](https://devops.com/logz-io-unveils-azure-open-source-elk-monitoring-solution/).

## <a name="references"></a>Referências

- [Instalar pilha elástica no Azure](/azure/virtual-machines/linux/tutorial-elasticsearch)

>[!div class="step-by-step"]
>[Anterior](observability-patterns.md) 
> [Avançar](monitoring-azure-kubernetes.md)
