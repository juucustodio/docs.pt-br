---
description: 'Saiba mais sobre: como criar um serviço AJAX-Enabled WCF e um cliente ASP.NET que acessa o serviço'
title: Criar um serviço AJAX-Enabled WCF e um cliente ASP.NET no Visual Studio
ms.date: 08/17/2018
ms.assetid: 95012df8-2a66-420d-944a-8afab261013e
ms.openlocfilehash: 59b0cab9b28dd68b27529b5d880138cc283144a4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780343"
---
# <a name="how-to-create-an-ajax-enabled-wcf-service-and-an-aspnet-client-that-accesses-the-service"></a>Como criar um serviço do WCF habilitado pelo AJAX em um cliente do ASP.NET que acessa o serviço

Este tópico mostra como usar o Visual Studio para criar um serviço de Windows Communication Foundation habilitado para AJAX (WCF) e um cliente ASP.NET que acessa o serviço.

## <a name="create-an-aspnet-web-app"></a>Criar um aplicativo Web ASP .NET

1. Abra o Visual Studio.

1. No menu **arquivo** , selecione **novo**  >  **projeto**

1. Na caixa de diálogo **novo projeto** , expanda a   >  categoria da Web do **Visual C#** instalado  >   e selecione **ASP.NET aplicativo Web (.NET Framework)**.

1. Nomeie o projeto como **sanduícheservices** e clique em **OK**.

1. Na caixa de diálogo **novo aplicativo Web ASP.net** , selecione **vazio** e, em seguida, selecione **OK**.

   ![Caixa de diálogo tipo de aplicativo Web ASP.NET no Visual Studio](./media/create-an-ajax-wcf-asp-net-client/new-asp-net-web-app-type.png)

## <a name="add-a-web-form"></a>Adicionar um formulário da Web

1. Clique com o botão direito do mouse no projeto sanduícheservices em **Gerenciador de soluções** e selecione **Adicionar**  >  **novo item**.

1. Na caixa de diálogo **Adicionar novo item** , expanda a   >  categoria da Web do **Visual C#** instalado  >   e selecione o modelo de **formulário da Web** .

1. Aceite o nome padrão (**WebForm1**) e, em seguida, selecione **Adicionar**.

   O *WebForm1. aspx* é aberto na exibição de **origem** .

1. Adicione a seguinte marcação dentro das **\<body>** marcas:

   ```html
   <input type="button" value="Price of 3 sandwiches" onclick="Calculate()"/>
   <br />
   <span id="additionResult"></span>
   ```

## <a name="create-an-ajax-enabled-wcf-service"></a>Criar um serviço WCF habilitado para AJAX

1. Clique com o botão direito do mouse no projeto sanduícheservices em **Gerenciador de soluções** e selecione **Adicionar**  >  **novo item**.

1. Na caixa de diálogo **Adicionar novo item** , expanda a   >  categoria da Web do **Visual C#** instalado  >   e selecione o modelo **serviço WCF (habilitado para Ajax)** .

   ![Modelo de item do serviço WCF (habilitado para AJAX) no Visual Studio](./media/create-an-ajax-wcf-asp-net-client/add-wcf-service.png)

1. Nomeie o serviço **CostService** e, em seguida, selecione **Adicionar**.

   *CostService.svc.cs* é aberto no editor.

1. Implemente a operação no serviço. Adicione o seguinte método à classe CostService para calcular o custo de uma quantidade de pizzas:

    ```csharp
    [OperationContract]
    public double CostOfSandwiches(int quantity)
    {
        return 1.25 * quantity;
    }
    ```

## <a name="configure-the-client-to-access-the-service"></a>Configurar o cliente para acessar o serviço

1. Abra o arquivo *WebForm1. aspx* e selecione o modo de exibição **design** .

2. No menu **Exibir** , selecione **caixa de ferramentas**.

3. Expanda o nó **extensões Ajax** e arraste e solte um **ScriptManager** no formulário.

4. De volta à exibição da **fonte** , adicione o seguinte código entre as **\<ScriptManager>** marcas para especificar o caminho para o serviço WCF:

    ```xml
    <Services>
       <asp:ServiceReference Path="~/CostService.svc" />
    </Services>
    ```

5. Adicione o código para a função JavaScript `Calculate()` . Coloque o seguinte código na seção de **cabeçalho** do formulário da Web:

    ```html
    <script type="text/javascript">

        function Calculate() {
            CostService.CostOfSandwiches(3, onSuccess);
        }

        function onSuccess(result) {
            var myres = $get("additionResult");
            myres.innerHTML = result;
        }

    </script>
    ```

   Esse código chama o método de CostService para calcular o preço de três pizzas e, em seguida, exibe o resultado na extensão chamada **additionResult**.

## <a name="run-the-program"></a>Execute o programa

Verifique se o *WebForm1. aspx* tem foco e pressione o botão **Iniciar** para iniciar o cliente Web. O botão tem um triângulo verde e diz algo como **IIS Express (Microsoft Edge)**. Ou, você pode pressionar <kbd>F5</kbd>. Clique no botão **preço de 3 pizzas** para gerar a saída esperada de "3,75".

## <a name="example"></a>Exemplo

Este é o código completo no arquivo *CostService.svc.cs* :

```csharp
using System.ServiceModel;
using System.ServiceModel.Activation;

namespace SandwichServices
{
    [ServiceContract(Namespace = "")]
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]
    public class CostService
    {
        [OperationContract]
        public double CostOfSandwiches(int quantity)
        {
            return 1.25 * quantity;
        }
    }
}
```

Veja a seguir o conteúdo completo da página *WebForm1. aspx* :

```aspx-csharp
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SandwichServices.WebForm1" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <script type="text/javascript">

        function Calculate() {
            CostService.CostOfSandwiches(3, onSuccess);
        }

        function onSuccess(result) {
            var myres = $get("additionResult");
            myres.innerHTML = result;
        }

    </script>
</head>
<body>
    <form id="form1" runat="server">
        <div>
        </div>
        <asp:ScriptManager ID="ScriptManager1" runat="server">
            <Services>
                <asp:ServiceReference Path="~/CostService.svc" />
            </Services>
        </asp:ScriptManager>

        <input type="button" value="Price of 3 sandwiches" onclick="Calculate()" />
        <br />
        <span id="additionResult"></span>
    </form>
</body>
</html>
```
