---
description: 'Saiba mais sobre: desenvolver para várias plataformas com .NET Framework'
title: Desenvolvendo para várias plataformas com .NET Framework
ms.date: 10/21/2020
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
ms.openlocfilehash: 6223da53a4b2bf26e793ac01f31d9d1bfeb03f9d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786473"
---
# <a name="develop-for-multiple-platforms-with-net-framework"></a>Desenvolva para várias plataformas com .NET Framework

Você pode desenvolver aplicativos para plataformas Microsoft e não Microsoft usando .NET Framework e o Visual Studio.

[!INCLUDE [net-framework-future](../../../includes/net-framework-future.md)]

## <a name="options-for-cross-platform-development"></a>Opções para o desenvolvimento de plataforma cruzada

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

Para desenvolver várias plataformas, é possível compartilhar código-fonte ou binários, além de fazer chamadas entre o código do .NET Framework e as APIs do Windows Runtime.

|Se desejar...|Use...|
|-----------------------|------------|
|Compartilhar código-fonte entre os aplicativos do Windows Phone 8.1 e do Windows 8.1|**Projetos compartilhados** (modelo de aplicativos universais no Visual Studio 2013, atualização 2).<br /><br /> -Atualmente não há suporte para Visual Basic.<br />-Você pode separar o código específico da plataforma usando # `if` Statements.<br /><br /> Para obter detalhes, confira:<br /><br /> -   [Iniciar codificação](/windows/uwp/get-started/create-uwp-apps)<br />-   [Usando o Visual Studio para criar aplicativos XAML universal](https://devblogs.microsoft.com/visualstudio/using-visual-studio-to-build-universal-xaml-apps/) (postagem de blog)<br />-   [Usando o Visual Studio para criar aplicativos convergidos XAML](https://channel9.msdn.com/Events/Build/2014/3-591) (vídeo)|
|Compartilhar binários entre aplicativos destinados a plataformas diferentes|**Projetos de biblioteca de classes portáteis** para códigos que são independentes de plataforma.<br /><br /> -Essa abordagem normalmente é usada para o código que implementa a lógica de negócios.<br />-Você pode usar Visual Basic ou C#.<br />-O suporte à API varia de acordo com a plataforma.<br />-Projetos de biblioteca de classes portáteis que visam Windows 8.1 e Windows Phone 8,1 dão suporte a APIs e XAML de Windows Runtime. Esses recursos não estão disponíveis em versões anteriores da Biblioteca de Classes Portátil.<br />-Se necessário, você pode abstrair o código específico da plataforma usando interfaces ou classes abstratas.<br /><br /> Para obter detalhes, confira:<br /><br /> -   [Biblioteca de classes portátil](portable-class-library.md)<br />-   [Como fazer as bibliotecas de classes portáteis funcionarem para você](/archive/blogs/dsplaisted/how-to-make-portable-class-libraries-work-for-you) (postagem no blog)<br />-   [Usando a biblioteca de classes portátil com MVVM](using-portable-class-library-with-model-view-view-model.md) <br />-   [Recursos do aplicativo para bibliotecas direcionadas a várias plataformas](app-resources-for-libraries-that-target-multiple-platforms.md) <br />-   [Analisador de portabilidade .net](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) (extensão do Visual Studio)|
|Compartilhar código-fonte entre aplicativos para plataformas diferentes do Windows 8.1 e do Windows Phone 8.1|**Adicionar como recurso de vínculo** .<br /><br /> -Essa abordagem é adequada para a lógica do aplicativo que é comum para aplicativos, mas não para portátil, por algum motivo. É possível usar esse recurso para o código do C# ou do Visual Basic.<br />     Por exemplo, o Windows Phone 8 e o Windows 8 compartilham as APIs do Windows Runtime, mas as Bibliotecas de Classes Portáteis não oferecem suporte ao Windows Runtime para essas plataformas. É possível usar `Add as link` para compartilhar o código do Windows Runtime entre um aplicativo do Windows Phone 8 e um aplicativo da Windows Store destinado ao Windows 8.<br /><br /> Para obter detalhes, confira:<br /><br /> -   [Compartilhar código com o link adicionar como](/previous-versions/windows/apps/jj714082(v=vs.105))<br />-   [Como: adicionar itens existentes a um projeto](/previous-versions/visualstudio/visual-studio-2010/9f4t9t92(v=vs.100))|
|Gravar aplicativos da Windows Store usando o .NET Framework ou chamar APIs do Windows Runtime do código do .NET Framework|**Windows Runtime APIs** do seu código .NET Framework C# ou Visual Basic e use o .NET Framework para criar aplicativos da Windows Store. Você deve saber as diferenças de API entre as duas plataformas. Porém, existem classes que ajudam a trabalhar com essas diferenças.<br /><br /> Para obter detalhes, confira:<br /><br /> -   [Suporte .NET Framework para aplicativos da Windows Store e Windows Runtime](support-for-windows-store-apps-and-windows-runtime.md) <br />-   [Passando um URI para a Windows Runtime](passing-a-uri-to-the-windows-runtime.md) <br />-   <xref:System.IO.WindowsRuntimeStreamExtensions><br />-    <xref:System.WindowsRuntimeSystemExtensions>|
|Compilar aplicativos do .NET Framework para plataformas que não sejam da Microsoft|Os **assemblies de referência da biblioteca de classes portátil** no .NET Framework e uma extensão do Visual Studio ou uma ferramenta de terceiros, como o Xamarin.<br /><br /> Para obter detalhes, confira:<br /><br /> -   [Biblioteca de classes portátil agora disponível em todas as plataformas.](https://devblogs.microsoft.com/dotnet/portable-class-library-pcl-now-available-on-all-platforms/) (publicação de blog)<br />-   [Documentação do Xamarin](/xamarin)|
|Usar JavaScript e HTML para desenvolvimento de plataforma cruzada|**Modelos de aplicativos universais** no Visual Studio 2013, atualização 2 para desenvolver em Windows Runtime APIs para Windows 8.1 e Windows Phone 8,1. No momento, você não pode usar JavaScript e HTML com APIs .NET Framework para desenvolver aplicativos de plataforma cruzada.<br /><br /> Para obter detalhes, confira:<br /><br /> -   [Modelos de projeto JavaScript](/previous-versions/windows/apps/hh758331(v=win.10))<br />-   [Portando um aplicativo Windows Runtime usando JavaScript para Windows Phone](/previous-versions/windows/apps/dn636144(v=win.10))|
