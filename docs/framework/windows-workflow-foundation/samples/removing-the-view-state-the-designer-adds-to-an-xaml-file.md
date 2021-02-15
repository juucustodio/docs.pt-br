---
description: 'Saiba mais sobre: removendo o estado de exibição que o designer adiciona a um arquivo XAML'
title: Removendo o estado de exibição que o designer adiciona a um arquivo XAML – WF
ms.date: 03/30/2017
ms.assetid: a801ce22-8699-483c-a392-7bb3834aae4f
ms.openlocfilehash: e6be1e8e4f754085b98f912923ad67cb12893910
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741790"
---
# <a name="removing-the-view-state-the-designer-adds-to-an-xaml-file"></a>Removendo o estado de exibição que o designer adiciona a um arquivo XAML

Este exemplo demonstra como criar uma classe que deriva de <xref:System.Xaml.XamlWriter> e se remova o modo estado de um arquivo XAML. O Windows Designer de Fluxo de Trabalho grava informações no documento XAML, que é conhecido como estado de exibição. O estado de exibição se refere à informação que é necessária em tempo de design, como o posicionamento de layout, que não é necessário em runtime. Designer de Fluxo de Trabalho insere essas informações no documento XAML conforme ele é editado. Designer de Fluxo de Trabalho grava o estado de exibição no arquivo XAML com o `mc:Ignorable` atributo, portanto, essas informações não são carregadas quando o tempo de execução carrega o arquivo XAML. Este exemplo demonstra como criar uma classe que remove essas informações de estado de exibição ao processar nós XAML.

## <a name="discussion"></a>Discussão

Este exemplo demonstra como criar um text writer personalizado.

Para criar um text writer personalizado XAML, crie uma classe que herda de <xref:System.Xaml.XamlWriter>. Como os gravadores XAML geralmente são aninhados, é comum manter o controle de um gravador XAML "interno". Esses gravadores "internos" podem ser considerados como referência à pilha restante de gravadores XAML, permitindo que você tenha vários pontos de entrada para realizar o trabalho e, em seguida, delegue o processamento para o restante da pilha.

Nesse exemplo, há alguns itens de interesse. Um é a verifique se o item que está sendo gravada for um namespace de designer. Observe que isso também tira para fora o uso de outros tipos de namespace de designer em um fluxo de trabalho.

```csharp
static Boolean IsDesignerAttachedProperty(XamlMember xamlMember)
{
    return xamlMember.IsAttachable &&
        xamlMember.PreferredXamlNamespace.Equals(c_sapNamespaceURI, StringComparison.OrdinalIgnoreCase);
}

const String c_sapNamespaceURI = "http://schemas.microsoft.com/netfx/2009/xaml/activities/presentation";

// The next item of interest is the constructor, where the utilization of the inner XAML writer is seen.
public ViewStateCleaningWriter(XamlWriter innerWriter)
{
    this.InnerWriter = innerWriter;
    this.MemberStack = new Stack<XamlMember>();
}

XamlWriter InnerWriter {get; set; }
Stack<XamlMember> MemberStack {get; set; }
```

Isso também cria uma pilha de membros XAML que são usados para atravessar o fluxo de nó. O trabalho restante deste exemplo é contido amplamente no método de `WriteStartMember` .

```csharp
public override void WriteStartMember(XamlMember xamlMember)
{
    MemberStack.Push(xamlMember);

    if (IsDesignerAttachedProperty(xamlMember))
    {
        m_attachedPropertyDepth++;
    }

    if (m_attachedPropertyDepth > 0)
    {
        return;
    }

    InnerWriter.WriteStartMember(xamlMember);
}
```

Os métodos subsequentes verifique para ver se ainda estão contidos em um recipiente de estado de exibição, e em caso afirmativo, retorno, e não passam o nó abaixo da pilha o gravador.

```csharp
public override void WriteValue(Object value)
{
    if (m_attachedPropertyDepth > 0)
    {
        return;
    }

    InnerWriter.WriteValue(value);
}
```

Para usar um text writer personalizado XAML, você deve encadear-la juntos em uma pilha de criadores de XAML. O código a seguir mostra como esse pode ser usado.

```csharp
XmlWriterSettings writerSettings = new XmlWriterSettings {  Indent = true };
XmlWriter xmlWriter = XmlWriter.Create(File.OpenWrite(args[1]), writerSettings);
XamlXmlWriter xamlWriter = new XamlXmlWriter(xmlWriter, new XamlSchemaContext());
XamlServices.Save(new ViewStateCleaningWriter(ActivityXamlServices.CreateBuilderWriter(xamlWriter)), ab);
```

## <a name="to-use-this-sample"></a>Para usar este exemplo

1. Usando o Visual Studio 2010, abra o arquivo de solução ViewStateCleaningWriter. sln.

2. Abra um prompt de comando e navegue para o diretório onde o ViewStageCleaningWriter.exe é criado.

3. Executar ViewStateCleaningWriter.exe no arquivo de Workflow1.xaml.

   A sintaxe para o arquivo executável é mostrada no exemplo a seguir.

   ```console
   ViewStateCleaningWriter.exe [input file] [output file]
   ```

   Isso gera um arquivo XAML para \[ outfile], que tem todas as suas informações de estado de exibição removidas.

> [!NOTE]
> Para um fluxo de trabalho <xref:System.Activities.Statements.Sequence> , um número de dicas de virtualização são removidos. Isso faz com que o designer recalcule o layout na próxima vez que é carregado. Quando você usa este exemplo para <xref:System.Activities.Statements.Flowchart>, qualquer posicionamento e linha informações de roteamento são removidos e a carga subsequente no designer, todas as atividades são empilhadas no lado esquerdo da tela.

## <a name="to-create-a-sample-xaml-file-for-use-with-this-sample"></a>Para criar um arquivo XAML exemplo para uso com esse exemplo

1. Abra o Visual Studio 2010.

2. Criar um novo aplicativo de console do fluxo de trabalho.

3. Arrastar e soltar quaisquer atividades na tela

4. Salve o arquivo de fluxo de trabalho XAML.

5. Inspecione o arquivo XAML para ver as propriedades anexadas do estado de exibição.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\ViewStateCleaningWriter`
