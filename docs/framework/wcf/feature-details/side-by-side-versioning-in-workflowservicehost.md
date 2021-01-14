---
title: Controle de versão lado a lado no WorkflowServiceHost
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 60887eed-df40-4412-b812-41e1dd329d15
ms.openlocfilehash: 1505582e5ac7303a2df20539fdcf67435746b9d3
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190488"
---
# <a name="side-by-side-versioning-in-workflowservicehost"></a>Controle de versão lado a lado no WorkflowServiceHost

O <xref:System.ServiceModel.Activities.WorkflowServiceHost> controle de versão lado a lado introduzido no .NET Framework 4,5 fornece a capacidade de hospedar várias versões de um serviço de fluxo de trabalho em um único ponto de extremidade. A funcionalidade de lado a lado fornecida permite que um serviço de fluxo de trabalho seja configurado para que novas instâncias do serviço de fluxo de trabalho sejam criadas usando a nova definição de fluxo de trabalho, enquanto executa instâncias completas usando a definição existente. Este tópico fornece uma visão geral da execução lado a lado do serviço de fluxo de trabalho usando <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
## <a name="hosting-multiple-versions-in-a-workflow-service"></a>Hospedando várias versões em um serviço de fluxo de trabalho  

 <xref:System.ServiceModel.Activities.WorkflowServiceHost> contém duas propriedades que podem ser configuradas para permitir que várias versões de um fluxo de trabalho sejam executadas lado a lado: <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A> e <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A>. <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A> contém as versões suportadas do serviço de fluxo de trabalho, e <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> é usado para identificar exclusivamente cada serviço de fluxo de trabalho. Isso é feito por meio da associação de um <xref:System.Activities.WorkflowIdentity> com o serviço de fluxo de trabalho. Uma instância <xref:System.Activities.WorkflowIdentity> contém três informações de identificação. <xref:System.Activities.WorkflowIdentity.Name%2A> e <xref:System.Activities.WorkflowIdentity.Version%2A> contêm um nome e um <xref:System.Version> e são necessários, e <xref:System.Activities.WorkflowIdentity.Package%2A> é opcional e pode ser usado para especificar uma cadeia de caracteres adicional que contém informações como o nome do assembly ou outras informações desejadas. Cada serviço de fluxo de trabalho contido na coleção <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A> deve ter um único <xref:System.Activities.WorkflowIdentity>. Um <xref:System.Activities.WorkflowIdentity> é exclusivo se qualquer uma de suas três propriedades for diferente da outra <xref:System.Activities.WorkflowIdentity>. Um `null` <xref:System.Activities.WorkflowIdentity> é um valor permitido para <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> , mas apenas uma versão anterior de um serviço de fluxo de trabalho pode ter um `null` <xref:System.Activities.WorkflowIdentity> .  
  
> [!IMPORTANT]
> Um <xref:System.Activities.WorkflowIdentity> não deve conter informações pessoalmente identificáveis (PII). <xref:System.Activities.WorkflowIdentity> é composto por três partes : um <xref:System.Activities.WorkflowIdentity.Name%2A> (<xref:System.String>), um <xref:System.Activities.WorkflowIdentity.Version%2A> (<xref:System.Version>) e um <xref:System.Activities.WorkflowIdentity.Package%2A> (<xref:System.String>). As informações sobre o <xref:System.Activities.WorkflowIdentity> usadas para criar uma instância são emitidas para todos os serviços de rastreamento configurados em vários pontos diferentes do ciclo de vida da atividade em runtime. O Rastreamento WF não tem nenhum mecanismo para ocultar o PII (dados de usuário confidenciais). Portanto, uma instância <xref:System.Activities.WorkflowIdentity> não deve conter nenhum dado de PII porque será emitido pelo runtime em registros de rastreamento e pode estar visível para qualquer um com acesso para exibir os registros de rastreamento.  
  
### <a name="rules-for-hosting-multiple-versions-of-a-workflow-service"></a>Regras para hospedar várias versões de um serviço de fluxo de trabalho  

 Quando um usuário adiciona uma versão adicional ao <xref:System.ServiceModel.Activities.WorkflowServiceHost>, há várias condições que devem ser cumpridas para que um serviço de fluxo de trabalho seja hospedado com o mesmo conjunto de pontos de extremidade e uma descrição. Se qualquer uma das versões adicionais não atenderem a essas condições, o <xref:System.ServiceModel.Activities.WorkflowServiceHost> gera uma exceção quando `Open` é chamado. Cada definição de fluxo de trabalho fornecida para o host como uma versão adicional deve atender aos seguintes requisitos (onde a versão principal é a definição do serviço de fluxo de trabalho é fornecida para o construtor de host). A versão de fluxo de trabalho adicional deverá:  
  
- Ter o mesmo <xref:System.ServiceModel.Activities.WorkflowService.Name%2A> que a versão principal do serviço de fluxo de trabalho.  
  
- Não deve ter quaisquer atividades <xref:System.ServiceModel.Activities.Receive> ou <xref:System.ServiceModel.Activities.SendReply> no seu <xref:System.ServiceModel.Activities.WorkflowService.Body%2A> que não são da versão principal, e eles devem corresponder ao contrato de operação.  
  
- Ter um único <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A>. Somente uma definição de fluxo de trabalho pode ter um `null`<xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A>.  
  
 Algumas alterações são permitidas. Os itens a seguir podem ser diferentes entre as versões:  
  
- O <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> pode ter um nome e um pacote diferente que a versão principal.  
  
- O valor <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> pode ser diferente da versão principal.  
  
- O <xref:System.ServiceModel.Activities.WorkflowService.ConfigurationName%2A> pode ser diferente da versão principal.  
  
- O <xref:System.ServiceModel.Activities.WorkflowService.ImplementedContracts%2A> pode ser diferente da versão principal.  
  
### <a name="configuring-the-definitionidentity"></a>Configurando a DefinitionIdentity  

 Quando um serviço de fluxo de trabalho é criado usando o designer de fluxo de trabalho, o <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> é definido usando a janela **Propriedades** . Clique fora da atividade raiz do serviço no designer para selecionar o serviço de fluxo de trabalho e escolha **janela de propriedades** no menu **Exibir** . Selecione **WorkflowIdentity** na lista suspensa exibida ao lado da propriedade **DefinitionIdentity** e, em seguida, expanda e especifique as propriedades desejadas <xref:System.Activities.WorkflowIdentity> . No exemplo a seguir <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> , o é configurado com o <xref:System.Activities.WorkflowIdentity.Name%2A> `MortgageWorkflow` e um <xref:System.Activities.WorkflowIdentity.Version%2A> de `1.0.0.0` . <xref:System.Activities.WorkflowIdentity.Package%2A> é opcional e neste exemplo é `null`.  
  
 ![Captura de tela que mostra a propriedade DefinitionIdentity.](./media/side-by-side-versioning-in-workflowservicehost/definitionidentity-property.bmp)  
  
 Quando um serviço de fluxo de trabalho é auto-hospedado, o <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> é configurado quando o serviço de fluxo de trabalho é criado. No exemplo a seguir, o <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> é configurado com os mesmos valores do exemplo anterior, com o <xref:System.Activities.WorkflowIdentity.Name%2A> `MortgageWorkflow` e um <xref:System.Activities.WorkflowIdentity.Name%2A> de `1.0.0.0` .  
  
```csharp  
WorkflowService service = new WorkflowService  
{  
    Name = "MortgageWorkflowService",  
    Body = new MortgageWorkflow(),  
    DefinitionIdentity = new WorkflowIdentity  
    {  
        Name = "MortgageWorkflow",  
        Version = new Version(1, 0, 0, 0)  
    }  
};  
```  
  
```vb  
Dim service As New WorkflowService  
With service  
    .Name = "MortgageWorkflowService"  
    .Body = New MortgageWorkflow  
    .DefinitionIdentity = New WorkflowIdentity With _  
    { _  
        .Name = "MortgageWorkflow", _  
        .Version = New Version(1, 0, 0, 0) _  
    }  
End With  
```  
  
 <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A>Não é necessário, embora apenas uma versão do serviço de fluxo de trabalho possa ter um **NULL** <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> .  
  
> [!NOTE]
> Isso é útil se o serviço foi implantado inicialmente sem um <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> configurado, e uma versão atualizada é criada.  
  
### <a name="adding-a-new-version-to-a-web-hosted-workflow-service"></a>Adicionar uma nova versão a um serviço de fluxo de trabalho hospedado na web   

 A primeira etapa na configuração de uma nova versão de um serviço de fluxo de trabalho em um serviço hospedado na web é criar uma nova pasta na pasta `App_Code` com o mesmo nome do arquivo de serviço. Se arquivo `xamlx` do serviço é chamado de `MortgageWorkflow.xamlx`, a pasta deve ser nomeada como `MortgageWorkflow`. Coloque uma cópia do arquivo `xamlx` original do serviço nesta pasta e renomeie-o para um novo nome, como `MortgageWorkflowV1.xamlx`. Faça as alterações desejadas no serviço primário, atualize seu <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> e implante o serviço. No exemplo a seguir, o <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> foi atualizado com um <xref:System.Activities.WorkflowIdentity.Name%2A> de `MortgageWorkflow` e um <xref:System.Activities.WorkflowIdentity.Version%2A> de `2.0.0.0`.  
  
 ![Captura de tela que mostra DefinitionIdentity de WorkflowIdentity.](./media/side-by-side-versioning-in-workflowservicehost/definitionidentity-workflowidentity.bmp)  
  
 Quando o serviço for reiniciado, a versão anterior será automaticamente adicionada à coleção <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A>, porque ela está localizada na subpasta `App_Code` designada. Observe que, se a versão primária do serviço de fluxo de trabalho tiver `null` <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> as versões anteriores, elas não serão adicionadas. Uma versão pode ter um `null`<xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A>, mas se houver várias versões, a versão principal não deve ser aquela com o `null`<xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A>, senão as versões anteriores não serão adicionadas à coleção <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A>.  
  
### <a name="adding-a-new-version-to-a-self-hosted-workflow-service"></a>Adicionar uma nova versão a um serviço de fluxo de trabalho auto-hospedado  

 Ao adicionar uma nova versão a um serviço de fluxo de trabalho auto-hospedado, o <xref:System.ServiceModel.Activities.WorkflowServiceHost> é configurado com a versão principal do serviço de fluxo de trabalho, e as versões anteriores devem ser adicionadas explicitamente à coleção <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A>. No exemplo a seguir, um <xref:System.ServiceModel.Activities.WorkflowServiceHost> é configurado com um serviço de fluxo de trabalho principal que usa uma definição de fluxo de trabalho `MortgageWorkflowV2` e um serviço de fluxo de trabalho configurado com uma definição de fluxo de trabalho `MortgageWorkflowV1` é adicionado à coleção <xref:System.ServiceModel.Activities.WorkflowServiceHost.SupportedVersions%2A>. Cada serviço de fluxo de trabalho é configurado com um único <xref:System.ServiceModel.Activities.WorkflowService.DefinitionIdentity%2A> que reflete a versão da definição de fluxo de trabalho.  
  
```csharp  
// Create the primary version of the workflow service.  
WorkflowService serviceV2 = new WorkflowService  
{  
    Name = "MortgageWorkflowService",  
    Body = new MortgageWorkflowV2(),  
    DefinitionIdentity = new WorkflowIdentity  
    {  
        Name = "MortgageWorkflow",  
        Version = new Version(2, 0, 0, 0)  
    }  
};  
  
// Configure the WorkflowServiceHost with the current version  
// of the workflow service. This code requires Administrator  
// privileges to function correctly. If running from Visual  
// Studio, Visual Studio must be run with Administrator privileges.  
WorkflowServiceHost host = new WorkflowServiceHost(serviceV2,
    new Uri("http://localhost:8080/MortgageWorkflowService"));  
  
// Create the previous version of the workflow service.  
WorkflowService serviceV1 = new WorkflowService  
{  
    Name = "MortgageWorkflowService",  
    Body = new MortgageWorkflowV1(),  
    DefinitionIdentity = new WorkflowIdentity  
    {  
        Name = "MortgageWorkflow",  
        Version = new Version(1, 0, 0, 0)  
    }  
};  
  
// Add the previous version of the service to the SupportedVersions collection.  
host.SupportedVersions.Add(serviceV1);  
```  
  
```vb  
'Create the primary version of the workflow service  
Dim serviceV2 As New WorkflowService  
With serviceV2  
    .Name = "MortgageWorkflowService"  
    .Body = New MortgageWorkflowV2  
    .DefinitionIdentity = New WorkflowIdentity With _  
    { _  
        .Name = "MortgageWorkflow", _  
        .Version = New Version(2, 0, 0, 0) _  
    }  
End With  
  
'Configure the WorkflowServiceHost with the current version  
'of the workflow service. This code requires Administrator  
'privileges to function correctly. If running from Visual  
'Studio, Visual Studio must be run with Administrator privileges.  
  
Dim host As New WorkflowServiceHost(serviceV2, _  
    New Uri("http://localhost:8080/MortgageWorkflowService"))  
  
'Create the previous version of the workflow service.  
Dim serviceV1 As New WorkflowService  
With serviceV1  
    .Name = "MortgageWorkflowService"  
    .Body = New MortgageWorkflowV1  
    .DefinitionIdentity = New WorkflowIdentity With _  
    { _  
        .Name = "MortgageWorkflow", _  
        .Version = New Version(1, 0, 0, 0) _  
    }  
End With  
  
'Add the previous version of the service to the SupportedVersions collection.  
host.SupportedVersions.Add(serviceV1)  
```
