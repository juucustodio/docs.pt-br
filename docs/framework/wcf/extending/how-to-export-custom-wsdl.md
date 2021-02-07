---
description: 'Saiba mais sobre: como exportar WSDL personalizado'
title: 'Como: exportar o WSDL personalizado'
ms.date: 03/30/2017
ms.assetid: 5c1e4b58-b76b-472b-9635-2f80d42a0734
ms.openlocfilehash: 3893e02807bce3db66e469abd5dc38808f530f01
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735017"
---
# <a name="how-to-export-custom-wsdl"></a>Como: exportar o WSDL personalizado

Este tópico explica como exportar informações personalizadas de WSDL. Para fazer isso, vamos definir um novo atributo de código chamado `WsdlDocumentationAttribute` que adicionará informações personalizadas ao WSDL gerado pelo serviço.

## <a name="to-export-custom-wsdl-information"></a>Para exportar informações personalizadas de WSDL

1. Implemente a interface <xref:System.ServiceModel.Description.IWsdlExportExtension>. Essa interface pode ser implementada em uma classe que implementa qualquer uma das seguintes interfaces: <xref:System.ServiceModel.Description.IOperationBehavior> , <xref:System.ServiceModel.Description.IContractBehavior> ou <xref:System.ServiceModel.Description.IEndpointBehavior> . Ele também pode ser implementado em uma classe derivada de <xref:System.ServiceModel.Channels.BindingElement> . Este exemplo implementa <xref:System.ServiceModel.Description.IWsdlExportExtension> em uma classe de atributo que implementa <xref:System.ServiceModel.Description.IContractBehavior> .

2. <xref:System.ServiceModel.Description.IWsdlExportExtension> define dois métodos <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%28System.ServiceModel.Description.WsdlExporter%2CSystem.ServiceModel.Description.WsdlEndpointConversionContext%29> e <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%28System.ServiceModel.Description.WsdlExporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> . Esses métodos permitem modificar ou adicionar (ou modificar e adicionar) informações adicionais no <xref:System.ServiceModel.Description.WsdlContractConversionContext> . Este exemplo, no <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%28System.ServiceModel.Description.WsdlExporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> método, recupera uma coleção de <xref:System.ServiceModel.Description.OperationDescription> objetos e, em seguida, itera pela verificação de coleção para um `WsdlDocumentationAttribute` . Se um for encontrado, o texto associado ao atributo será extraído, um elemento de resumo será gerado e o elemento Summary será adicionado ao `DocumentationElement` da operação.

    ```csharp
    public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)
    {
        Console.WriteLine("Inside ExportContract");
        if (context.Contract != null)
        {
            // Set the document element; if this is not done first, there is no XmlElement in the
            // DocumentElement property.
            context.WsdlPortType.Documentation = string.Empty;
            // Contract comments.
            XmlDocument owner = context.WsdlPortType.DocumentationElement.OwnerDocument;
            XmlElement summaryElement = Formatter.CreateSummaryElement(owner, this.Text);
            context.WsdlPortType.DocumentationElement.AppendChild(summaryElement);

            foreach (OperationDescription op in context.Contract.Operations)
            {
                Operation operation = context.GetOperation(op);
                object[] opAttrs = op.SyncMethod.GetCustomAttributes(typeof(WsdlDocumentationAttribute), false);
                if (opAttrs.Length == 1)
                {
                    string opComment = ((WsdlDocumentationAttribute)opAttrs[0]).Text;

                    // This.Text returns the string for the operation-level attributes.
                    // Set the doc element; if this is not done first, there is no XmlElement in the
                    // DocumentElement property.
                    operation.Documentation = String.Empty;

                    XmlDocument opOwner = operation.DocumentationElement.OwnerDocument;
                    XmlElement newSummaryElement = Formatter.CreateSummaryElement(opOwner, opComment);
                    operation.DocumentationElement.AppendChild(newSummaryElement);
                }
            }
        }
    }
    ```

## <a name="example"></a>Exemplo

O exemplo de código a seguir mostra a implementação completa da `WsdlDocumentationAttribute` classe.

```csharp
public class WsdlDocumentationAttribute : Attribute, IContractBehavior, IWsdlExportExtension
{
string text;
       XmlElement customWsdlDocElement = null;
public WsdlDocumentationAttribute(string text)
{ this.text = text;}

       public WsdlDocumentationAttribute(XmlElement wsdlDocElement)
        { this.customWsdlDocElement = wsdlDocElement; }

        public XmlElement WsdlDocElement
        {
            get { return this.customWsdlDocElement; }
            set { this.customWsdlDocElement = value; }
        }
       public string Text
{
get { return this.text; }
set { this.text = value; }
}

     public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)
{
          Console.WriteLine("Inside ExportContract");
if (context.Contract != null)
{
                // Set the document element; if this is not done first, there is no XmlElement in the
                // DocumentElement property.
                context.WsdlPortType.Documentation = string.Empty;
                // Contract comments.
                XmlDocument owner = context.WsdlPortType.DocumentationElement.OwnerDocument;
                XmlElement summaryElement = Formatter.CreateSummaryElement(owner, this.Text);
                context.WsdlPortType.DocumentationElement.AppendChild(summaryElement);

                foreach (OperationDescription op in context.Contract.Operations)
                {
                    Operation operation = context.GetOperation(op);
                    object[] opAttrs = op.SyncMethod.GetCustomAttributes(typeof(WsdlDocumentationAttribute), false);
                    if (opAttrs.Length == 1)
                    {
                        string opComment = ((WsdlDocumentationAttribute)opAttrs[0]).Text;

                        // This.Text returns the string for the operation-level attributes.
                        // Set the document element; if this is not done first, there is no XmlElement in the
                        // DocumentElement property.
                        operation.Documentation = String.Empty;

                        XmlDocument opOwner = operation.DocumentationElement.OwnerDocument;
                        XmlElement newSummaryElement = Formatter.CreateSummaryElement(opOwner, opComment);
                        operation.DocumentationElement.AppendChild(newSummaryElement);
                    }
                }
            }
        }

public void ExportEndpoint(WsdlExporter exporter, WsdlEndpointConversionContext context)
        {
            Console.WriteLine("ExportEndpoint called.");
        }

        public void AddBindingParameters(ContractDescription description, ServiceEndpoint endpoint, BindingParameterCollection parameters)
        { return; }

        public void ApplyClientBehavior(ContractDescription description, ServiceEndpoint endpoint, ClientRuntime client)
        { return; }

        public void ApplyDispatchBehavior(ContractDescription description, ServiceEndpoint endpoint, DispatchRuntime dispatch)
        { return; }

        public void Validate(ContractDescription description, ServiceEndpoint endpoint) { return; }
    }

  public class Formatter
  {

#region Utility Functions

    public static XmlElement CreateSummaryElement(XmlDocument owningDoc, string text)
    {
      XmlElement summaryElement = owningDoc.CreateElement("summary");
      summaryElement.InnerText = text;
      return summaryElement;
    }

public static CodeCommentStatementCollection FormatComments(string text)
{
      /*
       * Note that in Visual C# the XML comment format absorbs a
       * documentation element with a line break in the middle. This sample
       * could take an XmlElement and create code comments in which
       * the element never had a line break in it.
      */

      CodeCommentStatementCollection collection = new CodeCommentStatementCollection();
collection.Add(new CodeCommentStatement("From WsdlDocumentation:", true));
collection.Add(new CodeCommentStatement(String.Empty, true));

foreach (string line in WordWrap(text, 80))
{
collection.Add(new CodeCommentStatement(line, true));
}

collection.Add(new CodeCommentStatement(String.Empty, true));
return collection;
}

public static Collection<string> WordWrap(string text, int columnWidth)
{
Collection<string> lines = new Collection<string>();
System.Text.StringBuilder builder = new System.Text.StringBuilder();

string[] words = text.Split(' ');
foreach (string word in words)
{
if ((builder.Length > 0) && ((builder.Length + word.Length + 1) > columnWidth))
{
lines.Add(builder.ToString());
builder = new System.Text.StringBuilder();
}
builder.Append(word);
builder.Append(' ');
}
lines.Add(builder.ToString());

return lines;
}

#endregion

    public static XmlElement CreateReturnsElement(XmlDocument owner, string p)
    {
      XmlElement returnsElement = owner.CreateElement("returns");
      returnsElement.InnerText = p;
      return returnsElement;
    }
  }
```

## <a name="see-also"></a>Consulte também

- [Metadados](../feature-details/metadata.md)
