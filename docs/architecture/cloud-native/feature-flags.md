---
title: Sinalizadores de recurso
description: Implementar sinalizadores de recurso em aplicativos nativos de nuvem utilizando Azure App config
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: ee45c9f187b056887ea6dd3a08da508afca51987
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91158091"
---
# <a name="feature-flags"></a>Sinalizadores de recurso

No capítulo 1, afirmamos que a nuvem nativa é muito sobre velocidade e agilidade. Os usuários esperam uma rápida capacidade de resposta, recursos inovadores e zero tempo de inatividade. `Feature flags` é uma técnica de implantação moderna que ajuda a aumentar a agilidade para aplicativos nativos de nuvem. Eles permitem que você implante novos recursos em um ambiente de produção, mas restrinja sua disponibilidade. Com o movimento de um comutador, você pode ativar um novo recurso para usuários específicos sem reiniciar o aplicativo ou implantar um novo código. Eles separam o lançamento dos novos recursos da implantação de código.

Os sinalizadores de recurso são criados sobre a lógica condicional que controla a visibilidade da funcionalidade para usuários em tempo de execução. Em sistemas nativos de nuvem modernos, é comum implantar novos recursos no início da produção, mas testá-los com um público limitado. À medida que a confiança aumenta, o recurso pode ser distribuído incrementalmente para públicos mais largos.

Outros casos de uso para sinalizadores de recurso incluem:

- Restrinja a funcionalidade premium a grupos de clientes específicos dispostos a pagar taxas de assinatura maiores.
- Estabilizar um sistema ao desativar rapidamente um recurso de problema, evitando os riscos de uma reversão ou um hotfix imediato.
- Desabilite um recurso opcional com alto consumo de recursos durante períodos de pico de uso.
- Conduza `experimental feature releases` a pequenos segmentos de usuário para validar a viabilidade e a popularidade.

Os sinalizadores de recurso também promovem o `trunk-based` desenvolvimento. É um modelo de ramificação de controle de origem em que os desenvolvedores colaboram em recursos em uma única ramificação. A abordagem minimiza o risco e a complexidade de Mesclar grandes números de branches de recursos de longa execução. Os recursos ficam indisponíveis até serem ativados.

## <a name="implementing-feature-flags"></a>Implementando sinalizadores de recurso

Em seu núcleo, um sinalizador de recurso é uma referência a um simples `decision object` . Ele retorna um estado booliano de `on` ou `off` . O sinalizador normalmente encapsula um bloco de código que encapsula uma funcionalidade de recurso. O estado do sinalizador determina se o bloco de código é executado para um determinado usuário. A Figura 10-11 mostra a implementação.

```csharp
if (featureFlag) {
    // Run this code block if the featureFlag value is true
} else {
    // Run this code block if the featureFlag value is false
}
```

**Figura 10-11** – implementação de sinalizador de recurso simples.

Observe como essa abordagem separa a lógica de decisão do código de recurso.

No capítulo 1, discutimos o `Twelve-Factor App` . As diretrizes recomendadas para manter as definições de configuração externas do código executável do aplicativo. Quando necessário, as configurações podem ser lidas na fonte externa. Os valores de configuração do sinalizador de recurso também devem ser independentes da base de código. Ao externalizar a configuração do sinalizador em um repositório separado, você pode alterar o estado do sinalizador sem modificar e reimplantar o aplicativo.

[Azure app configuração](/azure/azure-app-configuration/overview) fornece um repositório centralizado para sinalizadores de recursos. Com ele, você define diferentes tipos de sinalizadores de recursos e manipula seus Estados de forma rápida e confiável. Você adiciona as bibliotecas de cliente de configuração de aplicativo ao seu aplicativo para habilitar a funcionalidade de sinalizador de recurso. Há suporte para várias estruturas de linguagem de programação.

Os sinalizadores de recurso podem ser facilmente implementados em um [serviço ASP.NET Core](/azure/azure-app-configuration/use-feature-flags-dotnet-core). A instalação das bibliotecas de gerenciamento de recursos do .NET e do provedor de configuração de aplicativo permite que você adicione sinalizadores de recurso declarativamente ao seu código. Eles habilitam `FeatureGate` atributos para que você não precise gravar manualmente as instruções if na base de código.

Uma vez configurado em sua classe de inicialização, você pode adicionar a funcionalidade de sinalizador de recurso no nível do controlador, da ação ou do middleware. A Figura 10-12 apresenta a implementação do controlador e da ação:

```csharp
[FeatureGate(MyFeatureFlags.FeatureA)]
public class ProductController : Controller
{
    ...
}
```

```csharp
[FeatureGate(MyFeatureFlags.FeatureA)]
public IActionResult UpdateProductStatus()
{
    return ObjectResult(ProductDto);
}
```

**Figura 10-12** -implementação do sinalizador de recurso em um controlador e uma ação.

Se um sinalizador de recurso estiver desabilitado, o usuário receberá um código de status 404 (não encontrado) sem nenhum corpo de resposta.

Os sinalizadores de recurso também podem ser injetados diretamente em classes C#. A Figura 10-13 mostra a injeção do sinalizador de recurso:

```csharp
public class ProductController : Controller
{
    private readonly IFeatureManager _featureManager;

    public ProductController(IFeatureManager featureManager)
    {
        _featureManager = featureManager;
    }
}
```

**Figura 10-13** -injeção de sinalizador de recurso em uma classe.

As bibliotecas de gerenciamento de recursos gerenciam o ciclo de vida do sinalizador de recursos em segundo plano. Por exemplo, para minimizar um número alto de chamadas para o repositório de configuração, o sinalizador cache de bibliotecas indica uma duração especificada. Eles podem garantir a imutabilidade dos Estados de sinalizador durante uma chamada de solicitação. Eles também oferecem um `Point-in-time snapshot` . Você pode reconstruir o histórico de qualquer valor-chave e fornecer seu valor passado a qualquer momento nos sete dias anteriores.

>[!div class="step-by-step"]
>[Anterior](devops.md) 
> [Avançar](infrastructure-as-code.md)
