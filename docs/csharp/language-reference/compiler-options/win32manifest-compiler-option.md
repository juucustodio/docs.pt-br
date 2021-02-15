---
description: -win32manifest (opções do compilador C#)
title: -win32manifest (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /win32manifest
helpviewer_keywords:
- /win32manifest compiler option [C#]
- win32manifest compiler option [C#]
- -win32manifest compiler option [C#]
ms.assetid: 9460ea1b-6c9f-44b8-8f73-301b30a01de1
ms.openlocfilehash: 1d2eefdab433f67e1cba5f709a2db8ec6b9a5dc7
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91171306"
---
# <a name="-win32manifest-c-compiler-options"></a>-win32manifest (opções do compilador C#)

Use a opção **-win32manifest** para especificar um arquivo de manifesto do aplicativo Win32 definido pelo usuário para ser inserido em um arquivo PE do projeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-win32manifest: filename  
```  
  
## <a name="arguments"></a>Argumentos  

 `filename`  
 O nome e o local do arquivo de manifesto personalizado.  
  
## <a name="remarks"></a>Comentários  

 Por padrão, o compilador do Visual C# insere um manifesto do aplicativo que especifica o nível de execução solicitado "asInvoker". Ele cria o manifesto na mesma pasta em que o executável é compilado, normalmente a pasta bin\Debug ou bin\Release quando você usa o Visual Studio. Se você quiser fornecer um manifesto personalizado, por exemplo, para especificar um nível de execução solicitado de "highestAvailable" ou "requireAdministrator", use esta opção para especificar o nome do arquivo.  
  
> [!NOTE]
> Essa opção e a opção [-win32res (opções do compilador do C#)](./win32res-compiler-option.md) são mutuamente exclusivas. Se você tentar usar ambas as opções na mesma linha de comando, você obterá um erro de build.  
  
 Um aplicativo que não tem nenhum manifesto do aplicativo que especifica um nível de execução solicitado estará sujeito à virtualização de arquivos/Registro sob o recurso Controle de Conta de Usuário no Windows. Para obter mais informações, consulte [Controle de Conta de Usuário](/windows/access-protection/user-account-control/user-account-control-overview).  
  
 Seu aplicativo estará sujeito à virtualização se alguma dessas condições for verdadeira:  
  
- Você usa a opção **-nowin32manifest** e não fornece um manifesto em uma etapa de build posterior ou como parte de um arquivo de Recurso (.res) do Windows usando a opção **-win32res**.  
  
- Você fornece um manifesto personalizado que não especifica um nível de execução solicitado.  
  
 O Visual Studio cria um arquivo .manifest padrão e o armazena nos diretórios de depuração e liberação juntamente com o arquivo executável. Você pode adicionar um manifesto personalizado criando um em qualquer editor de texto e, em seguida, adicionando o arquivo ao projeto. Como alternativa, você pode clicar com o botão direito do mouse no ícone **Projeto** no **Gerenciador de Soluções**, clicar em **Adicionar Novo Item** e clicar em **Arquivo de Manifesto do Aplicativo**. Depois de adicionar o arquivo de manifesto novo ou existente, ele aparecerá na lista suspensa **Manifesto**. Para obter mais informações, consulte [página do aplicativo, designer de projeto (C#)](/visualstudio/ide/reference/application-page-project-designer-csharp).  
  
 Você pode fornecer o manifesto do aplicativo como uma etapa de pós-build personalizada ou como parte de um arquivo de recurso Win32 usando a opção [-nowin32manifest (opções do compilador do C#)](./nowin32manifest-compiler-option.md). Use essa mesma opção se quiser que o aplicativo seja sujeito à virtualização de arquivo ou Registro no Windows Vista. Isso impedirá que o compilador crie e insira um manifesto padrão no arquivo PE.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra o manifesto padrão que o Compilador do Visual C# insere em um PE.  
  
> [!NOTE]
> O compilador insere um nome de aplicativo padrão "MyApplication" no xml. Essa é uma solução alternativa para habilitar os aplicativos para serem executados no Windows Server 2003 Service Pack 3.  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [-nowin32manifest (opções do compilador do C#)](./nowin32manifest-compiler-option.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
