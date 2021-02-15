---
description: 'Saiba mais sobre: como registrar e configurar um moniker de serviço'
title: 'Como: registrar e configurar um moniker de serviço'
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], configure service monikers
- COM [WCF], register service monikers
ms.assetid: e5e16c80-8a8e-4eef-af53-564933b651ef
ms.openlocfilehash: 9c6867941a5b96c6ced0f8e371e10697144bd121
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99643449"
---
# <a name="how-to-register-and-configure-a-service-moniker"></a>Como: registrar e configurar um moniker de serviço

Antes de usar o moniker do serviço Windows Communication Foundation (WCF) em um aplicativo com com um contrato tipado, você deve registrar os tipos atribuídos necessários com com e configurar o aplicativo COM e o moniker com a configuração de associação necessária.

## <a name="register-the-required-attributed-types-with-com"></a>Registrar os tipos atribuídos necessários com com

1. Use a ferramenta [Svcutil.exe (ferramenta de utilitário de metadados ServiceModel)](../servicemodel-metadata-utility-tool-svcutil-exe.md) para recuperar o contrato de metadados do serviço WCF. Isso gera o código-fonte para um assembly de cliente WCF e um arquivo de configuração de aplicativo cliente.

2. Verifique se os tipos no assembly estão marcados como `ComVisible` . Para fazer isso, adicione o seguinte atributo ao arquivo *AssemblyInfo.cs* em seu projeto do Visual Studio.

    ```csharp
    [assembly: ComVisible(true)]
    ```

3. Compile o cliente WCF gerenciado como um assembly de nome forte. Isso requer a assinatura com um par de chaves de criptografia. Para obter mais informações, consulte [Assinando um assembly com um nome forte](../../../standard/assembly/sign-strong-name.md).

4. Use a ferramenta de registro do assembly (Regasm.exe) com a `-tlb` opção de registrar os tipos no assembly com com.

5. Use a ferramenta cache de assembly global (Gacutil.exe) para adicionar o assembly ao cache de assembly global.

    > [!NOTE]
    > Assinar o assembly e adicioná-lo ao cache de assembly global são etapas opcionais, mas eles podem simplificar o processo de carregamento do assembly a partir do local correto em tempo de execução.

## <a name="configure-the-com-application-and-the-moniker-with-the-required-binding-configuration"></a>Configurar o aplicativo COM e o moniker com a configuração de associação necessária

- Coloque as definições de associação (geradas pela [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) no arquivo de configuração do aplicativo cliente gerado) no arquivo de configuração do aplicativo cliente. Por exemplo, para um executável Visual Basic 6,0 chamado CallCenterClient.exe, a configuração deve ser colocada em um arquivo chamado CallCenterConfig.exe.config no mesmo diretório que o executável. O aplicativo cliente agora pode usar o moniker. Observe que a configuração de associação não é necessária se estiver usando um dos tipos de associação padrão fornecidos pelo WCF.

     O tipo a seguir é registrado.

    ```csharp
    using System.ServiceModel;

    [ServiceContract]
    public interface IMathService
    {
        [OperationContract]
        public int Add(int x, int y);
        [OperationContract]
        public int Subtract(int x, int y);
    }
    ```

     O aplicativo é exposto usando uma `wsHttpBinding` associação. Para o tipo e a configuração de aplicativo fornecidos, as seguintes cadeias de caracteres de moniker de exemplo são usadas.

    ```
    service4:address=http://localhost/MathService, binding=wsHttpBinding, bindingConfiguration=Binding1
    ```

     ou

    ```
    service4:address=http://localhost/MathService, binding=wsHttpBinding, bindingConfiguration=Binding1, contract={36ADAD5A-A944-4d5c-9B7C-967E4F00A090}
    ```

     Você pode usar qualquer uma dessas cadeias de caracteres de moniker de dentro de um aplicativo Visual Basic 6,0, depois de adicionar uma referência ao assembly que contém os `IMathService` tipos, conforme mostrado no código de exemplo a seguir.

    ```vb
    Dim mathProxy As IMathService
    Dim result As Integer

    Set mathProxy = GetObject( _
            "service4:address=http://localhost/MathService, _
            binding=wsHttpBinding, _
            bindingConfiguration=Binding1")

    result = mathProxy.Add(3, 5)
    ```

     Neste exemplo, a definição para a configuração de associação `Binding1` é armazenada em um arquivo de configuração nomeado adequadamente para o aplicativo cliente, como *vb6appname.exe.config*.

    > [!NOTE]
    > Você pode usar um código semelhante em um C#, um C++ ou qualquer outro aplicativo de linguagem .NET.

    > [!NOTE]
    > Se o moniker estiver malformado ou se o serviço estiver indisponível, a chamada para `GetObject` retornará um erro de "sintaxe inválida". Se você receber esse erro, verifique se o moniker que você está usando está correto e se o serviço está disponível.

     Embora este tópico se concentre em usar o moniker do serviço de Visual Basic código 6,0, você pode usar um moniker de serviço de outros idiomas. Ao usar um moniker do código C++, o Svcutil.exe assembly gerado deve ser importado com "no_namespace named_guids raw_interfaces_only", conforme mostrado no código a seguir.

    ```cpp
    #import "ComTestProxy.tlb" no_namespace named_guids
    ```

     Isso modifica as definições de interface importadas para que todos os métodos retornem um `HResult` . Quaisquer outros valores de retorno são convertidos em parâmetros de saída. A execução geral dos métodos permanece a mesma. Isso permite que você determine a causa de uma exceção ao chamar um método no proxy. Essa funcionalidade só está disponível no código C++.

## <a name="see-also"></a>Consulte também

- [Ferramenta Utilitário de Metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
