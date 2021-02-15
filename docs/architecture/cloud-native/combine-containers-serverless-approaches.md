---
title: Combinando contêineres e abordagens sem servidor para serviços nativos de nuvem
description: Combinando contêineres e kubernetes com abordagens sem servidor
ms.date: 05/13/2020
ms.openlocfilehash: b1b85519ce02ddd1d69735d872cf24fadcc81ef7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91160886"
---
# <a name="combining-containers-and-serverless-approaches"></a>Como combinar contêineres e abordagens sem servidor

Aplicativos nativos de nuvem normalmente implementam serviços que aproveitam contêineres e orquestração. Muitas vezes, há oportunidades para expor alguns dos serviços do aplicativo como Azure Functions. No entanto, com um aplicativo nativo de nuvem implantado no kubernetes, seria interessante aproveitar Azure Functions dentro desse mesmo conjunto de ferramentas. Felizmente, você pode encapsular Azure Functions dentro de contêineres do Docker e implantá-los usando os mesmos processos e ferramentas que o restante de seu aplicativo baseado em kubernetes.

## <a name="when-does-it-make-sense-to-use-containers-with-serverless"></a>Quando faz sentido usar contêineres sem servidor?

Sua função do Azure não tem conhecimento da plataforma na qual ela está implantada. Para alguns cenários, você pode ter requisitos específicos e precisa personalizar o ambiente no qual o código de função será executado. Você precisará de uma imagem personalizada que dê suporte a dependências ou a uma configuração não suportada pela imagem padrão. Nesses casos, faz sentido implantar sua função em um contêiner do Docker personalizado.

## <a name="when-should-you-avoid-using-containers-with-azure-functions"></a>Quando você deve evitar o uso de contêineres com Azure Functions?

Se você quiser usar a cobrança de consumo, não poderá executar sua função em um contêiner. Além disso, se você implantar sua função em um cluster kubernetes, não se beneficiará mais do dimensionamento interno fornecido pelo Azure Functions. Você precisará usar os recursos de dimensionamento do kubernetes, descritos anteriormente neste capítulo.

## <a name="how-to-combine-serverless-and-docker-containers"></a>Como combinar contêineres sem servidor e Docker

Para encapsular uma função do Azure em um contêiner do Docker, instale o [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools) e, em seguida, execute o seguinte comando:

```console
func init ProjectName --worker-runtime dotnet --docker
```

Quando o projeto for criado, ele incluirá um Dockerfile e o tempo de execução de trabalho configurado como `dotnet` . Agora, você pode criar e testar sua função localmente. Compile e execute-o usando  `docker build` os `docker run` comandos e. Para obter etapas detalhadas para começar a criar Azure Functions com o suporte do Docker, consulte o tutorial [criar uma função no Linux usando uma imagem personalizada](/azure/azure-functions/functions-create-function-linux-custom-image) .

## <a name="how-to-combine-serverless-and-kubernetes-with-keda"></a>Como combinar servidores e kubernetes com KEDA

Neste capítulo, você viu que a plataforma Azure Functions ' é dimensionada automaticamente para atender à demanda. Ao implantar funções em contêineres no AKS, no entanto, você perde a funcionalidade de dimensionamento interna. Para o resgate vem [com base em eventos baseados em kubernetes (Keda)](/azure/azure-functions/functions-kubernetes-keda). Ele permite o dimensionamento automático refinado para `event-driven Kubernetes workloads,` incluir funções em contêineres.

O KEDA fornece funcionalidade de dimensionamento orientada a eventos para o tempo de execução do Functions em um contêiner do Docker. KEDA pode ser dimensionado de zero instâncias (quando nenhum evento está ocorrendo) para `n instances` , com base na carga. Ele permite o dimensionamento automático expondo métricas personalizadas para o kubernetes AutoScaler (dimensionamento automático de Pod horizontal). O uso de contêineres do Functions com KEDA permite replicar recursos de função sem servidor em qualquer cluster de Kubernetes.

Vale a pena observar que o projeto KEDA agora é gerenciado pela CNCF (nuvem Native Computing Foundation).

>[!div class="step-by-step"]
>[Anterior](leverage-serverless-functions.md) 
> [Avançar](deploy-containers-azure.md)
