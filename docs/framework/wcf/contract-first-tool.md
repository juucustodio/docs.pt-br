---
description: 'Saiba mais sobre: Contract-First ferramenta'
title: Ferramenta Contract-First
ms.date: 03/30/2017
ms.assetid: 0a880690-f460-4475-a5f4-9f91ce08fcc6
ms.openlocfilehash: 6455fa866afd440e70062f8433356b13fe163a8c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736395"
---
# <a name="contract-first-tool"></a>Ferramenta Contract-First

Os contratos de serviço geralmente precisam ser criados a partir de serviços existentes. No .NET Framework 4,5 e posterior, as classes de contrato de dados podem ser criadas automaticamente de serviços existentes usando a ferramenta contratar primeiro contrato. Para usar a ferramenta contratar primeiro o contrato, o arquivo de definição de esquema XML (XSD) deve ser baixado localmente; a ferramenta não pode importar contratos de dados remotos via HTTP.

 A ferramenta contratar primeiro é integrada ao Visual Studio 2012 como uma tarefa de compilação. Os arquivos de código gerados pela tarefa de compilação são criados toda vez que o projeto é compilado, para que o projeto possa adotar facilmente as alterações no contrato de serviço subjacente.

 Os tipos de esquema que a ferramenta contratar pela primeira vez podem importar incluem o seguinte:

```xml
<xsd:complexType>
 <xsd:simpleType>
 </xsd:simpleType>
</xsd:complexType>
```

 Tipos simples não serão gerados se forem primitivos como `Int16` ou `String` ; tipos complexos não serão gerados se forem do tipo `Collection` . Os tipos também não serão gerados se fizerem parte de outro `xsd:complexType` . Em todos esses casos, os tipos serão referenciados aos tipos existentes no projeto.

## <a name="adding-a-data-contract-to-a-project"></a>Adicionando um contrato de dados a um projeto

 Antes que a ferramenta contratar primeiro o contrato possa ser usada, o contrato de serviço (XSD) deve ser adicionado ao projeto. Para os fins desta visão geral, o contrato a seguir será usado para ilustrar as funções primeiro do contrato. Essa definição de serviço é um pequeno subconjunto do contrato de serviço usado pela API de pesquisa do Bing.

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema id="ServiceSchema"
    targetNamespace="http://tempuri.org/ServiceSchema.xsd"
    elementFormDefault="qualified"
    xmlns="http://tempuri.org/ServiceSchema.xsd"
    xmlns:mstns="http://tempuri.org/ServiceSchema.xsd"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
>
  <xs:complexType name="SearchRequest">
    <xs:sequence>
      <xs:element minOccurs="0" maxOccurs="1" name="Version" type="xs:string" default="2.2" />
      <xs:element minOccurs="0" maxOccurs="1" name="Market" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="UILanguage" type="xs:string" />
      <xs:element minOccurs="1" maxOccurs="1" name="Query" type="xs:string" />
      <xs:element minOccurs="1" maxOccurs="1" name="AppId" type="xs:string" />
      <xs:element minOccurs="0" maxOccurs="1" name="Latitude" type="xs:double" />
      <xs:element minOccurs="0" maxOccurs="1" name="Longitude" type="xs:double" />
      <xs:element minOccurs="0" maxOccurs="1" name="Radius" type="xs:double" />
    </xs:sequence>
  </xs:complexType>
  <xs:simpleType name="WebSearchOption">
    <xs:restriction base="xs:string">
      <xs:enumeration value="DisableHostCollapsing" />
      <xs:enumeration value="DisableQueryAlterations" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

 Para adicionar o contrato de serviço acima ao projeto, clique com o botão direito do mouse no projeto e selecione **Adicionar novo...**. Selecione definição de esquema no painel WCF da caixa de diálogo modelos e nomeie o novo arquivo SampleContract. xsd. Copie e cole o código acima na exibição de código do novo arquivo.

## <a name="configuring-contract-first-options"></a>Configurando opções de contrato primeiro

 As opções contrato-primeiro podem ser configuradas no menu Propriedades de um projeto do WCF. Para habilitar o desenvolvimento de primeiro contrato, marque a caixa de seleção **habilitar XSD como linguagem de definição de tipo** na página WCF da janela Propriedades do projeto.

 ![Captura de tela das opções do WCF com desenvolvimento de primeiro contrato habilitado.](./media/contract-first-tool/contract-first-options.png)

 Para configurar propriedades avançadas, clique no botão Avançado.

 ![Caixa de diálogo Configurações avançadas de geração de código de contrato.](./media/contract-first-tool/advanced-contract-settings.png)

 As configurações avançadas a seguir podem ser configuradas para geração de código de contratos. As configurações só podem ser configuradas para todos os arquivos no projeto; as configurações não podem ser configuradas para arquivos individuais neste momento.

- **Modo de serializador**: essa configuração determina qual serializador é usado para ler arquivos de contrato de serviço. Quando o **serializador de XML** é selecionado, as opções **tipos de coleção** e **reutilização de tipos** são desabilitadas. Essas opções se aplicam somente ao **serializador de contrato de dados**.

- **Reutilizar tipos**: essa configuração especifica quais bibliotecas são usadas para reutilização de tipo. Essa configuração se aplicará somente se o **modo de serializador** estiver definido como **serializador de contrato de dados**.

- **Tipo de coleção**: essa configuração especifica o tipo totalmente qualificado ou qualificado por assembly a ser usado para o tipo de dados da coleção. Essa configuração se aplicará somente se o **modo de serializador** estiver definido como **serializador de contrato de dados**.

- **Tipo de dicionário**: essa configuração especifica o tipo totalmente qualificado ou qualificado por assembly a ser usado para o tipo de dados do dicionário.

- **EnableDataBinding**: essa configuração especifica se a interface deve ser implementada <xref:System.ComponentModel.INotifyPropertyChanged> em todos os tipos de dados para implementar a vinculação de dados.

- **ExcludedTypes**: essa configuração especifica a lista de tipos totalmente qualificados ou qualificados por assembly a serem excluídos dos assemblies referenciados. Essa configuração se aplicará somente se o **modo de serializador** estiver definido como **serializador de contrato de dados**.

- **GenerateInternalTypes**: essa configuração especifica se as classes que estão marcadas como internas devem ser geradas. Essa configuração se aplicará somente se o **modo de serializador** estiver definido como **serializador de contrato de dados**.

- **GenerateSerializableTypes**: essa configuração especifica se as classes devem ser geradas com o <xref:System.SerializableAttribute> atributo. Essa configuração se aplicará somente se o **modo de serializador** estiver definido como **serializador de contrato de dados**.

- **ImportXMLTypes**: essa configuração especifica se o serializador de contrato de dados deve ser configurado para aplicar o <xref:System.SerializableAttribute> atributo a classes sem o <xref:System.Runtime.Serialization.DataContractAttribute> atributo.  Essa configuração se aplicará somente se o **modo de serializador** estiver definido como **serializador de contrato de dados**.

- **SupportFx35TypedDataSets**: essa configuração especifica se é para fornecer funcionalidade adicional para conjuntos de dados tipados criados para .NET Framework 3,5. Quando o  **modo de serializador** for definido como **serializador XML**, a <xref:System.Data.Design.TypedDataSetSchemaImporterExtensionFx35> extensão será adicionada ao importador de esquema XML quando esse valor for definido como true. Quando o  **modo de serializador** é definido como **serializador de contrato de dados**, o tipo <xref:System.DateTimeOffset> será excluído das referências quando esse valor for definido como false, para que um <xref:System.DateTimeOffset> sempre seja gerado para versões mais antigas do Framework.

- **InputXsdFiles**: essa configuração especifica a lista de arquivos de entrada. Cada arquivo deve conter um esquema XML válido.

- **Idioma**: essa configuração especifica o idioma do código de contrato gerado. A configuração deve ser reconhecível pelo <xref:System.CodeDom.Compiler.CodeDomProvider> .

- **NamespaceMappings**: essa configuração especifica os mapeamentos dos namespaces de destino XSD para namespaces CLR. Cada mapeamento deve usar o seguinte formato:

    ```xml
    "Schema Namespace, CLR Namespace"
    ```

     O serializador de XML aceita apenas um mapeamento no seguinte formato:

    ```xml
    "*, CLR Namespace"
    ```

- **OutputDirectory**: essa configuração especifica o diretório onde os arquivos de código serão gerados.

 As configurações serão usadas para gerar tipos de contrato de serviço a partir dos arquivos de contrato de serviço quando o projeto for compilado.

## <a name="using-contract-first-development"></a>Usando o desenvolvimento de primeiro contrato

 Depois de adicionar o contrato de serviço ao projeto e confirmar as configurações de compilação, compile o projeto pressionando **F6**. Os tipos definidos no contrato de serviço estarão disponíveis para uso no projeto.

 Para usar os tipos definidos no contrato de serviço, adicione uma referência a `ContractTypes` no namespace atual:

```csharp
using MyProjectNamespace.ContractTypes;
```

 Os tipos definidos no contrato de serviço serão resolvidos no projeto, conforme mostrado abaixo:

 ![Classe SearchRequest mostrada no IntelliSense depois de digitar as primeiras letras.](./media/contract-first-tool/service-contract-types.png)

 Os tipos gerados pela ferramenta são criados no arquivo GeneratedXSDTypes.cs. O arquivo é criado no \<project directory> diretório/obj/ \<build configuration> /XSDGeneratedCode/por padrão. O esquema de exemplo no início deste artigo é convertido da seguinte maneira:

```csharp
//------------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by a tool.
//     Runtime Version:4.0.30319.17330
//
//     Changes to this file may cause incorrect behavior and will be lost if
//     the code is regenerated.
// </auto-generated>
//------------------------------------------------------------------------------

namespace TestXSD3.ContractTypes
{
    using System.Xml.Serialization;

    /// <remarks/>
    [System.CodeDom.Compiler.GeneratedCodeAttribute("System.Xml", "4.0.30319.17330")]
    [System.SerializableAttribute()]
    [System.Diagnostics.DebuggerStepThroughAttribute()]
    [System.ComponentModel.DesignerCategoryAttribute("code")]
    [System.Xml.Serialization.XmlTypeAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd")]
    [System.Xml.Serialization.XmlRootAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd", IsNullable=true)]
    public partial class SearchRequest
    {

        private string versionField;

        private string marketField;

        private string uILanguageField;

        private string queryField;

        private string appIdField;

        private double latitudeField;

        private bool latitudeFieldSpecified;

        private double longitudeField;

        private bool longitudeFieldSpecified;

        private double radiusField;

        private bool radiusFieldSpecified;

        public SearchRequest()
        {
            this.versionField = "2.2";
        }

        /// <remarks/>
        [System.ComponentModel.DefaultValueAttribute("2.2")]
        public string Version
        {
            get
            {
                return this.versionField;
            }
            set
            {
                this.versionField = value;
            }
        }

        /// <remarks/>
        public string Market
        {
            get
            {
                return this.marketField;
            }
            set
            {
                this.marketField = value;
            }
        }

        /// <remarks/>
        public string UILanguage
        {
            get
            {
                return this.uILanguageField;
            }
            set
            {
                this.uILanguageField = value;
            }
        }

        /// <remarks/>
        public string Query
        {
            get
            {
                return this.queryField;
            }
            set
            {
                this.queryField = value;
            }
        }

        /// <remarks/>
        public string AppId
        {
            get
            {
                return this.appIdField;
            }
            set
            {
                this.appIdField = value;
            }
        }

        /// <remarks/>
        public double Latitude
        {
            get
            {
                return this.latitudeField;
            }
            set
            {
                this.latitudeField = value;
            }
        }

        /// <remarks/>
        [System.Xml.Serialization.XmlIgnoreAttribute()]
        public bool LatitudeSpecified
        {
            get
            {
                return this.latitudeFieldSpecified;
            }
            set
            {
                this.latitudeFieldSpecified = value;
            }
        }

        /// <remarks/>
        public double Longitude
        {
            get
            {
                return this.longitudeField;
            }
            set
            {
                this.longitudeField = value;
            }
        }

        /// <remarks/>
        [System.Xml.Serialization.XmlIgnoreAttribute()]
        public bool LongitudeSpecified
        {
            get
            {
                return this.longitudeFieldSpecified;
            }
            set
            {
                this.longitudeFieldSpecified = value;
            }
        }

        /// <remarks/>
        public double Radius
        {
            get
            {
                return this.radiusField;
            }
            set
            {
                this.radiusField = value;
            }
        }

        /// <remarks/>
        [System.Xml.Serialization.XmlIgnoreAttribute()]
        public bool RadiusSpecified
        {
            get
            {
                return this.radiusFieldSpecified;
            }
            set
            {
                this.radiusFieldSpecified = value;
            }
        }
    }

    /// <remarks/>
    [System.CodeDom.Compiler.GeneratedCodeAttribute("System.Xml", "4.0.30319.17330")]
    [System.SerializableAttribute()]
    [System.Xml.Serialization.XmlTypeAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd")]
    [System.Xml.Serialization.XmlRootAttribute(Namespace="http://tempuri.org/ServiceSchema.xsd", IsNullable=false)]
    public enum WebSearchOption
    {

        /// <remarks/>
        DisableHostCollapsing,

        /// <remarks/>
        DisableQueryAlterations,
    }
}
```

## <a name="errors-and-warnings"></a>Erros e avisos

 Erros e avisos encontrados na análise do esquema XSD serão exibidos como erros e avisos de compilação.

## <a name="interface-inheritance"></a>Herança de interface

 Não é possível usar a herança de interface com desenvolvimento de primeiro contrato; Isso é consistente com a maneira como as interfaces se comportam em outras operações. Para usar uma interface que herda uma interface base, use dois pontos de extremidade separados. O primeiro ponto de extremidade usa o contrato herdado e o segundo ponto de extremidade implementa a interface base.
