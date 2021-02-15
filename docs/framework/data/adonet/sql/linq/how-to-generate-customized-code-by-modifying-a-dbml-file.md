---
description: 'Saiba mais sobre: como gerar código personalizado modificando um arquivo DBML'
title: 'Como: gerar código personalizado modificando um arquivo DBML'
ms.date: 03/30/2017
ms.assetid: 50ad597a-8598-42d3-82dd-fc7d702ebc37
ms.openlocfilehash: 0dd4024b3f6a0ca0583de6bfbdb7463fab14d969
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785998"
---
# <a name="how-to-generate-customized-code-by-modifying-a-dbml-file"></a>Como: gerar código personalizado modificando um arquivo DBML

Você pode gerar o código-fonte do Visual Basic ou C# de um arquivo de metadados da linguagem de marcação de banco de dados (. dbml). Essa abordagem fornece uma oportunidade para personalizar o arquivo .dbml padrão antes de você gerar o código de mapeamento do aplicativo. Esse é um recurso avançado.  
  
 As etapas nesse processo são as seguintes:  
  
1. Gere um arquivo .dbml.  
  
2. Use um editor para modificar o arquivo .dbml. Observe que o arquivo. dbml deve validar em relação ao arquivo de definição de esquema (. xsd) para [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] arquivos. dbml. Para obter mais informações, consulte [geração de código em LINQ to SQL](code-generation-in-linq-to-sql.md).  
  
3. Gere o código-fonte do Visual Basic ou C#.  
  
 Os exemplos a seguir usam a ferramenta de linha de comando SQLMetal. Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="example"></a>Exemplo  

 O código a seguir gera um arquivo .dbml do banco de dados de exemplo Northwind. Como a origem para os metadados de banco de dados, você pode usar o nome do banco de dados ou o nome do arquivo .mdf.  
  
```console  
sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml  
sqlmetal /dbml:mymeta.dbml mydbfile.mdf  
```  
  
## <a name="example"></a>Exemplo  

 O código a seguir gera Visual Basic ou o arquivo de código-fonte C# de um arquivo. dbml.  
  
```console
sqlmetal /namespace:nwind /code:nwind.vb /language:vb DBMLFile.dbml  
sqlmetal /namespace:nwind /code:nwind.cs /language:csharp DBMLFile.dbml  
```  
  
## <a name="see-also"></a>Consulte também

- [Geração de código em LINQ para SQL](code-generation-in-linq-to-sql.md)
- [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [Criando o modelo de objeto](creating-the-object-model.md)
