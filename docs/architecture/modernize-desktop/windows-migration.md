---
title: Migração do Windows 10
description: Aprofunde-se nos recursos do Windows 10, como empacotamento e ilhas XAML.
ms.date: 12/29/2020
ms.openlocfilehash: 139a8f2354803dafeb0178b4dbfb57a95c4ddb34
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98615939"
---
# <a name="windows-10-migration"></a>Migração do Windows 10

Considere a seguinte situação: você tem um aplicativo de área de trabalho de trabalho que foi desenvolvido nos dias do Windows 7. Ele está usando a tecnologia do WPF disponível nesse momento e funcionando bem, mas tem uma interface do usuário desatualizada e comportamentos ao executá-lo no Windows 10. É como quando você observa um filme do fractais como a matriz e vê neo usando o dispositivo Nokia 8110. O filme funciona muito bem após 20 anos, mas se beneficiaria da modernização de um dispositivo.

Com o lançamento do Windows 10, a Microsoft introduziu muitas inovações para oferecer suporte a cenários como tablets e dispositivos de toque e para fornecer a melhor experiência para os usuários de um sistema operacional da Microsoft. Por exemplo, você pode:

- Entre com seu rosto usando o Windows Hello.
- Use uma caneta para desenhar ou escrever texto que seja automaticamente reconhecido e digital.
- Execute modelos de ia personalizados localmente criados na nuvem usando o WinML.

Todos esses recursos estão habilitados para desenvolvedores do Windows por meio de bibliotecas do Windows Runtime (WinRT). Você pode aproveitar esses recursos em seus aplicativos de área de trabalho existentes porque as bibliotecas também são expostas ao .NET Framework e ao .NET. Você pode até modernizar sua interface do usuário com o uso de ilhas XAML e melhorar os visuais e o comportamento de seus aplicativos de acordo com os horários.

Uma coisa importante a ser observada aqui é que você não precisa abandonar .NET Framework tecnologia para seguir esse caminho de modernização. Você pode permanecer lá com segurança e ter todos os benefícios do Windows 10 sem a pressão de migrar para o .NET. Portanto, você obtém tanto o poder quanto a flexibilidade para escolher o caminho de modernização.

## <a name="winrt-apis"></a>APIs do WinRT

As APIs do WinRT são interfaces de programação de aplicativo (APIs) orientadas a objeto e bem estruturadas que oferecem aos desenvolvedores do Windows 10 acesso a tudo o que o sistema operacional tem a oferecer. Por meio de APIs do WinRT, você pode integrar funcionalidades como notificações por push, APIs de dispositivo, Microsoft Ink e WinML, entre outras em seus aplicativos de área de trabalho.

Em geral, as APIs do WinRT podem ser chamadas de um aplicativo de área de trabalho clássico. No entanto, duas áreas principais apresentam uma exceção a essa regra:

* APIs que exigem uma identidade de pacote.
* APIs que exigem visualização como XAML ou composição.

### <a name="universal-windows-platform-uwp-packages"></a>Pacotes Plataforma Universal do Windows (UWP)

#### <a name="application-package-identity"></a>Identidade do pacote de aplicativos

Os aplicativos UWP têm um sistema de implantação em que o sistema operacional gerencia a instalação e a desinstalação do aplicativo. Isso requer que a instalação seja declarativa, o que significa que nenhum código de usuário é executado durante a instalação. Em vez disso, tudo o que o aplicativo deseja integrar ao sistema, como protocolos, tipos de arquivo e extensões, é declarado no manifesto do aplicativo. No momento da implantação, o pipeline de implantação configura esses pontos de integração. A única maneira de o sistema operacional gerenciar toda essa funcionalidade e controlar isso é que cada ' pacote ' tem uma identidade, um identificador exclusivo para o aplicativo.

Algumas APIs do WinRT exigem que essa identidade do pacote funcione conforme o esperado. No entanto, os aplicativos de área de trabalho clássicas, como aplicativos nativos C++ ou .NET, usam diferentes sistemas de implantação que não exigem uma identidade de pacote. Se você quiser usar essas APIs do WinRT em seu aplicativo de área de trabalho, será necessário fornecer uma identidade de pacote.

Uma maneira de proceder é criar um projeto de empacotamento adicional. Dentro do projeto de empacotamento, você aponta para o projeto de código-fonte original e especifica as informações de identidade que deseja fornecer. Se você instalar o pacote e executar o aplicativo instalado, ele receberá automaticamente uma identificação, permitindo que seu código chame todas as APIs do WinRT que exigem identidade.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10">
    <Identity Name="YOUR-APP-GUID "
              Publisher="CN=YOUR COMPANY"
              Version="1.x.x.x" />
</Package>
```

Você pode verificar quais APIs precisam de uma identidade de aplicativo empacotado inspecionando se o tipo que contém a API está marcado com o atributo [DualApiPartition](xref:Windows.Foundation.Metadata.DualApiPartitionAttribute) . Se for, você poderá chamar If de um aplicativo de área de trabalho tradicional não empacotado. Caso contrário, você deve converter seu aplicativo de área de trabalho clássico em um UWP com a ajuda de um projeto de empacotamento.

<https://docs.microsoft.com/windows/desktop/apiindex/uwp-apis-callable-from-a-classic-desktop-app>

#### <a name="benefits-of-packaging"></a>Benefícios do empacotamento

Além de fornecer acesso a essas APIs, você obtém alguns benefícios adicionais ao criar um pacote de aplicativos do Windows para seu aplicativo de área de trabalho, incluindo:

* **Implantação simplificada**. Os aplicativos têm uma ótima experiência de implantação, garantindo que os usuários possam instalar e atualizar um aplicativo com segurança. Se um usuário optar por desinstalar o aplicativo, ele será removido completamente sem nenhum rastreamento para evitar o problema de corrompidos do Windows.

* **Atualizações automáticas e licenciamento**. Seu aplicativo pode participar do licenciamento interno do Microsoft Store e dos recursos de atualização automática. A atualização automática é um mecanismo altamente confiável e eficiente, pois somente as partes alteradas dos arquivos são baixadas.

* **Maior alcance e monetização simplificada**. Talvez não seja seu caso, mas se você optar por distribuir seu aplicativo por meio do Microsoft Store você alcançar milhões de usuários do Windows 10.

* **Adicione recursos UWP**. Você pode adicionar recursos UWP ao pacote do seu aplicativo em seu próprio ritmo.

#### <a name="prepare-for-packaging"></a>Preparar para empacotamento

Antes de continuar a empacotar seu aplicativo de área de trabalho, há alguns pontos que você precisa abordar antes de iniciar o processo. Seu aplicativo deve respeitar qualquer uma das regras e políticas de Microsoft Store e executar no modelo de aplicativo UWP. Por exemplo, ele precisa ser executado no .NET Framework 4.6.2 ou posterior e grava no `HKEY_CURRENT_USER` hive do registro e as pastas AppData serão virtualizadas para um local de aplicativo específico do usuário.

A meta de design para empacotamento é separar o estado do aplicativo do estado do sistema enquanto mantém a compatibilidade com outros aplicativos. O Windows 10 realiza esse objetivo colocando o aplicativo dentro de um pacote UWP. Ele detecta e redireciona algumas alterações no sistema de arquivos e no registro em tempo de execução para atender à promessa de um comportamento de instalação e desinstalação confiável e limpo de um aplicativo fornecido pelo empacotamento.

Os pacotes que você cria para seu aplicativo de área de trabalho são aplicativos somente de área de trabalho, confiança total que não estão na área restrita, embora haja uma virtualização leve aplicada ao aplicativo para gravações em `HKCU` e `AppData` . Essa virtualização permite que eles interajam com outros aplicativos da mesma forma que os aplicativos de área de trabalho clássicos.

##### <a name="installation"></a>Instalação

Os pacotes de aplicativos são instalados em *% ProgramFiles% \\ WindowsApps \\ package_name*, com o executável intitulado `app_name.exe` . Cada pasta de pacote contém um manifesto (chamado `AppxManifest.xml` ) que contém um namespace XML especial para aplicativos empacotados. Dentro desse arquivo de manifesto está um elemento `<EntryPoint>`, que faz referência ao aplicativo de confiança total. Quando esse aplicativo é iniciado, ele não é executado dentro de um contêiner de aplicativo, mas, em vez disso, ele é executado como o usuário normalmente.

Depois da implantação, os arquivos do pacote serão marcados como somente leitura e totalmente bloqueados pelo sistema operacional. O Windows evitará a inicialização dos aplicativos se esses arquivos forem adulterados.

##### <a name="file-system"></a>Sistema de arquivos

O sistema operacional dá suporte a diferentes níveis de operações de sistema de arquivos para aplicativos de área de trabalho empacotados, dependendo do local da pasta.

Ao tentar acessar a pasta *AppData* do usuário, o sistema cria uma localização privada por usuário por aplicativo nos bastidores. Isso cria a ilusão de que o aplicativo empacotado está editando o verdadeiro *AppData* quando está realmente modificando uma cópia privada. Redirecionando gravações dessa maneira, o sistema pode acompanhar todas as modificações de arquivo feitas pelo aplicativo. Em seguida, ele pode limpar todos esses arquivos ao desinstalar o sistema "corrompidos" e fornecer uma melhor experiência de remoção do aplicativo para o usuário.

##### <a name="registry"></a>Registro

Os pacotes de aplicativos contêm um arquivo Registry. dat, que serve como o equivalente lógico de `HKLM\Software` no registro real. Em tempo de execução, esse Registro virtual mescla o conteúdo desse hive ao hive do sistema nativo para oferecer uma visão singular de ambos.

Todas as gravações são mantidas durante a atualização do pacote e são excluídas somente quando o aplicativo é desinstalado.

##### <a name="uninstallation"></a>Desinstalação

Quando o usuário desinstala um pacote, todos os arquivos e pastas localizados em `C:\Program Files\WindowsApps\package_name` são removidos, bem como quaisquer gravações redirecionadas para AppData ou o registro que foram capturados durante o processo.

Para obter detalhes sobre como um aplicativo empacotado trata da instalação, do acesso ao arquivo, do registro e da desinstalação, consulte <https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-behind-the-scenes> .

Você pode obter uma lista completa de itens a serem verificados <https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-prepare> .

## <a name="how-to-add-winrt-apis-to-your-desktop-project"></a>Como adicionar APIs do WinRT ao seu projeto de desktop

Nesta seção, você pode encontrar uma explicação sobre como integrar notificações do sistema em um aplicativo existente do WPF. Embora seja simples da perspectiva do código, ele ajuda a ilustrar todo o processo. As notificações são uma das muitas APIs do WinRT disponíveis que você pode usar no aplicativo .NET. Nesse caso, a API requer uma identidade de pacote. Esse processo será mais simples se as APIs não exigirem a identidade do pacote.

Vamos pegar um aplicativo de exemplo existente do WPF que lê arquivos e mostra seu conteúdo na tela. O objetivo é exibir uma notificação do sistema quando o aplicativo for iniciado.

![Captura de tela do aplicativo de exemplo em execução](./media/windows-migration/sample-application.png)

Primeiro, você deve verificar o link a seguir se a API do Windows 10 que você usará requer uma identidade de pacote:

<https://docs.microsoft.com/windows/apps/desktop/modernize/desktop-to-uwp-supported-api>

Nosso exemplo usará a <xref:Windows.UI.Notifications.Notification?displayProperty=nameWithType> API que requer uma identidade empacotada:

![Classe de notificação na documentação da Microsoft](./media/windows-migration/notification-class-documentation.png)

Para acessar a API do WinRT, adicione uma referência ao `Microsoft.Windows.SDK.Contracts` pacote NuGet e esse pacote fará a mágica nos bastidores (consulte os detalhes em <https://blogs.windows.com/windowsdeveloper/2019/04/30/calling-windows-10-apis-from-a-desktop-application-just-got-easier/> ).

Agora você está preparado para começar a adicionar algum código.

Crie um `ShowToastNotification` método que será chamado na inicialização do aplicativo. Ele simplesmente cria uma notificação do sistema a partir de um padrão XML:

```csharp
private void ShowNotification(string title, string content, string image)
{
    string xmlString = $@"<toast><visual><binding template = 'ToastGeneric'><text>{title}</text><text>{content}</text><image src=>'{image}'</image></binding></visual></toast>";
    XmlDocument toastXml = new XmlDocument();
    toastXml.LoadXml(xmlString);
    ToastNotification toast = new ToastNotification(toastXml);
    ToastNotificationManager.CreateToastNotifier().Show(toast);
}
```

Embora o projeto seja compilado, há erros porque a API de notificações requer uma identidade de pacote e você não a forneceu. Adicionar um projeto de empacotamento do Windows à solução corrigirá o problema:

![Captura de tela da caixa de diálogo Adicionar novo projeto no Visual Studio](./media/windows-migration/add-packaging-project.png)

Selecione a versão mínima do Windows à qual você deseja dar suporte e a versão que você está direcionando. Nem todas as APIs do WinRT têm suporte em todas as versões do Windows 10. Cada atualização do Windows 10 adiciona novas APIs que só estão disponíveis nesta versão; o suporte de nível inferior não está disponível.

![Selecionando a versão mínima do Windows](./media/windows-migration/select-versions.png)

A próxima etapa é adicionar o aplicativo WPF ao projeto de empacotamento do Windows adicionando uma referência de projeto:

![Adicionando o aplicativo WPF ao projeto de empacotamento do Windows](./media/windows-migration/add-application.png)

![Gerenciador de referências](./media/windows-migration/reference-manager.png)

Um projeto de empacotamento do Windows pode empacotar vários aplicativos para que você defina qual deles é o ponto de entrada:

![Definindo ponto de entrada](./media/windows-migration/set-entry-point.png)

A próxima etapa é definir o projeto do WPF como o projeto de inicialização na configuração da solução. Você pode pressionar F5 para compilar e compilar e ver os resultados.

![Aplicativo de exemplo em execução e mostrando os resultados](./media/windows-migration/sample-app-result.png)

Vamos gerar o pacote para que você possa instalar seu aplicativo. Clique com o botão direito do mouse em **armazenar**  >  **criar pacotes de aplicativos**.

![Caixa de diálogo criar pacotes de aplicativos](./media/windows-migration/create-app-packages.png)

Selecione a opção de Sideload para implantar o aplicativo do seu computador:

![Selecionando opção de Sideload](./media/windows-migration/select-sideloading-option.png)

Selecione a arquitetura do aplicativo do seu aplicativo:

![Selecionando a arquitetura do aplicativo](./media/windows-migration/select-app-architecture.png)

Por fim, crie o pacote clicando em **criar**.

## <a name="xaml-islands"></a>Ilhas XAML

As ilhas XAML são um conjunto de componentes que permitem que os desenvolvedores da área de trabalho do Windows usem controles XAML do UWP em seus aplicativos Win32 existentes, incluindo Windows Forms e WPF.

![Estrutura de ilhas XAML](./media/windows-migration/xaml-islands.png)

Você pode fazer a imagem de seu aplicativo Win32 com seus controles padrão e entre eles uma "ilha" da interface do usuário da UWP que contém controles do mundo moderno. O conceito é semelhante a ter um iFrame dentro de uma página da Web que mostra o conteúdo de um `different page.`

Além de adicionar funcionalidade das APIs do Windows 10, você pode adicionar partes do UWP XAML dentro do seu aplicativo usando as ilhas XAML.

A atualização do Windows 10 1903 apresenta um conjunto de APIs que permite hospedar conteúdo do UWP XAML no Windows Win32. Somente os aplicativos em execução no Windows 10 1903 podem usar as ilhas XAML.

### <a name="the-road-to-xaml-islands"></a>O caminho para as ilhas XAML

A estrada para as ilhas XAML começou em 2012 quando a Microsoft introduziu as APIs do WinRT como uma estrutura para modernizar os aplicativos Win32 (Windows Forms, WPF e aplicativos Win32 nativos). No entanto, os novos controles de interface do usuário dentro do WinRT estavam disponíveis para novos aplicativos, mas não para aqueles existentes.

Em 2015, junto com o Windows 10, o UWP nasceu. A UWP permite que você crie aplicativos que funcionam em dispositivos Windows, como XBox, Mobile e desktop. Um ano depois, a Microsoft anunciou a ponte de área de trabalho (anteriormente conhecida como projeto Centennial). A ponte de desktop é um conjunto de ferramentas que permitiam aos desenvolvedores trazer seus aplicativos Win32 existentes para o Microsoft Store. Mais recursos foram adicionados em 2017, permitindo que os desenvolvedores aprimorem seus aplicativos Win32 aproveitando algumas das novas APIs do Windows 10, como blocos dinâmicos e notificações na central de ações. Mas, ainda, não há novos controles de interface do usuário.

Na Build 2018, a Microsoft anunciou uma maneira para os desenvolvedores usarem os novos controles XAML do Windows 10 em seus aplicativos Win32 atuais, sem migrar totalmente seus aplicativos para a UWP. Ele foi marcado como ilhas UWP XAML.

### <a name="how-it-works"></a>Como ele funciona

A atualização do Windows 10 1903 apresenta várias APIs de hospedagem XAML. Duas delas são `WindowsXamlManager` e `DesktopWindowXamlSource` .

A `WindowsXamlManager` classe manipula a estrutura de XAML do UWP. Seu `InitializeForCurrentThread` método carrega a estrutura de XAML do UWP dentro do thread atual do aplicativo Win32.

O `DesktopWindowXamlSource` é a instância do conteúdo da sua ilha XAML. Ele tem a `Content` propriedade, que você é responsável por instanciar e definir. O `DesktopWindowXamlSource` renderiza e obtém sua entrada de um HWND. Ele precisa saber qual outro HWND ele anexará a ilha XAML, e você será responsável por dimensionar e posicionar o HWND do pai.

Os desenvolvedores do WPF ou Windows Forms normalmente não lidam com o HWND dentro de seu código, portanto, pode ser difícil entender e manipular ponteiros de HWND e as coisas de fiação subjacentes para comunicar os mundos do Win32 e do UWP.

#### <a name="the-xaml-islands-net-wrappers"></a>Os wrappers .NET das Ilhas XAML

O kit de ferramentas da Comunidade do Windows tem um conjunto de wrappers .NET das Ilhas XAML para WPF ou Windows Forms que facilitam o uso de ilhas XAML. Esses wrappers gerenciam os HWNDs, o gerenciamento de foco, entre outras coisas. Os desenvolvedores de Windows Forms e WPF devem usar esses wrappers.

O kit de ferramentas da Comunidade do Windows oferece dois tipos de controles: controles encapsulados e controles de hospedagem.

##### <a name="wrapped-controls"></a>Controles encapsulados

Esses controles encapsulados encapsulam alguns controles UWP em controles Windows Forms ou WPF, ocultando os conceitos de UWP para esses desenvolvedores. Esses controles são:

* WebView e WebViewCompatible
* InkCanvas e InkToolbar
* MediaPlayerElement
* MapControl

Adicione o `Microsoft.Toolkit.Wpf.UI.Controls` pacote ao seu projeto, inclua a referência ao namespace e comece a usá-lo.

```xml
<Window
        ...
        xmlns:uwpControls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls">
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="\*"/>
    </Grid.RowDefinitions>
    <uwpControls:InkToolbar TargetInkCanvas="{x:Reference Name=inkCanvas}"/>
    <uwpControls:InkCanvas Grid.Row="1" x:Name="inkCanvas" />
</Grid>
```

##### <a name="hosting-controls"></a>Controles de hospedagem

O poder das Ilhas XAML estende-se para a maioria dos controles de terceiros, controles de terceiros e controles personalizados desenvolvidos para UWP, que podem ser integrados ao Windows Forms e ao WPF como "ilhas" com interface do usuário totalmente funcional. O `WindowsXamlHost` controle para WPF e Windows Forms permite fazer isso.

Por exemplo, para usar o `WindowsXamlHost` controle no WPF, adicione uma referência ao `Microsoft.Toolkit.Wpf.UI.XamlHost` pacote fornecido pelo kit de ferramentas da Comunidade do Windows.

Depois de colocar seu `WindowsXamlHost` em seu código de interface do usuário, especifique qual tipo UWP você deseja carregar. Você pode optar por usar um controle encapsulado como um `Button` ou um mais complexo composto por vários controles diferentes, que são um controle UWP personalizado.

O exemplo a seguir mostra como adicionar um UWP `Button` :

```xml
<Window
        ...
        xmlns:xamlhost="clr-namespace:Microsoft.Toolkit.Wpf.UI.XamlHost;assembly=Microsoft.Toolkit.Wpf.UI.XamlHost">

<xamlhost:WindowsXamlHost x:Name="myUwpButton"
                          InitialTypeName="Windows.UI.Xaml.Controls.Button" />
```

Há uma recomendação clara sobre como abordar isso e é melhor ter uma ilha XAML única e maior contendo um controle composto personalizado do que ter várias ilhas com um controle em cada.

Um dos principais recursos do XAML é a associação e funciona entre o código Win32 e a ilha. Portanto, você pode ligar, por exemplo, um Win32 `Textbox` com um UWP `Textbox` . Uma coisa importante a ser considerada é que essas associações são associações unidirecionais, de UWP para Win32, portanto, se você atualizar o `Textbox` dentro da ilha XAML, a caixa de texto Win32 será atualizada, mas não o contrário.

Para ver instruções sobre como usar as ilhas XAML, consulte:

<https://docs.microsoft.com/windows/apps/desktop/modernize/host-standard-control-with-xaml-islands>

#### <a name="adding-uwp-xaml-custom-controls"></a>Adicionando controles personalizados UWP XAML

Um controle personalizado XAML é um controle (ou controle de usuário) criado por você ou por terceiros (incluindo os controles WinUI 2. x). Para hospedar um controle UWP personalizado em um aplicativo Windows Forms ou WPF, você precisará de:

- Para usar o `WindowsXamlHost` controle UWP em seu aplicativo .net.
- Para criar um projeto de aplicativo UWP que define um `XamlApplication` objeto.

Seu projeto do WPF ou Windows Forms deve ter acesso a uma instância da `Microsoft.Toolkit.Win32.UI.XamlHost.XamlApplication` classe fornecida pelo kit de ferramentas da Comunidade do Windows. Esse objeto atua como um provedor raiz de metadados para carregar metadados para tipos personalizados UWP XAML em assemblies no diretório atual do seu aplicativo. A maneira recomendada para fazer isso é adicionar um projeto de aplicativo em branco (universal do Windows) à mesma solução que o seu projeto do WPF ou Windows Forms e revisar a classe de aplicativo padrão neste projeto.

O controle XAML do UWP personalizado pode ser incluído neste aplicativo UWP ou em um projeto de biblioteca de classe UWP independente que você faz referência na mesma solução que o seu projeto do WPF ou Windows Forms.

Você pode verificar uma descrição detalhada do processo passo a passo em:

<https://docs.microsoft.com/windows/apps/desktop/modernize/host-custom-control-with-xaml-islands>

#### <a name="the-windows-ui-library-winui-2"></a>A biblioteca de interface do usuário do Windows (WinUI 2)

Além dos controles de caixa de entrada do Windows 10 que acompanham o sistema operacional, a mesma equipe do UWP XAML também fornece controles adicionais na biblioteca de interface do usuário do Windows (**WinUI 2**). O WinUI 2 fornece recursos e controles de interface do usuário nativos da Microsoft para aplicativos UWP do Windows e esses controles podem ser usados dentro de ilhas XAML.

WinUI 2 é código-fonte aberto e você pode encontrar informações em <https://github.com/microsoft/microsoft-ui-xaml> .

O artigo a seguir demonstra como hospedar um controle de XAML do UWP da biblioteca do WinUI 2: <https://docs.microsoft.com/windows/apps/desktop/modernize/host-custom-control-with-xaml-islands>

### <a name="do-you-need-xaml-islands"></a>Você precisa de ilhas XAML

As ilhas XAML são destinadas a aplicativos Win32 existentes que desejam melhorar a experiência do usuário aproveitando os novos controles e comportamentos do UWP sem uma regravação completa do aplicativo. Você já pode [aproveitar as APIs do Windows 10](/windows/uwp/porting/desktop-to-uwp-enhance), mas até as ilhas XAML, somente APIs não relacionadas à interface do usuário.

Se você estiver desenvolvendo um novo aplicativo do Windows, um [aplicativo UWP](/windows/uwp/get-started/universal-application-platform-guide) provavelmente será a abordagem certa.

### <a name="the-road-ahead-xaml-islands-winui-30"></a>As ilhas XAML do Road up: WinUI 3,0

Desde o Windows 8, a plataforma de interface do usuário do Windows, incluindo a estrutura de interface do usuário XAML, a camada de composição visual e o processamento de entrada, foi enviada como parte integrante do Windows. Isso significa que, para se beneficiar das melhorias mais recentes em tecnologias de interface do usuário, você deve atualizar para a versão mais recente da interface do usuário, reduzindo o ritmo da inovação ao desenvolver seus aplicativos. Para desassociar esses dois ciclos de evolução e promover a inovação, a Microsoft está trabalhando ativamente no projeto WinUI.

A partir do WinUI 2 em 2018, a Microsoft começou a enviar alguns novos controles e recursos de interface do usuário XAML como pacotes NuGet separados que se baseiam no SDK do UWP.

![Estrutura do WinUI 2,0](./media/windows-migration/winui2.png)

O WinUI 3 está em desenvolvimento ativo e expandirá muito o escopo de WinUI para incluir a plataforma de interface do usuário completa, que será totalmente dissociada do SDK do UWP:

![Estrutura do WinUI 3,0](./media/windows-migration/winui3.png)

A estrutura XAML agora será desenvolvida no GitHub e enviada fora da banda como pacotes [NuGet](/nuget/what-is-nuget) .

As APIs XAML da UWP existentes fornecidas como parte do sistema operacional não receberão mais novas atualizações de recursos. Eles ainda receberão atualizações de segurança e correções críticas, de acordo com o ciclo de vida de suporte do Windows 10.

O Plataforma Universal do Windows contém mais do que apenas a estrutura XAML (por exemplo, aplicativo e modelo de segurança, pipeline de mídia, integrações do shell do Xbox e do Windows 10, amplo suporte a dispositivos) e continuará a evoluir. Todos os novos recursos do XAML serão desenvolvidos e fornecidos como parte do WinUI em vez disso.

#### <a name="winui-3-in-desktop-app-and-winui-xaml-islands"></a>WinUI 3 no aplicativo de área de trabalho e nas ilhas XAML WinUI

Como você pode ver, WinUI 3 é a evolução do UWP XAML e funciona naturalmente dentro do modelo de aplicativo UWP e de todos os seus requisitos (ID de pacote MSIX, sandbox, CoreWindow e assim por diante. Para usar apenas WinUI 3 em um modelo de aplicativo Win32, o conteúdo do WinUI deve ser hospedado por outra estrutura de interface do usuário (Windows Forms, WPF e assim por diante) usando as **ilhas XAML do WinUI**. Este é o caminho correto se você quiser desenvolver seu aplicativo e misturar tecnologias. No entanto, se você quiser substituir toda a interface do usuário antiga para WinUI, seu aplicativo não deverá carregar estruturas de interface do usuário para apenas hospedar WinUI.

WinUI 3 abordará esses comentários críticos, adicionando **WinUI em aplicativos da área de trabalho**. Isso permitirá que os aplicativos Win32 possam usar o WinUI 3 como estrutura de interface do usuário autônoma; Não é necessário carregar Windows Forms ou o WPF.

Nessa agregação, o WinUI 3 permitirá que os desenvolvedores combinem e correspondam facilmente à combinação certa de:

* Modelo de aplicativo: UWP, Win32
* Plataforma: .NET ou nativo
* Idioma: .NET (C \# , Visual Basic), Standard C++
* Empacotamento: MSIX, AppX para o Microsoft Store, não empacotado
* Interoperabilidade: Use WinUI 3 para estender aplicativos WPF, WinForms e MFC existentes usando ilhas XAML WinUI.

Se você quiser saber mais detalhes, a Microsoft está compartilhando esse roteiro no <https://github.com/microsoft/microsoft-ui-xaml/blob/master/docs/roadmap.md> .

>[!div class="step-by-step"]
>[Anterior](migrate-modern-applications.md) 
> [Avançar](example-migration.md)
