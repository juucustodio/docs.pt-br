---
title: Como o tempo de execução .NET e o SDK têm controle de versão
description: Este artigo explica como o .NET SDK e o tempo de execução têm controle de versão (semelhante ao controle de versões semânticos).
ms.date: 12/07/2020
ms.openlocfilehash: 2fbc2775f31b4eab1c9883282c58accd9bb2b9f5
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633618"
---
# <a name="overview-of-how-net-is-versioned"></a>Visão geral de como o .NET tem controle de versão

O [tempo de execução do .net e o SDK do .net](../introduction.md#sdk-and-runtimes) adicionam novos recursos em frequências diferentes. Em geral, o SDK é atualizado com mais frequência do que o tempo de execução. Este artigo explica o tempo de execução e os números de versão do SDK.

## <a name="versioning-details"></a>Detalhes de controle de versão

O tempo de execução do .NET tem uma abordagem principal/secundária/patch para o controle de versão que segue o [controle de versão semântico](#semantic-versioning).

O SDK do .NET não segue o controle de versão semântico. O SDK do .NET libera mais rápido e seus números de versão devem comunicar o tempo de execução alinhado e as versões secundárias e de patch próprias do SDK.

As duas primeiras posições do número de versão do SDK do .NET são bloqueadas para a versão do .NET Runtime lançada com o. Cada versão do SDK pode criar aplicativos para esse runtime ou qualquer versão inferior.

A terceira posição do número de versão do SDK comunica o número de patch e da versão secundária. A versão secundária é multiplicada por 100. Os últimos dois dígitos representam o número de patch. Versão secundária 1, versão de patch 2 seria representada como 102. Por exemplo, aqui está uma possível sequência de números de versão de tempo de execução e SDK:

| Alterar                | Execução do .NET      | SDK do .NET ( \* )     |
|-----------------------|-------------------|-------------------|
| Versão inicial       | 2.2.0             | 2.2.100           |
| Patch do SDK             | 2.2.0             | 2.2.101           |
| Tempo de execução e patch do SDK | 2.2.1             | 2.2.102           |
| Alteração de recurso do SDK    | 2.2.1             | 2.2.200           |

OBSERVAÇÕES:

- Se o SDK tiver 10 atualizações de recurso antes de uma atualização de recurso de runtime, os números de versão serão passados na série 1000 com números como 2.2.1000 de acordo com a versão do recurso 2.2.900 a seguir. Essa situação não deve ocorrer.
- As versões de patch 99 sem uma versão do recurso não ocorrerão. Se uma versão se aproximar desse número, ela forçará uma versão do recurso.

Você poderá ver mais detalhes na proposta inicial no repositório [dotnet/designs](https://github.com/dotnet/designs/pull/29).

## <a name="semantic-versioning"></a>Controle de versão semântico

O *tempo de execução* do .net está em conformidade com o [controle de versão semântica (SemVer)](https://semver.org/), adotando o uso do `MAJOR.MINOR.PATCH` controle de versão, usando as várias partes do número de versão para descrever o grau e o tipo de alteração.

```
MAJOR.MINOR.PATCH[-PRERELEASE-BUILDNUMBER]
```

As partes `PRERELEASE` e `BUILDNUMBER` opcionais nunca farão parte das versões compatíveis e existem apenas em builds noturnos, compilados localmente de destinos de origem e versões prévias sem suporte.

### <a name="understand-runtime-version-number-changes"></a>Entender as alterações do número de versão do runtime

`MAJOR` é incrementado quando:

- Ocorrem alterações significativas no produto ou uma nova direção de produto.
- Alterações interruptivas foram identificadas. Há um alto padrão para aceitar alterações interruptivas.
- Não há mais suporte para uma versão mais antiga.
- Uma versão `MAJOR` mais nova de uma dependência existente é adotada.

`MINOR` é incrementado quando:

- Uma área de superfície de API pública é adicionada.
- Um novo comportamento é adicionado.
- Uma versão `MINOR` mais nova de uma dependência existente é adotada.
- Uma nova dependência é introduzida.

`PATCH` é incrementado quando:

- Correções de bug são feitas.
- O suporte para uma plataforma mais recente é adicionado.
- Uma versão `PATCH` mais nova de uma dependência existente é adotada.
- Qualquer outra alteração que não se enquadre em um dos casos anteriores.

Quando há várias alterações, o elemento mais alto afetado por alterações individuais é incrementado e os seguintes são redefinidos como zero. Por exemplo, quando `MAJOR` é incrementado, `MINOR` e `PATCH` são redefinidos como zero. Quando `MINOR` é incrementado, `PATCH` é redefinido como zero enquanto `MAJOR` permanece inalterado.

## <a name="version-numbers-in-file-names"></a>Números de versão nos nomes de arquivo

Os arquivos baixados para .NET carregam a versão, por exemplo, `dotnet-sdk-2.1.300-win10-x64.exe` .

### <a name="preview-versions"></a>Versões prévias

As versões de visualização têm um `-preview[number]-([build]|"final")` anexado ao número de versão. Por exemplo, `2.0.0-preview1-final`.

### <a name="servicing-versions"></a>Versões de manutenção

Depois que uma versão sai, os branches de versão geralmente param de produzir builds diários e, em vez disso, iniciam a produção de builds de manutenção. As versões de manutenção têm um `-servicing-[number]` anexado à versão. Por exemplo, `2.0.1-servicing-006924`.

## <a name="relationship-to-net-standard-versions"></a>Relacionamento com versões do .NET Standard

O .NET standard consiste em um assembly de referência do .NET. Há várias implementações específicas para cada plataforma. O assembly de referência contém a definição das APIs do .NET que fazem parte de uma determinada versão do .NET Standard. Cada implementação atende o contrato do .NET Standard na plataforma específica.

O assembly de referência do .NET Standard usa um esquema de controle de versão `MAJOR.MINOR`. O nível `PATCH` não é útil para o .NET Standard porque expõe apenas uma especificação de API (nenhuma implementação) e por definição, qualquer alteração à API representaria uma alteração no conjunto de recursos e, portanto, uma nova versão `MINOR`.

As implementações em cada plataforma podem ser atualizadas, normalmente como parte da versão de plataforma e isso, portanto, não é evidente para os programadores que usam o .NET Standard nessa plataforma.

Para obter mais informações, confira [.NET Standard](../../standard/net-standard.md).

## <a name="see-also"></a>Confira também

- [Estruturas de destino](../../standard/frameworks.md)
- [Empacotamento de distribuição do .NET](../distribution-packaging.md)
- [Folha de fatos do ciclo de vida de suporte do .NET](https://dotnet.microsoft.com/platform/support/policy)
- [Imagens do Docker para .NET](https://hub.docker.com/_/microsoft-dotnet/)
