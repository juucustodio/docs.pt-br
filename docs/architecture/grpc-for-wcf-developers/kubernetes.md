---
title: Kubernetes-gRPC para desenvolvedores do WCF
description: Executando ASP.NET Core serviços gRPC em um cluster kubernetes.
ms.date: 12/15/2020
ms.openlocfilehash: 0b457d6fa982b5f5b983194d4aedbff0eb782f36
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938047"
---
# <a name="kubernetes"></a>Kubernetes

Embora seja possível executar contêineres manualmente em hosts do Docker, para sistemas de produção confiáveis, é melhor usar um mecanismo de orquestração de contêiner para gerenciar várias instâncias em execução em vários servidores em um cluster. Há vários mecanismos de orquestração de contêiner disponíveis, incluindo kubernetes, Docker Swarm e Apache mesos. Mas desses mecanismos, o kubernetes está longe e distante do mais usado, portanto, será o foco deste capítulo.

O kubernetes inclui a seguinte funcionalidade:

- O **agendamento** executa contêineres em vários nós em um cluster, garantindo o uso equilibrado do recurso disponível, mantendo os contêineres em execução se houver interrupções e manipulando atualizações sem interrupção para novas versões de imagens ou novas configurações.
- As **verificações de integridade** monitoram contêineres para garantir o serviço contínuo.
- O **DNS & descoberta de serviço** manipula o roteamento entre serviços em um cluster.
- A **entrada** expõe os serviços selecionados externamente e geralmente fornece balanceamento de carga entre instâncias desses serviços.
- O **Gerenciamento de recursos** anexa recursos externos, como armazenamento a contêineres.

Este capítulo detalha como implantar um serviço de ASP.NET Core gRPC e um site que consome o serviço em um cluster kubernetes. O aplicativo de exemplo usado está disponível no repositório [dotnet-Architecture/grpc-for-WCF-Developers](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/KubernetesSample) no github.

## <a name="kubernetes-terminology"></a>Terminologia do kubernetes

O kubernetes usa a *configuração de estado desejado*: a API é usada para descrever objetos como *pods*, *implantações* e *Serviços*, e o *plano de controle* cuida da implementação do estado desejado em todos os *nós* em um *cluster*. Um cluster kubernetes tem um nó *mestre* que executa a *API kubernetes*, com a qual você pode se comunicar de forma programática ou usando a `kubectl` ferramenta de linha de comando. `kubectl` pode criar e gerenciar objetos por meio de argumentos de linha de comando, mas funciona melhor com arquivos YAML que contêm dados de declaração para objetos kubernetes.

### <a name="kubernetes-yaml-files"></a>Arquivos kubernetes YAML

Cada arquivo kubernetes YAML terá pelo menos três propriedades de nível superior:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  # Object properties
```

A `apiVersion` propriedade é usada para especificar qual versão (e qual API) o arquivo se destina. A `kind` propriedade especifica o tipo de objeto que o YAML representa. A `metadata` propriedade contém propriedades de objeto como `name` , `namespace` e `labels` .

A maioria dos arquivos kubernetes YAML também terá uma `spec` seção que descreve os recursos e a configuração necessários para criar o objeto.

### <a name="pods"></a>Pods

Pods são as unidades básicas de execução no kubernetes. Eles podem executar vários contêineres, mas também são usados para executar contêineres únicos. O pod também inclui todos os recursos de armazenamento exigidos pelos contêineres e o endereço IP da rede.

### <a name="services"></a>Serviços

Os serviços são metaobjetos que descrevem pods (ou conjuntos de Pods) e fornecem uma maneira de acessá-los no cluster, como o mapeamento de um nome de serviço para um conjunto de endereços IP Pod usando o serviço DNS do cluster.

### <a name="deployments"></a>Implantações

As implantações são os objetos de *estado desejado* para pods. Se você criar um pod manualmente, ele não será reiniciado quando for encerrado. As implantações são usadas para informar ao cluster quais pods e quantas réplicas desses pods devem estar em execução no momento atual.

### <a name="other-objects"></a>Outros objetos

Os pods, serviços e implantações são apenas três dos tipos de objetos mais básicos. Há dezenas de outros tipos de objeto que são gerenciados por clusters kubernetes. Para obter mais informações, consulte a documentação de [conceitos do kubernetes](https://kubernetes.io/docs/concepts/) .

### <a name="namespaces"></a>Namespaces

Os clusters kubernetes são projetados para dimensionar para centenas ou milhares de nós e para executar números semelhantes de serviços. Para evitar conflitos entre nomes de objeto, os namespaces são usados para agrupar objetos juntos como parte de aplicativos maiores. Os próprios serviços do kubernetes são executados em um `default` namespace. Todos os objetos de usuário devem ser criados em seus próprios namespaces para evitar possíveis conflitos com objetos padrão ou outros locatários no cluster.

## <a name="get-started-with-kubernetes"></a>Introdução ao Kubernetes

Se você estiver executando o Docker desktop para Windows ou o Docker desktop para Mac, o kubernetes já estará disponível. Basta habilitá-lo na seção **kubernetes** da janela **configurações** :

![Habilitar kubernetes no Docker desktop](media/kubernetes/enable-kubernetes-docker-desktop-v2.png)

Para executar um cluster kubernetes local no Linux, considere [minikube](https://github.com/kubernetes/minikube)ou [MicroK8s](https://microk8s.io/) se sua distribuição do Linux oferecer suporte a [snaps](https://snapcraft.io/).

Para confirmar se o cluster está em execução e acessível, execute o `kubectl version` comando:

```console
kubectl version
Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.3", GitCommit:"1e11e4a2108024935ecfcb2912226cedeafd99df", GitTreeState:"clean", BuildDate:"2020-10-14T12:50:19Z", GoVersion:"go1.15.2", Compiler:"gc", Platform:"windows/amd64"}
Server Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.3", GitCommit:"1e11e4a2108024935ecfcb2912226cedeafd99df", GitTreeState:"clean", BuildDate:"2020-10-14T12:41:49Z", GoVersion:"go1.15.2", Compiler:"gc", Platform:"linux/amd64"}
```

Neste exemplo, a `kubectl` CLI e o servidor kubernetes estão executando a versão 1.14.6. Cada versão do `kubectl` deve dar suporte à versão anterior e à próxima do servidor, portanto, `kubectl` 1,14 também deve funcionar com as versões 1,13 e 1,15 do servidor.

## <a name="run-services-on-kubernetes"></a>Executar serviços no kubernetes

O aplicativo de exemplo tem um `kube` diretório que contém três arquivos YAML. O `namespace.yml` arquivo declara um namespace personalizado: `stocks` . O `stockdata.yml` arquivo declara a implantação e o serviço para o aplicativo gRPC, e o `stockweb.yml` arquivo declara a implantação e o serviço para um aplicativo web ASP.NET Core 5,0 MVC que consome o serviço gRPC.

Para usar um `YAML` arquivo com `kubectl` o, execute o `apply -f` comando:

```console
kubectl apply -f object.yml
```

O `apply` comando verificará a validade do arquivo YAML e exibirá todos os erros recebidos da API, mas não aguardará até que todos os objetos declarados no arquivo tenham sido criados, pois essa etapa pode levar algum tempo. Use o `kubectl get` comando com os tipos de objeto relevantes para verificar a criação de objetos no cluster.

### <a name="the-namespace-declaration"></a>A declaração de namespace

A declaração de namespace é simples e requer apenas a atribuição de um `name` :

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: stocks
```

Use `kubectl` para aplicar o `namespace.yml` arquivo e confirmar que o namespace foi criado com êxito:

```console
> kubectl apply -f namespace.yml
namespace/stocks created

> kubectl get namespaces
NAME              STATUS   AGE
stocks            Active   2m53s
```

### <a name="the-stockdata-application"></a>O aplicativo StockData

O `stockdata.yml` arquivo declara dois objetos: uma implantação e um serviço.

#### <a name="the-stockdata-deployment"></a>A implantação do StockData

A parte de implantação do arquivo YAML fornece o `spec` para a implantação em si, incluindo o número de réplicas necessárias e um `template` para os objetos Pod a serem criados e gerenciados pela implantação. Observe que os objetos de implantação são gerenciados pela `apps` API, conforme especificado em `apiVersion` , em vez da API principal do kubernetes.

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
  replicas: 1
  template:
    metadata:
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

A `spec.selector` propriedade é usada para corresponder a execução de pods na implantação. A propriedade do pod `metadata.labels` deve corresponder à `matchLabels` propriedade ou a chamada à API falhará.

A `template.spec` seção declara o contêiner a ser executado. Quando você estiver trabalhando com um cluster kubernetes local, como o fornecido pela área de trabalho do Docker, poderá especificar imagens que foram criadas localmente, desde que tenham uma marca de versão.

> [!IMPORTANT]
> Por padrão, o kubernetes sempre verificará e tentará efetuar pull de uma nova imagem. Se não conseguir localizar a imagem em nenhum de seus repositórios conhecidos, a criação do pod falhará. Para trabalhar com imagens locais, defina `imagePullPolicy` como `Never` .

A `ports` propriedade especifica quais portas de contêiner devem ser publicadas no pod. A `stockservice` imagem executa o serviço na porta http padrão, portanto, a porta 80 é publicada.

A `resources` seção aplica limites de recursos ao contêiner em execução no pod. Essa é uma boa prática porque impede que um pod individual consuma toda a CPU ou memória disponível em um nó.

> [!NOTE]
> ASP.NET Core 5,0 foi otimizado e ajustado para ser executado em contêineres limitados por recursos. A `dotnet/core/aspnet` imagem do Docker define uma variável de ambiente para informar ao `dotnet` tempo de execução que ele está em um contêiner.

#### <a name="the-stockdata-service"></a>O serviço StockData

A parte de serviço do arquivo YAML declara o serviço que fornece acesso ao pods dentro do cluster.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: stockdata
  namespace: stocks
spec:
  ports:
  - port: 80
  selector:
    run: stockdata
```

O serviço `spec` usa a `selector` propriedade para corresponder à execução `Pods` , neste caso, procurando pods que têm um rótulo `run: stockdata` . O especificado `port` na correspondência de pods é publicado pelo serviço nomeado. Outros pods em execução no `stocks` namespace podem acessar http nesse serviço usando `http://stockdata` como o endereço. O pods em execução em outros namespaces pode usar o `http://stockdata.stocks` nome do host. Você pode controlar o acesso ao serviço de namespace cruzado usando [as políticas de rede](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

#### <a name="deploy-the-stockdata-application"></a>Implantar o aplicativo StockData

Use `kubectl` para aplicar o `stockdata.yml` arquivo e confirmar que a implantação e o serviço foram criados:

```console
> kubectl apply -f .\stockdata.yml
deployment.apps/stockdata created
service/stockdata created

> kubectl get deployment stockdata --namespace stocks
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
stockdata   1/1     1            1           17s

> kubectl get service stockdata --namespace stocks
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
stockdata   ClusterIP   10.97.132.103   <none>        80/TCP    33s
```

### <a name="the-stockweb-application"></a>O aplicativo StockWeb

O `stockweb.yml` arquivo declara a implantação e o serviço para o aplicativo MVC.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stockweb
  namespace: stocks
spec:
  selector:
    matchLabels:
      run: stockweb
  replicas: 1
  template:
    metadata:
      labels:
        run: stockweb
    spec:
      containers:
      - name: stockweb
        image: stockweb:1.0.0
        imagePullPolicy: Never
        resources:
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
        env:
        - name: StockData__Address
          value: "http://stockdata"
        - name: DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2UNENCRYPTEDSUPPORT
          value: "true"

---

apiVersion: v1
kind: Service
metadata:
  name: stockweb
  namespace: stocks
spec:
  type: NodePort
  ports:
  - port: 80
  selector:
    run: stockweb
```

#### <a name="environment-variables"></a>Variáveis de ambiente

A `env` seção do objeto de implantação especifica as variáveis de ambiente a serem definidas no contêiner que está executando as `stockweb:1.0.0` imagens.

A **`StockData__Address`** variável de ambiente será mapeada para a `StockData:Address` definição de configuração graças ao provedor de configuração EnvironmentVariables. Essa configuração usa sublinhados duplos entre nomes para separar seções. O endereço usa o nome do serviço `stockdata` , que está em execução no mesmo namespace kubernetes.

A **`DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2UNENCRYPTEDSUPPORT`** variável de ambiente define uma <xref:System.AppContext> opção que HABILITA conexões http/2 não criptografadas para o <xref:System.Net.Http.HttpClient> . Essa variável de ambiente faz a mesma coisa que definir a opção no código, como mostrado aqui:

```csharp
AppContext.SetSwitch("System.Net.Http.SocketsHttpHandler.Http2UnencryptedSupport", true);
```

Se você usar uma variável de ambiente para a opção, poderá alterar facilmente o contexto dependendo do contexto no qual o aplicativo está sendo executado.

#### <a name="service-types"></a>Tipos de serviços

A `type: NodePort` propriedade é usada para tornar o aplicativo Web acessível de fora do cluster. Esse tipo de propriedade faz com que o kubernetes publique a porta 80 no serviço em uma porta arbitrária nos soquetes de rede externa do cluster. Você pode encontrar a porta atribuída usando o `kubectl get service` comando.

O `stockdata` serviço não deve ser acessível de fora do cluster, portanto, ele usa o tipo padrão, `ClusterIP` .

Os sistemas de produção provavelmente usarão um balanceador de carga integrado para expor aplicativos públicos a consumidores externos. Os serviços expostos dessa maneira devem usar o `LoadBalancer` tipo.

Para obter mais informações sobre tipos de serviço, consulte a documentação [dos serviços de publicação do kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) .

#### <a name="deploy-the-stockweb-application"></a>Implantar o aplicativo StockWeb

Use `kubectl` para aplicar o `stockweb.yml` arquivo e confirmar que a implantação e o serviço foram criados:

```console
> kubectl apply -f .\stockweb.yml
deployment.apps/stockweb created
service/stockweb created

> kubectl get deployment stockweb --namespace stocks
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
stockweb   1/1     1            1           8s

> kubectl get service stockweb --namespace stocks
NAME       TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
stockweb   NodePort   10.106.141.5   <none>        80:32564/TCP   13s
```

A saída do `get service` comando mostra que a porta http foi publicada na porta `32564` na rede externa. Para o Docker desktop, esse endereço IP será localhost. Você pode acessar o aplicativo navegando até `http://localhost:32564` .

### <a name="test-the-application"></a>Testar o aplicativo

O aplicativo StockWeb exibe uma lista de ações de NASDAQ que são recuperadas de um serviço de solicitação-resposta simples. Para esta demonstração, cada linha também mostra a ID exclusiva da instância do serviço que a retornou.

![Captura de tela StockWeb](media/kubernetes/stockweb-screenshot.png)

Se o número de réplicas do `stockdata` serviço tiver sido aumentado, você poderá esperar que o valor do **servidor** mude de uma linha para uma linha, mas, na verdade, todos os registros 100 sempre serão retornados da mesma instância. Se você atualizar a página a cada poucos segundos, a ID do servidor permanecerá a mesma. Por que isso acontece? Há dois fatores em jogo aqui.

Primeiro, o sistema de descoberta de serviço kubernetes usa o balanceamento de carga Round Robin por padrão. Na primeira vez que o servidor DNS for consultado, ele retornará o primeiro endereço IP correspondente para o serviço. Na próxima vez, ele retornará o próximo endereço IP na lista, e assim por diante, até o final. Nesse ponto, ele faz um loop de volta para o início.

Em segundo lugar, o `HttpClient` usado para o cliente gRPC do aplicativo StockWeb é criado e gerenciado pelo [ASP.NET Core HttpClientFactory](../microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests.md)e uma única instância desse cliente é usada para cada chamada à página. O cliente faz apenas uma pesquisa DNS, de modo que todas as solicitações são roteadas para o mesmo endereço IP. E como o `HttpClientHandler` é armazenado em cache por motivos de desempenho, várias solicitações em uma rápida  sucessão usarão o mesmo endereço IP, até que a entrada DNS armazenada em cache expire ou a instância do manipulador seja descartada por algum motivo.

O resultado é que, por padrão, as solicitações para um serviço gRPC não são balanceadas em todas as instâncias desse serviço no cluster. Consumidores diferentes usarão instâncias diferentes, mas isso não garante uma boa distribuição de solicitações ou um uso balanceado de recursos.

O próximo capítulo, [malhas de serviço](service-mesh.md), resolverá esse problema.

>[!div class="step-by-step"]
>[Anterior](docker.md) 
> [Avançar](service-mesh.md)
