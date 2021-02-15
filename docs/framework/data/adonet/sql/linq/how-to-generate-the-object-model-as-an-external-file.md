---
description: 'Saiba mais sobre: como gerar o modelo de objeto como um arquivo externo'
title: 'Como: gerar o modelo de objeto como um arquivo externo'
ms.date: 03/30/2017
ms.assetid: 2496fa06-3df4-4ecb-86c4-70a49ea08565
ms.openlocfilehash: 7270e0204b1de5c56d9bc7bf9df89f72d8030e7b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738891"
---
# <a name="how-to-generate-the-object-model-as-an-external-file"></a>Como: gerar o modelo de objeto como um arquivo externo

Como uma alternativa para o mapeamento baseado em atributos, você pode gerar seu modelo de objeto como um arquivo externo XML usando a ferramenta de linha de comando SQLMetal. Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md). Usando um arquivo de mapeamento externo XML, você reduz a confusão em seu código. Você também pode alterar o comportamento alterando o arquivo externo sem recompilar os binários do seu aplicativo. Para obter mais informações, consulte [mapeamento externo](external-mapping.md).  
  
> [!NOTE]
> O Object Relational Designer não oferece suporte à geração de um arquivo de mapeamento externo.  
  
## <a name="example"></a>Exemplo  

 O comando a seguir gerencia um arquivo externo de mapeamento de base de dados de exemplo Northwind.  
  
```console  
sqlmetal /server:myserver /database:northwind /map:externalfile.xml  
```  
  
## <a name="example"></a>Exemplo  

 O seguinte trecho de um arquivo de mapeamento externo mostra o mapeamento para a tabela clientes na base de dados de exemplo Northwind. Esse trecho foi gerado pela execução de SqlMetal com a opção **/MAP** .  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Database xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Name="northwnd">  
  <Table Name="Customers">  
    <Type Name=".Customer">  
      <Column Name="CustomerID" Member="CustomerID" Storage="_CustomerID" DbType="NChar(5) NOT NULL" CanBeNull="False" IsPrimaryKey="True" />  
      <Column Name="CompanyName" Member="CompanyName" Storage="_CompanyName" DbType="NVarChar(40) NOT NULL" CanBeNull="False" />  
      <Column Name="ContactName" Member="ContactName" Storage="_ContactName" DbType="NVarChar(30)" />  
      <Column Name="ContactTitle" Member="ContactTitle" Storage="_ContactTitle" DbType="NVarChar(30)" />  
      <Column Name="Address" Member="Address" Storage="_Address" DbType="NVarChar(60)" />  
      <Column Name="City" Member="City" Storage="_City" DbType="NVarChar(15)" />  
      <Column Name="Region" Member="Region" Storage="_Region" DbType="NVarChar(15)" />  
      <Column Name="PostalCode" Member="PostalCode" Storage="_PostalCode" DbType="NVarChar(10)" />  
      <Column Name="Country" Member="Country" Storage="_Country" DbType="NVarChar(15)" />  
      <Column Name="Phone" Member="Phone" Storage="_Phone" DbType="NVarChar(24)" />  
      <Column Name="Fax" Member="Fax" Storage="_Fax" DbType="NVarChar(24)" />  
      <Association Name="FK_CustomerCustomerDemo_Customers" Member="CustomerCustomerDemos" Storage="_CustomerCustomerDemos" ThisKey="CustomerID" OtherTable="CustomerCustomerDemo" OtherKey="CustomerID" DeleteRule="NO ACTION" />  
      <Association Name="FK_Orders_Customers" Member="Orders" Storage="_Orders" ThisKey="CustomerID" OtherTable="Orders" OtherKey="CustomerID" DeleteRule="NO ACTION" />  
    </Type>  
  </Table>  
</Database>  
```  
  
## <a name="see-also"></a>Consulte também

- [Criando o modelo de objeto](creating-the-object-model.md)
- [Mapeamento externo](external-mapping.md)
- [Como: gerar o modelo de objeto em Visual Basic ou em C#](how-to-generate-the-object-model-in-visual-basic-or-csharp.md)
