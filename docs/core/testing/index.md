---
title: Teste no .NET
description: Este artigo fornece uma breve visão geral dos conceitos de teste, da terminologia e das ferramentas para teste no .NET.
author: IEvangelist
ms.author: dapine
ms.date: 10/19/2020
ms.openlocfilehash: 137a8f4e3bc9e3be529d5034c233d283cf158b31
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824851"
---
# <a name="testing-in-net"></a>Teste no .NET

Este artigo apresenta o conceito de teste e ilustra como os diferentes tipos de testes podem ser usados para validar o código. Há várias ferramentas disponíveis para testar aplicativos .NET, como a [CLI .net](#net-cli) ou [ides (ambientes de desenvolvimento integrado)](#ide).

## <a name="test-types"></a>Tipos de teste

Ter testes automatizados é uma ótima maneira de garantir que o código do aplicativo faça o que seus autores pretendem fazer. Este artigo aborda testes de unidade, testes de integração e testes de carga.

### <a name="unit-tests"></a>Testes de unidade

Um *teste de unidade* é um teste que exercita componentes ou métodos de software individuais, também conhecido como "unidade de trabalho". Os testes de unidade só devem testar o código dentro do controle do desenvolvedor. Eles não testam as preocupações de infraestrutura. As preocupações com a infraestrutura incluem a interação com bancos de dados, sistemas de arquivos e recursos de rede.

Para obter mais informações sobre como criar testes de unidade, consulte [ferramentas de teste](#testing-tools).

### <a name="integration-tests"></a>Testes de integração

Um *teste de integração* difere de um teste de unidade, pois ele exercita dois ou mais recursos de componentes de software para funcionar juntos, também conhecido como "integração". Esses testes operam em um espectro mais amplo do sistema em teste, enquanto os testes de unidade se concentram em componentes individuais. Geralmente, os testes de integração incluem questões de infraestrutura.

### <a name="load-tests"></a>Testes de carga

Um *teste de carga* visa determinar se um sistema pode ou não manipular uma carga especificada, por exemplo, o número de usuários simultâneos usando um aplicativo e a capacidade do aplicativo de lidar com as interações de uma resposta. Para obter mais informações sobre o teste de carga de aplicativos Web, consulte [ASP.NET Core teste de carga/estresse](/aspnet/core/test/load-tests).

## <a name="test-considerations"></a>Considerações de teste

Tenha em mente que há [práticas recomendadas](unit-testing-best-practices.md) para escrever testes. Por exemplo, o [TDD (desenvolvimento controlado por teste)](https://deviq.com/test-driven-development) é quando um teste de unidade é gravado antes do código que deve ser verificado. O TDD é como criar uma estrutura de tópicos para um livro antes de escrevê-lo. Ele destina-se a ajudar os desenvolvedores a escrever código mais legível, simples e eficiente.

## <a name="testing-tools"></a>Ferramentas de teste

O .net é uma plataforma de desenvolvimento em várias linguagens, e você pode escrever vários tipos de teste para [C#](../../csharp/index.yml), [F #](../../fsharp/index.yml)e [Visual Basic](../../visual-basic/index.yml). Para cada um desses idiomas, você pode escolher entre várias estruturas de teste.

### <a name="xunit"></a>xUnit

o [xUnit](https://xunit.net) é uma ferramenta de teste de unidade gratuita, com foco na Comunidade para .net. Escrito pelo inventário original do NUnit v2, o xUnit.net é a tecnologia mais recente para aplicativos .NET de teste de unidade. xUnit.net funciona com o reCodeRush, o TestDriven.NET e o [Xamarin](https://dotnet.microsoft.com/apps/xamarin). É um projeto do [.net Foundation](https://dotnetfoundation.org) e opera sob seu código de conduta.

Para obter mais informações, consulte os seguintes recursos:

- [Testes de unidade com C #](unit-testing-with-dotnet-test.md)
- [Teste de unidade com F #](unit-testing-fsharp-with-dotnet-test.md)
- [Testes de unidade com Visual Basic](unit-testing-visual-basic-with-dotnet-test.md)

### <a name="nunit"></a>NUnit

O [NUnit](https://nunit.org) é uma estrutura de teste de unidade para todas as linguagens .net. Inicialmente portado do JUnit, a versão de produção atual foi reescrita com muitos recursos novos e suporte para uma ampla variedade de plataformas .NET. É um projeto do [.net Foundation](https://dotnetfoundation.org).

Para obter mais informações, consulte os seguintes recursos:

- [Testes de unidade com C #](unit-testing-with-nunit.md)
- [Teste de unidade com F #](unit-testing-fsharp-with-nunit.md)
- [Testes de unidade com Visual Basic](unit-testing-visual-basic-with-nunit.md)

### <a name="mstest"></a>MSTest

[MSTest](https://github.com/Microsoft/testfx-docs) é a estrutura de teste da Microsoft para todas as linguagens .net. Ele é extensível e funciona com a CLI do .NET e o Visual Studio. Para obter mais informações, consulte os seguintes recursos:

- [Testes de unidade com C #](unit-testing-with-mstest.md)
- [Teste de unidade com F #](unit-testing-fsharp-with-mstest.md)
- [Testes de unidade com Visual Basic](unit-testing-visual-basic-with-mstest.md)

### <a name="net-cli"></a>CLI do .NET

Você pode executar um teste de unidade de soluções da [CLI do .net](../tools/index.md), com o comando [dotnet Test](../tools/dotnet-test.md) . A CLI do .NET expõe a maior parte da funcionalidade que os [ides (ambientes de desenvolvimento integrados)](#ide) disponibilizam por meio de interfaces do usuário. A CLI do .NET é de plataforma cruzada e está disponível para uso como parte dos pipelines de integração e de entrega contínua. A CLI do .NET é usada com processos com script para automatizar tarefas comuns.

### <a name="ide"></a>IDE

Se você estiver usando o Visual Studio, Visual Studio para Mac ou Visual Studio Code, há interfaces gráficas do usuário para testar a funcionalidade. Há mais recursos disponíveis para IDEs que a CLI, por exemplo [Live Unit Testing](/visualstudio/test/live-unit-testing). Para obter mais informações, consulte [incluindo e excluindo testes com o Visual Studio](/visualstudio/test/live-unit-testing#include-and-exclude-test-projects-and-test-methods).

## <a name="see-also"></a>Consulte também

Para obter mais informações, consulte os seguintes artigos:

- [Práticas recomendadas de teste de unidade com o .NET](unit-testing-best-practices.md)
- [Testes de integração no ASP.NET Core](/aspnet/core/test/integration-tests#test-app-prerequisites)
- [Executar testes de unidade seletivos](selective-unit-tests.md)
- [Usar cobertura de código para teste de unidade](unit-testing-code-coverage.md)
