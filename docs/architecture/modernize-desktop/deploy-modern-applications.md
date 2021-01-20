---
title: Implantar aplicativos modernos de área de trabalho
description: Tudo o que você precisa saber sobre a implantação de aplicativos de área de trabalho modernos.
ms.date: 05/12/2020
ms.openlocfilehash: ba47f09b27adf270734bbfff285fe44dd4175d29
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98615848"
---
# <a name="deploying-modern-desktop-applications"></a>Implantar aplicativos modernos de área de trabalho

Quando você desenvolve aplicativos de área de trabalho, uma coisa a considerar é como seu aplicativo será empacotado e implantado nos computadores dos usuários. O problema com o empacotamento, a implantação e a instalação é que ele geralmente se encontra sob a abrangência dos profissionais de ti, que se preocupam com coisas diferentes dos desenvolvedores.

Hoje em dia, todos nós estamos familiarizados com o conceito de DevOps, em que os desenvolvedores e os profissionais de ti trabalham em conjunto para mover aplicativos para seus ambientes de produção. Mas se você esteve na batalha da área de trabalho por mais de 10 anos, talvez tenha visto a história a seguir. Uma equipe de desenvolvedores trabalha com dificuldade para atender aos prazos do projeto. As pessoas de negócios são preocupadoss, pois precisam do sistema trabalhando em muitos computadores do usuário para executar a empresa. No "D-Day", o gerente de projeto verifica com todos os desenvolvedores que seu código está funcionando bem e que tudo está bem, para que eles possam ser entregues. Em seguida, a equipe de pacotes vem gerando a configuração para o aplicativo, distribuí-lo a cada computador do usuário e um conjunto de usuários de teste que executam o aplicativo. Bem, eles tentam, porque antes de mostrar qualquer interface do usuário, o aplicativo gera uma exceção que diz "o método ~ do objeto ~ falhou". A pane começa a fluir pelo ar e uma breve investigação aponta para um desenvolvedor jovem e cansado que introduziu um controle de terceiros, que certamente "funcionou na máquina de desenvolvimento".

A instalação de aplicativos de área de trabalho tradicionalmente foi um pesadelo por dois motivos principais:

- Falta de uma cultura de colaboração próxima entre o desenvolvedor e as equipes de ti.
- Falta de um pacote sólido e da tecnologia de implantação com a qual podemos se basear.

Na verdade, estamos vivendo com o fato de que, às vezes, você optou por ter instalado um aplicativo porque:

- Ele acaba tendo alguns efeitos colaterais indesejados em seu computador.
- Alguns aplicativos que foram instalados anteriormente param de funcionar.

Além disso, você não pode apenas restaurar o sistema para seu estado original desinstalando o aplicativo. Estamos acostumados a viver essa situação de que temos termos de Cunha como "DLL inferno" ou "Winrot".

Neste capítulo, falaremos sobre MSIX. A MSIX é a tecnologia totalmente nova da Microsoft que tenta capturar o melhor das tecnologias anteriores para fornecer uma base sólida para a tecnologia de empacotamento do futuro.

O que uma tecnologia de empacotamento tem a ver com modernização? Bem, acontece que o empacotamento é fundamental para a ti empresarial com muito dinheiro investido lá. A modernização não está relacionada apenas ao uso das tecnologias mais recentes. Ele também está relacionado à redução do tempo de colocação no mercado desde o momento em que um requisito de negócios é definido até que sua empresa forneça o recurso ao seu cliente.

## <a name="the-modern-application-lifecycle"></a>O ciclo de vida do aplicativo moderno

Hoje, os desenvolvedores escrevem e criam o código para um aplicativo e, em seguida, passam os ativos gerados para os profissionais de ti. Em seguida, os profissionais de ti reconfiguram o aplicativo e o reempacotam, normalmente em um MSI ou mais recentemente em um formato de empacotamento do App-V. O aplicativo é então implantado por meio de diferentes canais e ferramentas. Um dos principais problemas com essa abordagem é normalmente conhecido como "empacotamento de paralysis". O problema é que esse ciclo se repete toda vez que houver uma atualização de aplicativo ou uma atualização do sistema operacional.

Você pode ver o processo refletido na imagem a seguir:

![Diagrama mostrando o ciclo de vida de ti moderno](./media/deploy-modern-applications/modern-it-application-lifecycle.png)

As empresas precisam de uma maneira de dividir esse ciclo de empacotamento em três ciclos independentes:

- Atualizações do sistema operacional
- Atualizações de aplicativos
- Personalização

![Diagrama mostrando o ciclo de ti moderno virtuoso](./media/deploy-modern-applications/modern-it-virtuous-cycle.png)

O diagrama anterior mostra que você pode:

- Atualize o sistema operacional subjacente sem precisar reempacotar seus aplicativos.
- Habilite as personalizações a partir dela sem a necessidade de reempacotar o pacote do desenvolvedor original.

Esse radical mudar nos leva ao ciclo de vida de ti novo e moderno, conforme mostrado na figura a seguir:

![Diagrama mostrando o ciclo de vida do aplicativo usando as ferramentas da Microsoft](./media/deploy-modern-applications/microsoft-it-tools.png)

Os desenvolvedores criam o aplicativo e geram um pacote MSIX que os profissionais de ti podem consumir e configurar sem a necessidade de reempacotamento. Junto com a tecnologia MSIX, a Microsoft criou ferramentas para permitir que ela personalize e configure pacotes sem reempacotamento.

## <a name="msix-the-next-generation-of-deployment"></a>MSIX: a próxima geração de implantação

Antes do MSIX, havia várias tecnologias de empacotamento disponíveis, como assistentes de instalação, MSI, ClickOnce, App-V e scripts. Cada uma dessas tecnologias tem seus próprios pontos fortes e a Microsoft decidiu escolher o melhor de tudo para criar MSIX. O MSIX se baseia nas bases dessas tecnologias existentes que selecionam o melhor de cada:

- App-V = \> contêinerização
- ClickOnce = \> atualização automática
- MSI = \> fácil de distribuir

Com o MSIX, você obtém uma tecnologia de instalador com todos esses recursos.

![Diagrama mostrando as diferentes tecnologias que tiveram um impacto na criação de MSIX](./media/deploy-modern-applications/msix.png)

### <a name="benefits-of-msix"></a>Benefícios do MSIX

#### <a name="never-regret-installing-an-app"></a>Nunca canminha instalação de um aplicativo

O MSIX fornece uma implantação previsível, confiável e segura. O método declarativo contido no manifesto do pacote permite que o sistema operacional Mantenha o controle de todos os ativos de que seu aplicativo precisa. Ele também fornece uma verdadeira desinstalação limpa sem efeitos colaterais.

#### <a name="disk-space-optimization"></a>Otimização de espaço em disco

O MSIX é otimizado para reduzir a superfície que um aplicativo tem no espaço em disco do computador do usuário. Ele cria um único armazenamento de instância de seus arquivos. Ou seja, se você tiver dois pacotes diferentes com a mesma DLL, a DLL não será instalada duas vezes. A plataforma cuida desse problema porque ele conhece todos os arquivos que um determinado aplicativo instalou graças à sua natureza declarativa. Ele também permite que você tenha versões diferentes de uma DLL funcionando lado a lado.

Com o uso de pacotes de recursos, você pode criar facilmente aplicativos multilíngues e o sistema operacional cuida da instalação dos que são usados.

#### <a name="network-optimization"></a>Otimização de rede

O MSIX detecta as diferenças nos arquivos no nível de bloco de byte, habilitando um recurso chamado atualizações diferenciais. Isso significa que apenas os blocos de bytes atualizados são baixados nas atualizações do aplicativo.

![Um diagrama que mostra como o MSIX gerencia atualizações diferenciais](./media/deploy-modern-applications/msix-managing-updates.png)

Com a instalação de streaming, o usuário pode começar rapidamente a trabalhar em seu aplicativo enquanto outras partes do aplicativo são baixadas em segundo plano. Esse recurso contribui para uma experiência envolvente para seus usuários.

Com o recurso de pacotes opcionais, você obtém a componentização na implantação de seu aplicativo, para que possa baixá-los quando necessário.

#### <a name="simple-packaging-and-deployment"></a>Empacotamento e implantação simples

O arquivo AppManifest declara o controle de versão, direcionamento de dispositivo e identifica de forma padrão para cada aplicativo. Ele também fornece uma maneira de assinar seus ativos fornecendo uma base sólida de segurança.

#### <a name="os-managed"></a>Gerenciado pelo so

O sistema operacional manipula todos os processos de instalação, atualização e remoção de um aplicativo. Os aplicativos são instalados por usuário, mas baixados apenas uma vez, minimizando a superfície do disco. A Microsoft está trabalhando para fornecer a experiência de MSIX também no Windows 7.

#### <a name="windows-provides-integrity-for-the-app"></a>O Windows fornece integridade para o aplicativo

Com o uso de assinaturas digitais, você pode garantir que não instale um aplicativo de fontes não confiáveis. O MSIX também impede a violação porque:

- Ele mantém um registro dos hashes de arquivo.
- Ele detecta se um arquivo foi modificado após a instalação.

#### <a name="works-for-the-entire-app-catalog"></a>Funciona para todo o catálogo de aplicativos

Uma das coisas mais interessantes sobre o MSIX é que ele funciona para todo o catálogo de aplicativos, Windows Forms, WPF, MFC/ATL, Delphi, mesmo que você queira fazer a implantação do xCopy, o ClickOnce ou ir para a loja, pode usar o mesmo pacote MSIX.

### <a name="tools"></a>Ferramentas

#### <a name="windows-application-packaging-project"></a>Projeto de Empacotamento de Aplicativo do Windows

Você pode usar o projeto do **Projeto de Empacotamento de Aplicativo do Windows** no Visual Studio para gerar um pacote para o aplicativo de área de trabalho. Em seguida, você pode publicar esse pacote no Microsoft Store ou Sideload-lo em um ou mais computadores.

#### <a name="msix-packaging-tool"></a>Ferramenta de Empacotamento MSIX

A Ferramenta de Empacotamento MSIX permite que você empacote novamente os aplicativos Win32 existentes para o formato MSIX. Ele oferece uma interface do usuário interativa e uma linha de comando para conversões e oferece a você a capacidade de converter um aplicativo sem ter o código-fonte.

![Ferramenta de Empacotamento MSIX](./media/deploy-modern-applications/msix-packaging-tool.png)

#### <a name="package-support-framework"></a>PSF (estrutura de suporte do pacote)

O Package support Framework é um kit de código-fonte aberto que ajuda a aplicar correções ao seu aplicativo Win32 existente quando você não tem acesso ao código-fonte, para que ele possa ser executado em um contêiner MSIX. O Package Support Framework ajuda seu aplicativo a seguir as melhores práticas do ambiente moderno do runtime.

#### <a name="app-installer"></a>Instalador de Aplicativo

O instalador do aplicativo permite que os aplicativos do Windows 10 sejam instalados clicando duas vezes no pacote do aplicativo. Isso significa que os usuários não precisam usar o PowerShell ou outras ferramentas de desenvolvedor para implantar aplicativos do Windows 10. O Instalador de Aplicativo também pode instalar um aplicativo da Web, pacotes opcionais e conjuntos relacionados.

## <a name="how-to-create-an-msix-package-from-an-existing-win32-desktop-application"></a>Como criar um pacote MSIX de um aplicativo de área de trabalho Win32 existente

Vamos passar pelo processo para criar um pacote MSIX de um aplicativo Win32 existente. Neste exemplo, usaremos um aplicativo Windows Forms.

Para começar, adicione um novo projeto à sua solução, selecione o projeto de empacotamento de aplicativos do Windows e dê um nome a ele.

![Adicionando novo projeto de empacotamento de aplicativos do Windows](./media/deploy-modern-applications/add-packaging-project.png)

Você verá a estrutura do projeto de empacotamento e notará uma pasta especial chamada *aplicativos*. Dentro dessa pasta, você pode especificar quais aplicativos deseja incluir no pacote. Pode ser mais de um.

![A estrutura do projeto de empacotamento](./media/deploy-modern-applications/packaging-project.png)

Clique com o botão direito do mouse na pasta *aplicativos* e selecione o projeto de Windows Forms que você deseja empacotar da solução do Visual Studio.

![Adicionando o projeto de Windows Forms ao projeto de empacotamento](./media/deploy-modern-applications/add-winforms-project.png)

Neste ponto, você pode compilar e gerar o pacote, mas vamos examinar algumas coisas. Para ter uma melhor experiência do usuário, o Visual Studio pode gerar automaticamente todos os ativos visuais que um aplicativo moderno precisa para lidar com ícones e ativos de bloco para a barra de blocos e o menu iniciar. Abra o arquivo *Package. appxmanifest* para acessar o designer de manifesto. Você pode, então, gerar todos os ativos visuais de uma determinada imagem presente no projeto apenas clicando em **criar**.

![Captura de tela do designer de manifesto no Visual Studio](./media/deploy-modern-applications/manifest-designer.png)

Se você abrir o código para o arquivo *Package. appxmanifest* , poderá ver algumas coisas interessantes.

Certo `<Package>` , em, há um `<Identity>` nó. É aí que o aplicativo empacotado vai obter sua identidade, que será gerenciada pelo sistema operacional.

![Nó de identidade](./media/deploy-modern-applications/identity-node.png)

No `<Capabilities>` nó, você pode encontrar todos os requisitos de que o aplicativo precisa, pagando atenção especial para o `<rescap:Capability Name="runFullTrust" \>` , que informa ao sistema operacional para executar o aplicativo no modo de confiança total, já que ele é um aplicativo Win32.

![Nó de recursos](./media/deploy-modern-applications/capabilities-node.png)

Defina o projeto de empacotamento como o projeto de inicialização para a solução e selecione *executar*. Isso vai para:

- Compile o aplicativo Windows Forms.
- Crie um pacote MSIX fora dos resultados da compilação.
- Implante os pacotes.
- Instale-o localmente no computador de desenvolvimento.
- Iniciar o aplicativo.

![Nosso aplicativo instalado](./media/deploy-modern-applications/our-installed-application.png)

Com isso, você tem a experiência de instalação e desinstalação limpa que o MSIX fornece totalmente integrado ao Windows 10.

O estágio final é sobre como implantar o pacote MSIX em outro computador.

Clique com o botão direito do mouse no projeto de empacotamento, selecione o menu **armazenar** e selecione a opção **criar pacotes de aplicativos** .

Em seguida, você pode escolher entre criar um pacote para carregar na loja ou criar pacotes para Sideload. Na maioria dos cenários de modernização, você escolherá **que desejo criar pacotes para Sideload**.

![Configurando pacotes](./media/deploy-modern-applications/configuring-packages.png)

Lá, você pode selecionar as diferentes arquiteturas que deseja direcionar, pois você pode incluir quantos quiser no mesmo pacote MSIX.

A etapa final é declarar onde você deseja implantar os ativos de instalação finais.

![Definir configurações de atualização](./media/deploy-modern-applications/configure-update-settings.png)

Você pode optar por usar um servidor Web de um caminho UNC compartilhado em seus servidores de arquivos corporativos. Preste atenção às configurações para especificar como deseja atualizar seu aplicativo. Abordaremos as atualizações do aplicativo na próxima seção.

Para obter um guia passo a passo detalhado, consulte [empacotar um aplicativo de área de trabalho do código-fonte usando o Visual Studio](/windows/msix/desktop/desktop-to-uwp-packaging-dot-net).

## <a name="auto-updates-in-msix"></a>Atualizações automáticas no MSIX

A Windows Store tem um ótimo mecanismo de atualização usando Windows Update. Na maioria dos cenários empresariais, você não usa a loja para distribuir seus aplicativos de área de trabalho. Portanto, você precisa de uma maneira semelhante de configurar atualizações para seu aplicativo e extraí-las para seus usuários.

Usando uma combinação de recursos do Windows 10 e pacotes do MSIX, você pode fornecer uma ótima experiência de atualização para seus usuários. Na verdade, o usuário não precisa ser técnico, mas ainda se beneficiar de uma experiência de atualização de aplicativo sem problemas.

Você pode configurar suas atualizações para interagir com o usuário de duas maneiras diferentes:

- Atualizações solicitadas pelo usuário: o sistema operacional mostra alguma boa interface de usuário gerada automaticamente para notificar o usuário sobre o aplicativo que está prestes a ser instalado. Ele cria essa interface do usuário com base nas propriedades que você especificar nos arquivos de instalação.

- Atualizações silenciosas em segundo plano. Com essa opção, os usuários não precisam estar cientes das atualizações.

Você também pode configurar quando deseja realizar atualizações, quando o aplicativo é iniciado ou regularmente. Graças aos recursos de carregamento no lado, você pode até mesmo obter essas atualizações enquanto o aplicativo está em execução.

Quando você usa esse tipo de implantação, um arquivo especial é criado chamado *. AppInstaller*. Esse arquivo simples contém as seguintes seções:

- O local do arquivo *. AppInstaller*
- As propriedades principais do pacote MSIX do aplicativo
- O comportamento de atualização

![arquivo. AppInstaller](./media/deploy-modern-applications/appinstaller-file.png)

Em combinação com esse arquivo, a Microsoft projetou um protocolo de URL especial para iniciar o processo de instalação a partir de um link:

```xml
<a href="ms-appinstaller:?source=http://mywebservice.azureedge.net/MyApp.msix">Install app package </a>
```

Esse protocolo funciona em todos os navegadores e inicia o processo de instalação com uma excelente experiência do usuário no Windows 10. Como o sistema operacional gerencia o processo de instalação, ele reconhece o local do qual esse aplicativo foi instalado e rastreia todos os arquivos afetados pelo processo.

O MSIX cria uma interface do usuário para a instalação mostrando automaticamente algumas propriedades do pacote. Isso permite uma experiência de instalação comum para cada aplicativo.

Depois de gerar o novo pacote MSIX e movê-lo para o servidor de implantação, basta editar o arquivo *. AppInstaller* para refletir essas alterações, principalmente a versão e o caminho para o novo arquivo MSIX. Na próxima vez que o usuário iniciar o aplicativo, o sistema irá detectar a alteração e baixar os arquivos para a nova versão em segundo plano. Quando isso for feito, a instalação será executada na inicialização do novo aplicativo de forma transparente para o usuário.

>[!div class="step-by-step"]
>[Anterior](example-migration.md)
