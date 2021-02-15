---
description: 'Saiba mais sobre: como criar um serviço de fluxo de trabalho que consome um contrato de serviço existente'
title: 'Como: criar um serviço de fluxo de trabalho que consome um contrato de serviço existente'
ms.date: 03/30/2017
ms.assetid: 11d11b59-acc4-48bf-8e4b-e97b516aa0a9
ms.openlocfilehash: 0a31f0f4e205c72b857b59726437e896a7c68231
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631249"
---
# <a name="how-to-create-a-workflow-service-that-consumes-an-existing-service-contract"></a>Como: criar um serviço de fluxo de trabalho que consome um contrato de serviço existente

.NET Framework 4,5 oferece uma integração melhor entre os serviços Web e os fluxos de trabalho na forma de desenvolvimento de fluxo de trabalho de primeiro contrato. A ferramenta de desenvolvimento de fluxo de trabalho de primeiro contrato permite que você crie o contrato no código primeiro. A ferramenta em seguida gera automaticamente um modelo de atividade na caixa de ferramentas para as operações no contrato.  
  
> [!NOTE]
> Este tópico fornece orientação passo a passo sobre como criar um serviço de fluxo de trabalho de primeiro contrato. Para obter mais informações sobre o desenvolvimento do serviço de fluxo de trabalho do primeiro contrato, consulte [contratar primeiro o desenvolvimento do serviço de fluxo de trabalho](contract-first-workflow-service-development.md)  
  
### <a name="creating-the-workflow-project"></a>Criando o projeto de fluxo de trabalho  
  
1. No Visual Studio, selecione **Arquivo**, **Novo Projeto**. Selecione o nó **WCF** sob o nó **C#** na árvore **modelos** e selecione o modelo aplicativo de serviço de **fluxo de trabalho WCF** .  
  
2. Nomeie o novo projeto `ContractFirst` e clique em **OK**.  
  
### <a name="creating-the-service-contract"></a>Criando o contrato de serviço  
  
1. Clique com o botão direito do mouse no projeto em **Gerenciador de soluções** e selecione **Adicionar**, **novo item...**. Selecione o nó de **código** à esquerda e o modelo de **classe** à direita. Nomeie a nova classe `IBookService` e clique em **OK**.  
  
2. Na parte superior da janela de código que aparece, adicione uma instrução Using a `System.Servicemodel`.  
  
    ```csharp  
    using System.ServiceModel;  
    ```  
  
3. Altere a definição de classe de exemplo à seguinte definição da interface.  
  
    ```csharp  
    [ServiceContract]  
        public interface IBookService  
        {  
            [OperationContract]  
            void Buy(string bookName);  
  
            [OperationContract(IsOneWay=true)]  
            void Checkout();  
        }  
    ```  
  
4. Crie o projeto pressionando **Ctrl + Shift + B**.  
  
### <a name="importing-the-service-contract"></a>Importando o contrato de serviço  
  
1. Clique com o botão direito do mouse no projeto em **Gerenciador de soluções** e selecione **importar contrato de serviço**. Em **\<Current Project>** , abra todos os subnós e selecione **IBookService**. Clique em **OK**.  
  
2. Uma caixa de diálogo abrirá, alertando-o de que a operação foi concluída com êxito e que as atividades geradas serão exibidas na caixa de ferramentas depois que você compilar o projeto. Clique em **OK**.  
  
3. Crie o projeto pressionando **Ctrl + Shift + B** para que as atividades importadas apareçam na caixa de ferramentas.  
  
4. Em **Gerenciador de soluções**, abra Service1. xamlx. O serviço de fluxo de trabalho aparecerá no designer.  
  
5. Selecione a atividade **sequência** . Na janela Propriedades, clique em **...** na propriedade **ImplementedContract** . Na janela do **Editor de coleção de tipos** que aparece, clique na lista suspensa **tipo** e selecione **procurar tipos...** . Na caixa de diálogo **procurar e selecionar um tipo .net** , em **\<Current Project>** , abra todos os subnós e selecione **IBookService**. Clique em **OK**. Na caixa de diálogo **Editor de coleção de tipos** , clique em **OK**.  
  
6. Selecione e exclua as atividades **ReceiveRequest** e **SendResponse** .  
  
7. Na caixa de ferramentas, arraste uma **Buy_ReceiveAndSendReply** e uma atividade de **Checkout_Receive** para a atividade de **serviço sequencial** .
