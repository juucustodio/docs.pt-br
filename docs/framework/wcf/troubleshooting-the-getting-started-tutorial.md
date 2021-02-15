---
description: 'Saiba mais sobre: solucionar os tutoriais de introdução aos Windows Communication Foundation'
title: Solucionar problemas dos tutoriais de introdução aos Windows Communication Foundation
ms.date: 01/25/2019
ms.assetid: 69a21511-0871-4c41-9a53-93110e84d7fd
ms.openlocfilehash: c57598da80beb7b95d324359f6f9cf7cab9a4879
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703387"
---
# <a name="troubleshoot-the-get-started-with-windows-communication-foundation-tutorials"></a>Solucionar problemas dos tutoriais de introdução aos Windows Communication Foundation

Este artigo fornece soluções para os problemas e erros mais comuns que você pode enfrentar ao seguir as etapas no [tutorial: introdução aos aplicativos Windows Communication Foundation](getting-started-tutorial.md).
  
## <a name="common-problems"></a>Problemas comuns

**Não consigo encontrar os arquivos de projeto em meu disco rígido.**

 O Visual Studio salva arquivos de projeto em *C:\Users \\ &lt; User name &gt; \source\repos*.  

**Não consigo localizar o arquivo de *App.config* gerado pelo *Svcutil.exe*.**

 No Visual Studio, a janela **Adicionar item existente** exibe apenas os arquivos com as seguintes extensões por padrão:

- *. cs*
- *.resx*
- *. configurações*
- *. xsd*
- *. WSDL*

Para exibir todos os tipos de arquivo, selecione **todos os arquivos ( \* . \* )** na lista suspensa no canto inferior direito da janela **Adicionar item existente** .  
  
## <a name="common-errors"></a>Erros comuns

### <a name="compile-the-service-application"></a>Compilar o aplicativo de serviço

**Erro BC30420 ' Sub Main ' não encontrado em ' GettingStartedHost. Module1 '.**

O ponto de entrada está incorreto para o aplicativo Visual Basic. Faça a seguinte alteração:

   1. Na janela **Gerenciador de soluções** , selecione a pasta **GettingStartedHost** e, em seguida, selecione **Propriedades** no menu de atalho.
    a. Na janela **GettingStartedHost** , para **objeto de inicialização**, selecione **Service. Program** (ou o ponto de entrada para seu aplicativo específico) na lista.
    b. No menu principal, selecione **arquivo**  >  **salvar tudo**.

### <a name="run-the-service-application"></a>Executar o aplicativo de serviço

**O HTTP não pôde registrar a URL ' http: \/ /+: 8000/gettingstarted/CalculatorService '. Seu processo não tem direitos de acesso a este namespace.**

 Para obter acesso adequado, inicie o processo que hospeda o serviço do Windows Communication Foundation (WCF) com privilégios administrativos:

- Para o Visual Studio: selecione o programa Visual Studio no menu **Iniciar** e, em seguida, selecione **mais**  >  **Executar como administrador** no menu de atalho.
- Para uma janela de console: selecione **prompt de comando** no menu **Iniciar** e, em seguida, selecione **mais**  >  **Executar como administrador** no menu de atalho.
- Para o Windows Explorer: selecione o executável e, em seguida, selecione **Executar como administrador** no menu de atalho.

### <a name="compile-the-client-application"></a>Compilar o aplicativo cliente

**' CalculatorClient ', não contém uma definição para ' \<method name> ' e nenhum método de extensão ' \<method name> ' aceitando um primeiro argumento do tipo ' CalculatorClient ' foi encontrado (está faltando uma diretiva using ou uma referência de assembly?)**  

Somente os métodos que você marca com o `ServiceOperationAttribute` atributo são expostos publicamente. Se você omitir o `ServiceOperationAttribute` atributo de um método na `ICalculator` interface, receberá essa mensagem de erro durante a compilação.  

**Não foi possível encontrar o nome do tipo ou do namespace ' CalculatorClient ' (está faltando uma diretiva using ou uma referência de assembly?)**

 Você receberá esse erro se não adicionar o arquivo *generatedProxy.cs* (ou *generatedProxy. vb*) ao seu projeto de cliente quando os tiver gerado com a ferramenta de *Svcutil.exe* .  

### <a name="run-the-client-application"></a>Executar o aplicativo cliente

**Exceção sem tratamento: System. ServiceModel. EndpointNotFoundException: não foi possível conectar-se a ' http: \/ /localhost: 8000/gettingstarted/CalculatorService '. Código de erro TCP 10061: não foi possível estabelecer conexão porque a máquina de destino a recusou ativamente.**

Esse erro ocorrerá se você executar o aplicativo cliente sem primeiro iniciar o serviço. Primeiro, execute o aplicativo host para iniciar o serviço e, em seguida, execute o aplicativo cliente.

### <a name="use-the-svcutilexe-tool"></a>Usar a ferramenta de Svcutil.exe

**' SvcUtil ' não é reconhecido como comando interno ou externo, programa operável ou arquivo em lotes.**

 *Svcutil.exe* deve estar no caminho do sistema. A solução mais fácil é usar o prompt de comando do Visual Studio. No menu **Iniciar** , selecione o diretório do **Visual \<version> Studio** e, em seguida, selecione **\<version> prompt de comando do desenvolvedor para vs**. Esse prompt de comando define o caminho do sistema para os locais corretos de todas as ferramentas enviadas como parte do Visual Studio.  
  
### <a name="run-the-service-and-client-applications"></a>Executar os aplicativos de serviço e cliente

**System. ServiceModel. Security. SecurityNegotiationException: a negociação de segurança SOAP com ' http: \/ /localhost: 8000/gettingstarted/CalculatorService ' para o destino ' http: \/ /localhost: 8000/gettingstarted/CalculatorService ' falhou**  

Esse erro ocorre em um computador ingressado no domínio que não tem conectividade de rede. Conecte seu computador à rede ou desative a segurança para o serviço e o cliente.

Para desativar a segurança:

- Para o serviço, substitua o código que cria o `WSHttpBinding` com o código a seguir:  
  
    ```csharp
    // Step 3: Add a service endpoint.
    selfhost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(SecurityMode.None), "CalculatorService");  
    ```

- Para o cliente, no arquivo de configuração, atualize o **\<security>** elemento sob o **\<binding>** elemento da seguinte maneira:  
  
    ```xml
    <binding name="WSHttpBinding_ICalculator">
      <security mode="None" />
    </binding
    ```  

## <a name="see-also"></a>Consulte também  

 [Introdução aos aplicativos WCF](getting-started-tutorial.md)  
 [Início rápido da solução de problemas do WCF](wcf-troubleshooting-quickstart.md)  
 [Solucionando problemas de instalação](troubleshooting-setup-issues.md)
