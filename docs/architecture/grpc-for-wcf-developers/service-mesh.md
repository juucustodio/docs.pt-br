---
title: Malhas de serviço-gRPC para desenvolvedores do WCF
description: Usar uma malha de serviço para rotear e balancear solicitações para serviços gRPC em um cluster kubernetes.
ms.date: 12/15/2020
ms.openlocfilehash: a1c72a4facf1c133af912bbee242328653a051b6
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938124"
---
# <a name="service-meshes"></a>Malhas de serviço

Uma malha de serviço é um componente de infraestrutura que assume o controle das solicitações de serviço de roteamento em uma rede. As malhas de serviço podem lidar com todos os tipos de preocupações de nível de rede dentro de um cluster kubernetes, incluindo:

- Descoberta de serviço
- Balanceamento de carga
- Tolerância a falhas
- Criptografia
- Monitoramento

As malhas do serviço kubernetes funcionam adicionando um contêiner extra, chamado *proxy sidecar*, a cada pod incluído na malha. O proxy assume o tratamento de todas as solicitações de rede de entrada e saída. Em seguida, você pode manter a configuração e o gerenciamento de rede que são importantes separadamente dos contêineres de aplicativo. Em muitos casos, essa separação não requer nenhuma alteração no código do aplicativo.

No [exemplo do capítulo anterior](kubernetes.md#test-the-application), as solicitações gRPC do aplicativo Web foram todas roteadas para uma única instância do serviço gRPC. Isso acontece porque o nome do host do serviço é resolvido para um endereço IP e esse endereço IP é armazenado em cache durante o tempo de vida da `HttpClientHandler` instância. Pode ser possível contornar esse comportamento tratando as pesquisas de DNS manualmente ou criando vários clientes. Mas essa solução alternativa complicaria o código do aplicativo sem adicionar nenhum valor comercial ou de cliente.

Quando você usa uma malha de serviço, as solicitações do contêiner de aplicativo são enviadas para o proxy sidecar. O proxy sidecar pode então distribuí-los de forma inteligente em todas as instâncias do outro serviço. A malha também pode:

- Responda de forma direta às falhas de instâncias individuais de um serviço.
- Manipule a semântica de repetição para chamadas com falha ou tempos limite.
- Redirecionar solicitações com falha para uma instância alternativa sem retornar ao aplicativo cliente.

A captura de tela a seguir mostra o aplicativo StockWeb em execução com a malha de serviço do Linkerd. Não há nenhuma alteração no código do aplicativo e a imagem do Docker não está sendo usada. A única alteração necessária foi a adição de uma anotação à implantação nos arquivos YAML para os `stockdata` `stockweb` serviços e.

![StockWeb com malha de serviço](media/service-mesh/stockweb-servicemesh-screenshot.png)

Você pode ver na coluna **servidor** que as solicitações do aplicativo StockWeb foram roteadas para ambas as réplicas do serviço StockData, apesar de serem originadas de uma única `HttpClient` instância no código do aplicativo. Na verdade, se você examinar o código, verá que todas as solicitações de 100 para o serviço StockData são feitas simultaneamente usando a mesma `HttpClient` instância. Com a malha de serviço, essas solicitações serão balanceadas em todas as instâncias de serviço, no entanto, estão disponíveis.

As malhas de serviço aplicam-se somente ao tráfego em um cluster. Para clientes externos, consulte o próximo capítulo, [balanceamento de carga](load-balancing.md).

## <a name="service-mesh-options"></a>Opções de malha de serviço

Três implementações de malha de serviço de uso geral estão disponíveis atualmente para uso com kubernetes: [İSTİO](https://istio.io), [Linkerd](https://linkerd.io)e [Consul Connect](https://consul.io/mesh.html). Todos os três fornecem roteamento/proxy de solicitação, criptografia de tráfego, resiliência, autenticação de host para host e controle de tráfego.

Escolher uma malha de serviço depende de vários fatores:

- Os requisitos específicos da organização em relação aos custos, conformidade, planos de suporte pagos e assim por diante.
- A natureza do cluster, seu tamanho, o número de serviços implantados e o volume de tráfego na rede de cluster.
- Facilidade de implantar e gerenciar a malha e usá-la com serviços.

## <a name="example-add-linkerd-to-a-deployment"></a>Exemplo: Adicionar Linkerd a uma implantação

Neste exemplo, você aprenderá a usar a malha de serviço Linkerd com o aplicativo *StockKube* da [seção anterior](kubernetes.md).
Para seguir este exemplo, você precisará [instalar a CLI do Linkerd](https://linkerd.io/2/getting-started/#step-1-install-the-cli). Você pode baixar binários do Windows na seção que lista as versões do GitHub. Certifique-se de usar a versão *estável* mais recente e não uma das versões de borda.

Com a CLI do Linkerd instalada, siga as instruções de [introdução](https://linkerd.io/2/getting-started/index.html) para instalar os componentes do Linkerd no cluster do kubernetes. As instruções são simples e a instalação deve levar apenas alguns minutos em uma instância de kubernetes local.

### <a name="add-linkerd-to-kubernetes-deployments"></a>Adicionar Linkerd a implantações do kubernetes

A CLI do Linkerd fornece um `inject` comando para adicionar as seções e propriedades necessárias aos arquivos kubernetes. Você pode executar o comando e gravar a saída em um novo arquivo.

```console
linkerd inject stockdata.yml > stockdata-with-mesh.yml
linkerd inject stockweb.yml > stockweb-with-mesh.yml
```

Você pode inspecionar os novos arquivos para ver quais alterações foram feitas. Para objetos de implantação, uma anotação de metadados é adicionada para informar ao Linkerd para injetar um contêiner de proxy sidecar no pod quando ele é criado.

Também é possível canalizar a saída do `linkerd inject` comando `kubectl` diretamente. Os comandos a seguir funcionarão no PowerShell ou em qualquer shell do Linux.

```console
linkerd inject stockdata.yml | kubectl apply -f -
linkerd inject stockweb.yml | kubectl apply -f -
```

### <a name="inspect-services-in-the-linkerd-dashboard"></a>Inspecionar serviços no painel do Linkerd

Abra o painel do Linkerd usando a `linkerd` CLI.

```console
linkerd dashboard
```

O painel fornece informações detalhadas sobre todos os serviços que estão conectados à malha.

![Painel do Linkerd mostrando aplicativos StockKube](media/service-mesh/linkerd-screenshot.png)

Se você aumentar o número de réplicas do serviço StockData gRPC, conforme mostrado no exemplo a seguir, e atualizar a página StockWeb no navegador, você deverá ver uma mistura de IDs na coluna **servidor** . Essa combinação indica que todas as instâncias disponíveis estão atendendo a solicitações.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stockdata
  namespace: stocks
spec:
  selector:
    matchLabels:
      run: stockdata
  replicas: 2 # Increase the target number of instances
  template:
    metadata:
      annotations:
        linkerd.io/inject: enabled
      creationTimestamp: null
      labels:
        run: stockdata
    spec:
      containers:
      - name: stockdata
        image: stockdata:1.0.0
        imagePullPolicy: Never
        resources:
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
```

>[!div class="step-by-step"]
>[Anterior](kubernetes.md) 
> [Avançar](load-balancing.md)
