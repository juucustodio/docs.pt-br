---
title: Expondo componentes do .NET Core ao COM
description: Este tutorial mostra como expor uma classe para COM do .NET Core. Você gera um servidor COM e um manifesto de servidor lado a lado para Registry-Free COM.
ms.date: 07/12/2019
helpviewer_keywords:
- exposing .NET Core components to COM
- interoperation with unmanaged code, exposing .NET Core components
- COM interop, exposing COM components
ms.assetid: 21271167-fe7f-46ba-a81f-a6812ea649d4
author: jkoritzinsky
ms.author: jekoritz
ms.openlocfilehash: 13c91e5cb6728c5669642d1b5f7bb461efdd44f8
ms.sourcegitcommit: 78eb25647b0c750cd80354ebd6ce83a60668e22c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2021
ms.locfileid: "99065045"
---
# <a name="exposing-net-core-components-to-com"></a>Expondo componentes do .NET Core ao COM

No .NET Core, o processo de expor seus objetos .NET ao COM foi significativamente simplificado em comparação com o .NET Framework. O processo a seguir explicará como expor uma classe ao COM. Este tutorial mostra como:

- Expor uma classe ao COM do .NET Core.
- Gerar um servidor COM como parte de criar sua biblioteca do .NET Core.
- Gerar automaticamente um manifesto de servidor lado a lado para COM Sem Registro.

## <a name="prerequisites"></a>Pré-requisitos

- Instale o [SDK do .NET Core 3,0](https://dotnet.microsoft.com/download) ou uma versão mais recente.

## <a name="create-the-library"></a>Criar a biblioteca

A primeira etapa é criar a biblioteca.

1. Crie uma nova pasta e, nessa pasta, execute o seguinte comando:

    ```dotnetcli
    dotnet new classlib
    ```

2. Abra `Class1.cs`.
3. Adicione `using System.Runtime.InteropServices;` ao topo do arquivo.
4. Crie uma interface chamada `IServer`. Por exemplo:

   ```csharp
   using System;
   using System.Runtime.InteropServices;

   [ComVisible(true)]
   [Guid(ContractGuids.ServerInterface)]
   [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
   public interface IServer
   {
       /// <summary>
       /// Compute the value of the constant Pi.
       /// </summary>
       double ComputePi();
   }
   ```

5. Adicione o atributo `[Guid("<IID>")]` à interface, com o GUID da interface COM que você está implementando. Por exemplo, `[Guid("fe103d6e-e71b-414c-80bf-982f18f6c1c7")]`. Observe que esse GUID precisa ser exclusivo, pois é o único identificador dessa interface para COM. No Visual Studio, você pode gerar um GUID acessando Ferramentas > Criar GUID para abrir a ferramenta Criar GUID.
6. Adicione o atributo `[InterfaceType]` à interface e especifique quais interfaces COM base sua interface deve implementar.
7. Crie uma classe chamada `Server` que implementa `IServer`.
8. Adicione o atributo `[Guid("<CLSID>")]` à classe, com o GUID do identificador de classe da classe COM que você está implementando. Por exemplo, `[Guid("9f35b6f5-2c05-4e7f-93aa-ee087f6e7ab6")]`. Como ocorre com o GUID da interface, esse GUID deve ser exclusivo pois é o único identificador dessa interface para COM.
9. Adicione o atributo `[ComVisible(true)]` à interface e à classe.

> [!IMPORTANT]
> Diferentemente do .NET Framework, o .NET Core exige que você especifique o CLSID de qualquer classe que você deseja que seja ativável por meio do COM.

## <a name="generate-the-com-host"></a>Gerar o host COM

1. Abra o arquivo de projeto `.csproj` e adicione `<EnableComHosting>true</EnableComHosting>` dentro de uma marca `<PropertyGroup></PropertyGroup>`.
2. Compile o projeto.

A saída resultante terá um arquivo `ProjectName.dll`, `ProjectName.deps.json`, `ProjectName.runtimeconfig.json` e `ProjectName.comhost.dll`.

## <a name="register-the-com-host-for-com"></a>Registrar o host COM para COM

Abra um prompt de comandos com privilégios elevados e execute `regsvr32 ProjectName.comhost.dll`. Isso registrará todos os seus objetos .NET expostos com o COM.

## <a name="enabling-regfree-com"></a>Habilitar o COM RegFree

1. Abra o arquivo de projeto `.csproj` e adicione `<EnableRegFreeCom>true</EnableRegFreeCom>` dentro de uma marca `<PropertyGroup></PropertyGroup>`.
2. Compile o projeto.

A saída resultante agora também terá um arquivo `ProjectName.X.manifest`. Esse arquivo é o manifesto lado a lado para uso com o COM Sem Registro.

## <a name="sample"></a>Amostra

Há um [exemplo de servidor COM](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo) totalmente funcional no repositório dotnet/de exemplos no GitHub.

## <a name="additional-notes"></a>Observações adicionais

Ao contrário do .NET Framework, não há suporte no .NET Core para gerar um TLB (Biblioteca de Tipos) COM com base em um assembly .NET Core. A orientação é gravar manualmente um arquivo IDL ou um cabeçalho C/C++ para as declarações nativas das interfaces COM.

> [!IMPORTANT]
> No .NET Framework, um assembly "qualquer CPU" pode ser consumido por clientes de 32 bits e de 64 bits. Por padrão, no .NET Core, no .NET 5 e em versões posteriores, os assemblies de "qualquer CPU" são acompanhados por um *\*.comhost.dll* de 64 bits. Por isso, eles só podem ser consumidos por clientes de 64 bits. Esse é o padrão porque é o que o SDK representa. Esse comportamento é idêntico ao modo como o recurso "autônomo" é publicado: por padrão, ele usa o que o SDK fornece. A `NETCoreSdkRuntimeIdentifier` Propriedade MSBuild determina o bit de bits de *\*.comhost.dll*. A parte gerenciada é realmente independente de bit de bits, como esperado, mas o ativo nativo que o acompanha é padronizado para o SDK de destino.

Não há suporte para [implantações independentes](../deploying/index.md#publish-self-contained) de componentes com. Somente as [implantações dependentes da estrutura](../deploying/index.md#publish-framework-dependent) de componentes com têm suporte.

Além disso, o carregamento de .NET Framework e do .NET Core no mesmo processo tem limitações de diagnóstico. A principal limitação é a depuração de componentes gerenciados, pois não é possível depurar .NET Framework e o .NET Core ao mesmo tempo. Além disso, as duas instâncias de tempo de execução não compartilham assemblies gerenciados. Isso significa que não é possível compartilhar os tipos reais do .NET entre os dois tempos de execução e, em vez disso, todas as interações devem ser restritas aos contratos de interface COM expostos.
