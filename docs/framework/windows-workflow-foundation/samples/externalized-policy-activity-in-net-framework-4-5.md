---
description: 'Saiba mais sobre: atividade de política externa no .NET Framework 4,5'
title: Atividade exteriorizada de política no .NET Framework 4.5
ms.date: 03/30/2017
ms.assetid: 92fd6f92-23a1-4adf-b96a-2754ea93ad3e
ms.openlocfilehash: 52dad208aacf2993acffa605b896c14c0a906d4e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631210"
---
# <a name="externalized-policy-activity-in-net-framework-45"></a>Atividade exteriorizada de política no .NET Framework 4.5

Este exemplo demonstra como a atividade ExternalizedPolicy4 permite a execução de objetos existentes .NET Framework 3,5 Windows Workflow Foundation (WF 3,5) <xref:System.Workflow.Activities.Rules.RuleSet> no [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] Windows Workflow Foundation (WF 4,5) diretamente usando o mecanismo de regras que é enviado no WF 3,5. Usando esta atividade, você pode abrir e executar qualquer WF existente <xref:System.Workflow.Activities.Rules.RuleSet>3,5. Para obter mais informações sobre o mecanismo de regras do WF 3,5 incluído como parte do Windows Workflow Foundation, leia [introdução ao mecanismo de regras de Windows Workflow Foundation](/previous-versions/dotnet/articles/aa480193(v=msdn.10)). Para obter mais informações sobre como migrar regras para [!INCLUDE[wf1](../../../../includes/wf1-md.md)] [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] o no, consulte as [diretrizes de migração](../migration-guidance.md).

## <a name="projects-in-this-sample"></a>Projetos nisso exemplo

|Nome do projeto|Descrição|Arquivos de chave|
|-|-|-|
|ExternalizedPolicy4|Contém a atividade ExternalizedPolicy4 e o designer de WF 4,5.|**ExternalizedPolicy4.cs**: definição da atividade.<br /><br /> **ExternalizedPolicy4Designer. XAML**: designer personalizado para atividade ExternalizedPolicy4. Usar o editor das regras (<xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>) do mecanismo de regras WF 3,5.|
|ImperativeCodeClientSample|Aplicativo cliente de exemplo que configura e executa um fluxo de trabalho usando um aplicativo ExternalizedPolicy4 usando o código em c obrigatório (nenhum designer usado).|**ApplyDiscount. Rules**: file com [!INCLUDE[wf1](../../../../includes/wf1-md.md)] definições de regra.<br /><br /> **Order.cs**: tipo que representa uma ordem de cliente. As regras são aplicadas a objetos desse tipo.<br /><br /> **Program.cs**: configura e executa um fluxo de trabalho que tem uma atividade Policy4 para aplicar regras definidas em ApplyDiscount. Rules a instâncias de objetos Order.<br /><br /> App.config: O arquivo de configuração com o caminho do arquivo de regras.|
|DesignerClientSample|Aplicativo cliente de exemplo que configura e executa um fluxo de trabalho usando um aplicativo ExternalPolicy4 no designer de [!INCLUDE[wf1](../../../../includes/wf1-md.md)] .|**Sequence1. XAML**: fluxo de trabalho Sequencial que usa uma atividade Policy4 para executar avaliações de regra.<br /><br /> **Program.cs**: executa uma instância do fluxo de trabalho definido em Sequence1. XAML.|

## <a name="the-externalizedpolicy4-activity"></a>A atividade ExternalizedPolicy4

A atividade ExternalizedPolicy4 é <xref:System.Activities.NativeActivity> que permite executar objetos de WF 3,5 <xref:System.Workflow.Activities.Rules.RuleSet> dentro de fluxos de trabalho WF 4,5. O exemplo a seguir é uma definição do modelo simplificada de objeto utilitário da atividade.

```csharp
public class ExternalizedPolicy4Activity<TResult>: CodeActivity
{
    public string RulesFilePath

    public string RuleSetName

    [RequiredArgument]
    public InArgument<T> TargetObject

    [RequiredArgument]
    public OutArgument<T> ResultObject

    public OutArgument<ValidationErrorCollection> ValidationErrors
}
```

|Propriedade|Descrição|
|-|-|
|RuleSetFilePath|Caminho para o arquivo do .NET Framework 3.5 <xref:System.Workflow.Activities.Rules.RuleSet> a ser avaliado quando a atividade é executada.|
|RuleSetName|Nome de <xref:System.Workflow.Activities.Rules.RuleSet> a ser usado dentro do arquivo de .rules.|
|TargetObject|O objeto em que <xref:System.Workflow.Activities.Rules.Rule> objetos em <xref:System.Workflow.Activities.Rules.RuleSet> é avaliado contra.|
|ResultObject|O objeto resultante depois que as regras são aplicadas (por exemplo, regras é aplicado no argumento de entrada e o resultado é armazenado no argumento de resultado.|
|ValidationError|A lista de erros de validação retornado pelo mecanismo de regras WF 3,5 para validar contra <xref:System.Workflow.Activities.Rules.RuleSet> o objeto alvo antes de execução.|

## <a name="externalizedpolicy4-activity-designer"></a>Designer de atividade ExternalizedPolicy4

O designer ExternalizedPolicy4 permite que você configure uma atividade para usar um RuleSet existente sem escrever código. Apenas definir o caminho onde o arquivo de .rules é encontrado e especifica o nome de <xref:System.Workflow.Activities.Rules.RuleSet> que você deseja uso. Também permite que você altere <xref:System.Workflow.Activities.Rules.RuleSet>. Após compilar a solução, pode ser encontrado na caixa de ferramentas na seção Microsoft.Samples.Activities.Rules. O designer permite que você selecione um arquivo de .rules e um <xref:System.Workflow.Activities.Rules.RuleSet>. Quando o botão **Editar RuleSet** é clicado, o WF 3,5 <xref:System.Workflow.Activities.Rules.Design.RuleSetDialog> é exibido. Esta caixa de diálogo é o editor hospedado novamente de regras WF 3,5 e é usada para exibir e editar as regras que a atividade ExternalizedPolicy4 executa.

## <a name="policy4-and-externalpolicy4"></a>Policy4 e ExternalPolicy4

A atividade Policy permite criar e executar um conjunto de regras .NET Framework 3,5 em um fluxo de trabalho do WF 4,5. <xref:System.Workflow.Activities.Rules.RuleSet> é embutido serializado Policy4 na definição da atividade XAML. O exemplo ExternalizedPolicy4 mostra como usar <xref:System.Workflow.Activities.Rules.RuleSet> externo existente (contido em um arquivo de .rules).

## <a name="use-this-sample"></a>Use este exemplo

Qualquer configuração especial é necessária para executar este exemplo. Abra a solução no Visual Studio e pressione **F5** para executar o aplicativo.

Este exemplo contém dois aplicativos cliente: ImperativeCodeClientSample e DesignerClientSample. O cliente de ImperativeCodeClientSample mostra como configurar e executar a atividade ExternalizedPolicy4 usando o código obrigatório C#. O DesignerClientSample mostra como configurar e executar a atividade ExternalizedPolicy4 usando o designer.

### <a name="run-the-imperativecodeclientsample-application"></a>Executar o aplicativo ImperativeCodeClientSample

1. Usando o Visual Studio, abra o arquivo de solução *Policy4sample. sln* .

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **ImperativeCodeClientSample** e selecione **definir como projeto de inicialização**.

3. Para executar o projeto, pressione **Ctrl** + **F5**.

### <a name="run-the-designerclientsample-application"></a>Executar o aplicativo DesignerClientSample

1. Usando o Visual Studio, abra o arquivo de solução *Policy4sample. sln* .

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DesignerClientSample** e selecione **definir como projeto de inicialização**.

3. Pressione **Ctrl** + **Shift** + **B** para compilar o projeto.

4. Pressione **Ctrl** + **F5** para executar o projeto.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos.
>
> Este exemplo está no seguinte diretório:
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Rules-ExternalizedPolicy4`
