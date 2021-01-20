---
title: Por que escolher aplicativos de área de trabalho modernos
description: Saiba mais sobre as tecnologias de desktop, como Windows Forms, WPF e UWP no mundo moderno.
ms.date: 12/29/2020
ms.openlocfilehash: 8489e41c973bb472a23bca38e9374c36e4cdd366
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98615887"
---
# <a name="why-modern-desktop-applications"></a>Por que escolher aplicativos de área de trabalho modernos

## <a name="introduction"></a>Introdução

### <a name="a-story-of-one-company"></a>Uma história de uma empresa

De volta ao 2000s inicial, uma empresa multinacional começou a desenvolver uma solução de área de trabalho distribuída para trocar informações entre diferentes ramificações da empresa e executar operações otimizadas em unidades centralizadas. Eles escolheram uma estrutura totalmente nova chamada Windows Forms (também conhecida como WinForms) para o desenvolvimento de aplicativos. Ao longo dos anos, o projeto evoluiu para um aplicativo maduro, bem testado e comprovado por tempo com centenas de milhares de linhas de código. O tempo passado e o .NET Framework 2,0 não é mais a nova tecnologia quente. Os desenvolvedores que estão trabalhando neste aplicativo estão enfrentando um dilema. Eles gostariam de usar a pilha mais recente de tecnologias em seu desenvolvimento e fazer com que seus aplicativos pareçam e "sentem" modernos. Ao mesmo tempo, eles não querem jogar o excelente produto criado há mais de 15 anos e reescrever todo o aplicativo do zero.

### <a name="your-story"></a>Sua história

Você pode se deparar no mesmo barco, em que você tem aplicativos de Windows Forms ou Windows Presentation Foundation (WPF) maduros que provaram sua confiabilidade ao longo dos anos. Provavelmente você desejará continuar usando esses aplicativos por muitos anos. Ao mesmo tempo, como esses aplicativos foram escritos há algum tempo, eles podem estar faltando em recursos como aparência moderna, desempenho, integração com novos dispositivos e recursos de plataforma, e assim por diante, o que dá a eles a sensação de "Tech antigo". Há outro problema que pode lhe preocupar como desenvolvedor. Ao trabalhar nas versões mais antigas do .NET Framework e manter os aplicativos que foram gravados há algum tempo, você pode achar que não está aprendendo novas tecnologias e ausente na criação de habilidades técnicas modernas. Se essa for sua história – este livro é para você!

## <a name="desktop-applications-nowadays"></a>Aplicativos de área de trabalho de hoje

Antes do aumento da Internet, os aplicativos de área de trabalho eram a principal abordagem para a criação de sistemas de software. Os desenvolvedores podem escolher qualquer linguagem de programação, como COBOL, Fortran, VB6 ou C++. Mas onde eles desenvolveram pequenas ferramentas ou arquiteturas distribuídas complexas, foram todos os aplicativos da área de trabalho.

Em seguida, as tecnologias da Internet começaram a chocanter o mundo de desenvolvimento e ganhar mais engenheiros com vantagens como fácil implantação e processos de distribuição simplificados. O fato de uma vez que um aplicativo Web foi implantado na produção, todos os usuários receberam que as atualizações automáticas fizeram um enorme impacto na agilidade do software.

No entanto, a infraestrutura de Internet, os protocolos subjacentes e os padrões como HTTP e HTML não foram projetados para a criação de aplicativos complexos. Na verdade, o esforço de desenvolvimento principal, em seguida, era objetivando apenas um objetivo: fornecer aos aplicativos Web os mesmos recursos que os aplicativos da área de trabalho têm, como a entrada rápida de dados e o gerenciamento de estado.

Mesmo que os aplicativos Web e móveis tenham crescido em um ritmo incrível, para determinadas tarefas, os aplicativos de área de trabalho ainda mantêm o número um em termos de eficiência e desempenho. Isso explica por que há milhões de desenvolvedores que estão criando seus projetos com o WPF e WinForms, e a quantidade desses aplicativos está crescendo constantemente.

Aqui estão alguns motivos para escolher aplicativos de área de trabalho em seu desenvolvimento:

- Os aplicativos da área de trabalho têm uma melhor interação com o PC do usuário.
- O desempenho dos aplicativos da área de trabalho para cálculos complexos é muito maior do que o desempenho dos aplicativos Web.
- A execução da lógica personalizada no lado do cliente é possível, mas muito mais difícil com um aplicativo Web.
- O uso de multithreading é mais fácil e eficiente em um aplicativo de área de trabalho.
- A curva de aprendizado para criar interfaces do usuário (UIs) não é acentuada. E para WinForms, ele é intuitivo com a experiência de arrastar e soltar do Windows Forms Designer.
- É fácil começar a codificar e testar seus algoritmos sem a necessidade de configurar uma infraestrutura de servidor ou de se preocupar com problemas de conectividade, firewalls e compatibilidade de navegadores.
- A depuração é eficiente em comparação com a depuração da Web.
- O acesso a dispositivos de hardware, como câmera, Bluetooth ou leitores de cartão, é fácil.
- Como a tecnologia já existe há muito tempo, há muitos especialistas e uma base de dados de conhecimento disponível para desenvolver aplicativos de área de trabalho.

Assim, como você pode ver, o desenvolvimento para área de trabalho é ótimo por vários motivos. A tecnologia é madura e testada, o ciclo de desenvolvimento é rápido, a depuração é poderosa e de forma imprecisa, os aplicativos da área de trabalho têm menos complexidade e são mais fáceis de começar.

A Microsoft ofereceu muitas tecnologias de área de trabalho de interface do usuário ao longo dos anos do Win32 introduzidas em 1995 a Plataforma Universal do Windows (UWP) lançado em 2016.

![Tecnologias de desktop da Microsoft](./media/why-modern-applications/microsoft-desktop-technologies.png)

De acordo com uma pesquisa publicada pelo Telerik em abril de 2016, as tecnologias mais populares para a criação de aplicativos para a área de trabalho do Windows são Windows Forms, WPF e UWP.

![Pesquisa de Telerik mostrando Windows Forms, WPF e UWP como as tecnologias de desktop mais populares](./media/why-modern-applications/telerik-survey.png)

Você pode desenvolver em qualquer um deles usando C# e Visual Basic, mas vamos dar uma olhada mais detalhada.

### <a name="windows-forms"></a>Windows Forms

Lançado pela primeira vez em 2002, Windows Forms é uma estrutura gerenciada e é a tecnologia de desktop mais antiga, mais usada, criada no mecanismo da interface de dispositivo gráfico do Windows (GDI). Ele oferece uma experiência de arrastar e soltar tranqüila para o desenvolvimento de interfaces do usuário no Visual Studio.  Ao mesmo tempo, Windows Forms se baseia no designer do Visual Studio como a principal maneira de desenvolver sua interface do usuário, portanto, a criação de componentes visuais a partir do código não é trivial.

A lista a seguir resume as principais características do Windows Forms:

- Tecnologia madura com muitos exemplos de código e documentação.
- Designer eficiente e produtivo. Não é tão conveniente criar a interface do usuário "do código".
- Fácil e intuitivo aprender, graças à experiência de arrastar e soltar do designer.
- Com suporte em qualquer versão do Windows.
- Com suporte no .NET Core 3,0 e versões posteriores.

### <a name="wpf"></a>WPF

Com base na especificação da linguagem XAML, o WPF favorece uma separação clara entre a interface do usuário e o código. O XAML oferece recursos como Templating, estilo e associação, que é adequado para a criação de aplicativos grandes. Como Windows Forms, é uma estrutura gerenciada, mas o design é modular e reutilizável.

Estes são os principais recursos do WPF:

- Tecnologia desenvolvida.
- O designer está disponível, mas os desenvolvedores geralmente preferem criar o design a partir do código usando o XAML declarativo.
- A curva de aprendizado é mais acentuada que Windows Forms.
- Com suporte em qualquer versão do Windows.
- Com suporte no .NET Core 3,0 e versões posteriores.

### <a name="uwp"></a>UWP

A UWP não é apenas uma estrutura de apresentação como o WPF e o Windows Forms, mas também é uma plataforma em si. Esta plataforma tem:

- Seu próprio conjunto de API (a API de Windows Runtime).
- Um novo sistema de implantação (MSIX)
- Um modelo de ciclo de vida de aplicativo moderno (para consumo de bateria baixa).
- Um novo sistema de gerenciamento de recursos (com base em arquivos PRI).

A plataforma foi criada para dar suporte a todos os tipos de sistemas de entrada (como tinta, toque, gamepad, mouse, teclado, olhar e assim por diante) em todos os fatores forma com desempenho e baixo consumo de bateria em mente. Por esses motivos, o Shell do sistema operacional Windows 10 usa partes da plataforma UWP.

![Estrutura UWP](./media/why-modern-applications/uwp-structure.png)

A UWP contém uma estrutura de apresentação baseada em XAML, como o WPF, mas tem algumas diferenças importantes, como:

- Os aplicativos são executados em contêineres de aplicativos. Os contêineres de aplicativo controlam quais recursos um aplicativo UWP pode acessar.
- Com suporte apenas no Windows 10.
- Os aplicativos podem ser implantados por meio de Microsoft Store para facilitar a implantação.
- Projetado como parte da API de Windows Runtime.
- Contém um amplo conjunto de controles internos avançados e controles adicionais disponíveis por meio dos pacotes NuGet da biblioteca de interface do usuário da Microsoft (biblioteca WinUI) atualizados a cada poucos meses.

## <a name="a-tale-of-two-platforms"></a>Uma história de duas plataformas

Nos últimos 20 anos, embora as tecnologias de desktop da interface do usuário estivessem crescendo e seguindo o caminho de Windows Forms para UWP, o hardware também estava evoluindo de unidades de PC de peso pesada com pequenos monitores CRT para monitores de alto DPI e tablets leves e telefones com técnicas de entrada de dados diferentes, como toque e tinta. Essas alterações resultaram na criação de dois conceitos diferentes: um aplicativo de área de trabalho e um aplicativo moderno. Um aplicativo moderno é aquele que considera diferentes fatores forma de dispositivo, vários métodos de entrada e saída e aproveita os recursos modernos da área de trabalho durante a execução em um modelo de execução em área restrita. O aplicativo de área de trabalho (tradicional), por outro lado, é um aplicativo que precisa de uma interface do usuário sólida com uma alta densidade de controles que é melhor operado com um mouse e um teclado.

A tabela a seguir descreve as diferenças entre os dois conceitos:

|   | Aplicativo moderno | Aplicativo de desktop |
| --- | --- | --- |
| Segurança | A execução continha &amp; ótimos conceitos básicos. Criado desde o início para respeitar a privacidade do usuário, gerenciar a vida útil da bateria e se concentrar para manter o dispositivo seguro.  | &amp;Nível de segurança do administrador do usuário. Você tem acesso nativo ao registro e às pastas de disco rígido. |
| Implantação | A instalação e as atualizações são gerenciadas pela plataforma.   | MSI, atualizações de instaladores personalizados &amp; . Tradicionalmente, uma fonte de dores de cabeça para desenvolvedores e gerentes de ti.  |
| Distribuição | &amp;Pacotes assinados de distribuição confiável. A distribuição é realizada de uma fonte confiável e nunca da Web.  | Web, &amp; distribuição personalizada do SCCM. Nenhum controle sobre o que está instalado, afeta todo o computador.   |
| Interface do usuário | Interface do usuário moderna. Diferentes mecanismos de entrada, tinta, toque, gamepad, teclado, mouse, etc.  | Windows Forms, WPF, MFC. Projetado para o mouse e o teclado para uma interface do usuário densa e para obter a maior produtividade da área de trabalho.  |
| Dados | Dados da nuvem primeiro com insights. Fonte de verdade na nuvem. Informações para saber o que acontece com seu aplicativo e como ele está sendo executado.  | Dados locais. Normalmente, os aplicativos de área de trabalho tradicionais precisam de alguns dados locais.  |
| Design | Projetado para reutilização. Reutilização em mente entre diferentes plataformas, front-end e back-end, executando ativos em muitos lugares o mais possível.  | Projetado somente para Windows Desktop  |

Como parte do compromisso de fornecer aos desenvolvedores as melhores ferramentas para criar aplicativos, a Microsoft tem um grande esforço para trazer esses conceitos, ou podemos até mesmo dizer plataformas, mais perto para capacitar os desenvolvedores com o melhor dos dois mundos. Para fazer isso, a Microsoft realizou um esforço bidirecional entre as duas plataformas.

![Esforço bidirecional entre aplicativo moderno e aplicativos de área de trabalho](./media/why-modern-applications/bidirectional-effort.png)

1. Mova cenários de aplicativos da área de trabalho para a plataforma de aplicativo moderna. O desenvolvimento tradicional de desktops ainda é popular, pois ele atende bem a certos cenários. Faz sentido pegar esses cenários de área de trabalho comuns e colocá-los na plataforma de desktop moderna para tornar a plataforma totalmente capaz.

    ![Mova cenários de aplicativos da área de trabalho para a plataforma de aplicativo moderna](./media/why-modern-applications/desktop-to-modern.png)

1. Mova recursos de aplicativos modernos para aplicativos de área de trabalho. Para aplicativos de área de trabalho existentes que precisam de uma maneira de aproveitar os recursos modernos sem reescrever do zero, os recursos da plataforma de aplicativo moderna são enviados para o aplicativo da área de trabalho.

    ![Mover recursos de aplicativos modernos para aplicativos de área de trabalho](./media/why-modern-applications/modern-to-desktop.png)

Neste livro, nos concentraremos na segunda parte e mostraremos como você pode modernizar seus aplicativos de área de trabalho existentes.

## <a name="paths-to-modernization"></a>Caminhos para modernização

A estrutura deste guia reflete três eixos diferentes para realizar a modernização: recursos modernos, implantação e instalação.

### <a name="modern-features"></a>Recursos modernos

Digamos que você tenha um aplicativo de Windows Forms funcional que um representante de vendas de sua empresa usa para preencher um pedido de cliente. Um novo requisito é fornecido para permitir que o cliente assine o pedido usando uma caneta eletrônica. A escrita à tinta é nativa nos sistemas operacionais e nas tecnologias atuais, mas não estava disponível quando o aplicativo foi desenvolvido.

Esse caminho mostrará como você pode aproveitar os recursos modernos da área de trabalho em seu desenvolvimento de área de trabalho existente.

### <a name="deployment"></a>Implantação

Os ciclos de desenvolvimento modernos foram analisados para fornecer agilidade sobre como as novas versões dos aplicativos são implantadas em todos os usuários individuais. Como os aplicativos Windows Forms e WPF se baseiam em uma versão específica do .NET Framework que devem estar presentes no computador, eles não podem aproveitar os novos recursos de versão .NET Framework sem a intervenção das pessoas de ti com o risco de ter efeitos colaterais para outros aplicativos em execução no mesmo computador. Ele limitou o ritmo de inovação para os desenvolvedores forçá-los a se manterem em versões desatualizadas do .NET Framework.

Desde o lançamento do .NET Core 3,0, você pode aproveitar uma nova abordagem de implantação de várias versões do .NET lado a lado e especificar qual versão do .NET cada aplicativo deve ter como destino. Dessa forma, você pode usar os recursos mais recentes em um aplicativo, enquanto tem certeza de que não vai interromper outros aplicativos.

### <a name="installation"></a>Instalação

Os aplicativos de desktop sempre dependem de algum tipo de processo de instalação antes que o usuário possa começar a usá-los. Esse fato trouxe ao jogo um conjunto de tecnologias, do MSI e do ClickOnce para instaladores personalizados ou até mesmo implantação do XCOPY. Qualquer um desses métodos lida com problemas delicados porque os aplicativos precisam de uma maneira de acessar recursos compartilhados no computador. Às vezes, a instalação precisa acessar o registro para inserir ou atualizar novos valores de chave, às vezes, para atualizar DLLs compartilhadas referenciadas pelo aplicativo principal. Esse comportamento causa uma dor de cabeça contínua para os usuários, criando essa percepção de que, depois de instalar algum aplicativo, o computador nunca será o mesmo, mesmo se você desinstalá-lo posteriormente.

Neste livro, apresentaremos uma nova maneira de instalar aplicativos com MSIX que resolve o problema descrito anteriormente. Você aprenderá como é possível configurar facilmente empacotamento, instalação e atualizações para seu aplicativo.

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](whats-new-dotnet.md)
