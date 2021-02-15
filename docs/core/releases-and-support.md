---
title: Versões, patches e suporte do .NET
description: Saiba mais sobre versões, patches e suporte para o .NET 5 (incluindo o .NET Core) e versões posteriores.
ms.date: 10/07/2020
ms.topic: overview
ms.author: tdykstra
author: tdykstra
ms.openlocfilehash: 896b88cbf1f7f31d2d26d69ec7d219da6b27ceff
ms.sourcegitcommit: 6d1ae17e60384f3b5953ca7b45ac859ec6d4c3a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94982289"
---
# <a name="releases-and-support-for-net-core-and-net-5"></a>Versões e suporte para .NET Core e .NET 5

A Microsoft fornece versões principais, versões secundárias e atualizações de serviços (patches) para .NET 5,0 (e .NET Core) e versões posteriores. Este artigo explica os tipos de versão, as atualizações de serviço, as faixas de recursos do SDK, os períodos de suporte e as opções de suporte.

## <a name="release-types"></a>Tipos de versão

As informações sobre o tipo de cada versão são codificadas no número de versão no formato *Major. Minor. patch*.

Por exemplo:

* O .NET Core 3,0 e o NET 5,0 são versões principais.
* O .NET Core 3,1 é a primeira versão secundária após a versão principal do .NET Core 3,0.
* O .NET Core 3.1.7 é o sétimo patch para o .NET Core 3,1.

### <a name="major-releases"></a>Versões principais

As versões principais incluem novos recursos, nova área de superfície de API pública e correções de bugs. Os exemplos incluem o .NET Core 3,0 e o .NET 5,0.  Devido à natureza das alterações, espera-se que essas versões tenham alterações interruptivas. As versões principais são instaladas lado a lado com as versões principais anteriores.

### <a name="minor-releases"></a>Versões secundárias

As versões secundárias também incluem novos recursos, área de superfície de API pública e correções de bugs, além de também poderem ter alterações interruptivas. Os exemplos incluem o .NET Core 2,1 e o .NET Core 3,1. A diferença entre essas versões e as principais é que a magnitude das alterações é menor. Um aplicativo que atualiza do .NET Core 3,0 para 3,1 tem um salto menor para avançar. Versões secundárias são instaladas lado a lado com versões secundárias anteriores.

### <a name="servicing-updates"></a>Atualizações de serviço

As atualizações de serviço (patches) são entregues quase todos os meses, e essas atualizações contêm correções de bugs de segurança e não segurança. Por exemplo, o .NET Core 3.1.8 é a oitava atualização para o .NET Core 3,1. Quando essas atualizações incluem correções de segurança, elas são lançadas em "Patch Tuesday", que é sempre a segunda terça-feira do mês. Espera-se que as atualizações de serviço mantenham a compatibilidade. A partir do .NET Core 3,1, as atualizações de serviço são atualizações que removem a atualização anterior. Por exemplo, a atualização de serviço mais recente para 3,1 remove a atualização anterior 3,1 após a instalação bem-sucedida.

### <a name="feature-bands-sdk-only"></a>Faixas de recursos (somente SDK)

O controle de versão do SDK do .NET funciona um pouco diferente do tempo de execução do .NET. Para se alinhar com as novas versões do Visual Studio, as atualizações do SDK do .NET às vezes incluem novos recursos ou novas versões de componentes, como MSBuild e NuGet. Esses novos recursos ou componentes podem ser incompatíveis com as versões fornecidas nas atualizações do SDK anteriores para a mesma versão principal ou secundária.

Para diferenciar essas atualizações, o SDK do .NET usa o conceito de faixas de recursos. Por exemplo, o primeiro SDK 3,1 do .NET Core foi 3.1.100. Esta versão corresponde à  *faixa de recursos* do 3.1.1 XX. As faixas de recursos são definidas nos centenas de grupos na terceira seção do número de versão. Por exemplo, 3.1.101 e 3.1.201 são versões em duas faixas de recursos diferentes, enquanto 3.1.101 e 3.1.199 estão na mesma faixa de recursos. Quando SDK do .NET Core 3.1.101 for instalado, SDK do .NET Core 3.1.100 será removido do computador, se existir. Quando SDK do .NET Core 3.1.200 é instalado no mesmo computador, SDK do .NET Core 3.1.101 não é removido.

### <a name="runtime-roll-forward-and-compatibility"></a>Avanço e compatibilidade de tempo de execução

As atualizações principais e secundárias são instaladas lado a lado com versões anteriores. Um aplicativo criado para direcionar uma versão *principal. secundária* específica continua a usar esse tempo de execução direcionado mesmo que uma versão mais recente esteja instalada. O aplicativo não é automaticamente rolado para usar uma versão *principal* mais recente do tempo de execução, a menos que você opte por esse comportamento. Um aplicativo criado para o .NET Core 3,0 de destino não começa a ser executado automaticamente no .NET Core 3,1. É recomendável recriar o aplicativo e testá-lo em uma versão mais recente ou secundária de tempo de execução antes de implantar na produção. Para obter mais informações, consulte [roll forward de aplicativos dependentes da estrutura](versions/selection.md#framework-dependent-apps-roll-forward) e [roll forward do tempo de execução de implantação autônomo](deploying/runtime-patch-selection.md).

As atualizações de serviço são tratadas de forma diferente das versões principais e secundárias. Um aplicativo criado para direcionar o .NET Core 3,1 é executado no tempo de execução do 3.1.0 por padrão. Ele é automaticamente encaminhado para usar um tempo de execução 3.1.1 mais recente quando a atualização de serviço é instalada. Esse comportamento é o padrão porque queremos que as correções de segurança sejam usadas assim que são instaladas sem qualquer outra ação necessária. Você pode recusar esse comportamento de roll-forward padrão.

## <a name="net-core-and-net-5-version-lifecycles"></a>Ciclos de vida de versão do .NET Core e do .NET 5

O .NET Core, o .NET 5 e as versões posteriores adotam o [ciclo de vida moderno](/lifecycle/policies/modern) em vez do [ciclo de vida fixo](/lifecycle/policies/fixed) que foi usado para .NET Framework versões. Os produtos com ciclos de vida fixos fornecem um longo período fixo de suporte, por exemplo, 5 anos de suporte base e outros cinco anos de suporte estendido. O suporte base inclui correções de segurança e não segurança, enquanto o suporte estendido fornece apenas correções de segurança. Os produtos que adotam um ciclo de vida moderno têm um modelo de suporte mais semelhante ao serviço, com períodos de suporte mais curtos e versões mais frequentes.

### <a name="release-tracks"></a>Faixas de versão

Há duas faixas de suporte para as versões:

* Versões *atuais*

  Essas versões têm suporte até três meses após a próxima versão principal ou secundária ser enviada.

  Exemplo:

  * O .NET Core 3,0 foi enviado em setembro de 2019 e foi seguido pelo .NET Core 3,1 em dezembro de 2019.
  * O suporte do .NET Core 3,0 foi encerrado em 2020 de março, 3 meses após o 3,1 ser enviado.

* Versões de *suporte a longo prazo* (LTS)

  Essas versões têm suporte por um mínimo de 3 anos ou 1 ano após a próxima versão de LTS enviada se essa data for mais tarde.

  Exemplo:

  * O .NET Core 2,1 foi lançado em maio de 2018 e foi considerado uma versão LTS em agosto de 2018.
  * O .NET Core 3,1 foi a próxima versão de LTS e foi lançado em dezembro de 2019.
  * Como 2021 de agosto (3 anos) é posterior a dezembro de 2020 (um ano após a versão 3,1), o .NET Core 2,1 tem suporte até agosto de 2021.

Libera a alternativa entre LTS e Current, portanto, é possível que uma versão anterior seja suportada por mais tempo do que uma versão posterior. Por exemplo, o .NET Core 2,1 é uma versão LTS com suporte até a 2021 de agosto. A versão 3,0 foi enviada mais de um ano, mas saiu do suporte antes, em dezembro de 2019.

As atualizações de serviço são enviadas mensalmente e incluem correções de segurança e não segurança (confiabilidade, compatibilidade e estabilidade). As atualizações de serviço têm suporte até que a próxima atualização de manutenção seja liberada. Atualizações de serviço têm comportamento de roll-forward de tempo de execução. Isso significa que os aplicativos assumem o padrão de execução na atualização de serviço de tempo de execução instalada mais recente.

## <a name="how-to-choose-a-release"></a>Como escolher uma versão

Se você estiver criando um serviço e esperar continuar a atualizá-lo regularmente, uma versão atual como o .NET 5,0 pode ser a melhor opção para manter-se atualizado com os recursos mais recentes que o .NET tem a oferecer.

Se você estiver criando um aplicativo cliente que será distribuído aos consumidores, a estabilidade poderá ser mais importante do que o acesso aos recursos mais recentes. Seu aplicativo pode precisar ter suporte por um determinado período antes que o consumidor possa atualizar para a próxima versão do aplicativo. Nesse caso, uma versão LTS como o .NET Core 3,1 pode ser a opção correta.

### <a name="servicing-updates"></a>Atualizações de serviço

As atualizações de serviço .NET têm suporte até que a próxima atualização de manutenção seja liberada. A cadência da versão é mensal.

Você precisa instalar regularmente as atualizações de serviço para garantir que seus aplicativos estejam em um estado seguro e com suporte. Por exemplo, se a atualização de serviço mais recente para o .NET Core 3,1 for 3.1.8 e enviarmos 3.1.9, o 3.1.8 não será mais o mais recente. O nível de manutenção com suporte para 3,1 é então 3.1.9.

Para obter informações sobre as atualizações de serviço mais recentes para cada versão principal e secundária, consulte a [página de downloads do .net](https://dotnet.microsoft.com/download/dotnet-core).

## <a name="end-of-support"></a>Fim do suporte

Fim do suporte refere-se à data após a qual a Microsoft não fornece mais correções, atualizações ou assistência técnica para uma versão do produto. Antes dessa data, verifique se você moveu para o usando uma versão com suporte. As versões que estão sem suporte não recebem mais atualizações de segurança que protegem seus aplicativos e dados.

## <a name="supported-operating-systems"></a>Sistemas operacionais compatíveis

O .NET 5 (e o .NET Core) e versões posteriores podem ser executados em uma variedade de sistemas operacionais. Cada um desses sistemas operacionais tem um ciclo de vida definido por sua organização responsável (por exemplo, Microsoft, Red Hat ou Apple). Levamos essas agendas de ciclo de vida em conta ao adicionar e remover o suporte para versões do sistema operacional.

Quando uma versão do sistema operacional sai do suporte, deixamos de testar essa versão e fornecer suporte para essa versão. Os usuários precisam avançar para uma versão do sistema operacional com suporte para obter suporte.

Para obter mais informações, consulte a [política de ciclo de vida do sistema operacional .net](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md).

## <a name="get-support"></a>Obter suporte

Você tem uma opção entre o suporte assistido da Microsoft e o suporte da Comunidade.

### <a name="microsoft-support"></a>Suporte da Microsoft

Para obter suporte assistido, [entre em contato com um suporte da Microsoft Professional](https://support.microsoft.com/supportforbusiness/productselection/?sapid=4fd4947b-15ea-ce01-080f-97f2ca3c76e8).

Você precisa estar em um nível de manutenção com suporte (a atualização de serviço mais recente disponível) para ser elegível para suporte. Se um sistema estiver executando o 3,1 e a atualização de serviço do 3.1.8 tiver sido liberada, o 3.1.8 precisará ser instalado como uma primeira etapa.

### <a name="community-support"></a>Suporte da comunidade

Para obter suporte da Comunidade, consulte a [página da Comunidade](https://dotnet.microsoft.com/platform/community).

## <a name="see-also"></a>Confira também

Para obter mais informações, incluindo intervalos de datas com suporte para cada versão do .NET Core e para o .NET 5, consulte a [política de suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).
