---
description: 'Saiba mais sobre: como gerar o modelo de objeto em Visual Basic ou C #'
title: 'Como: gerar o modelo de objeto em Visual Basic ou em C#'
ms.date: 03/30/2017
ms.assetid: a0c73b33-5650-420c-b9dc-f49310c201ee
ms.openlocfilehash: d842a646f9f6186d252d10297618ddc2cb137e70
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785959"
---
# <a name="how-to-generate-the-object-model-in-visual-basic-or-c"></a>Como gerar o modelo de objeto em Visual Basic ou C\#

No [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], um modelo de objeto em sua própria linguagem de programação é mapeado para um banco de dados relacional. Duas ferramentas estão disponíveis para gerar automaticamente um modelo de Visual Basic ou C# a partir dos metadados de um banco de dados existente.  
  
- Se você estiver usando o Visual Studio, poderá usar o Object Relational Designer para gerar um modelo de objeto. O o/R Designer fornece uma rica interface do usuário para ajudá-lo a gerar um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] modelo de objeto. Para obter mais informações, consulte [Ferramentas do LINQ to SQL no Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).
  
- A ferramenta de linha de comando SQLMetal. Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
    > [!NOTE]
    > Se você não tiver um banco de dados existente e não quiser criar um a partir de um modelo de objeto, poderá criar seu modelo de objeto usando o editor de códigos e <xref:System.Data.Linq.DataContext.CreateDatabase%2A>. Para obter mais informações, consulte [como criar dinamicamente um banco de dados](how-to-dynamically-create-a-database.md).  
  
 A documentação do o/R Designer fornece exemplos de como gerar um modelo de objeto Visual Basic ou C# usando o o/R Designer. As informações a seguir fornecem exemplos de como usar a ferramenta de linha de comando SqlMetal. Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="example"></a>Exemplo  

 A linha de comando SqlMetal mostrada no exemplo a seguir produz Visual Basic código como o modelo de objeto baseado em atributo do banco de dados de exemplo Northwind. Os procedimentos armazenados e funções são renderizados também.  
  
```console  
sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions  
```  
  
## <a name="example"></a>Exemplo  

 A linha de comando SQLMetal mostrada no exemplo a seguir gera código C# como o modelo de objeto baseado em atributos de banco de dados de exemplo Northwind. Os procedimentos armazenados e funções também são processados, e os nomes de tabela são automaticamente pluralizados.  
  
```console  
sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize  
```  
  
## <a name="see-also"></a>Consulte também

- [Guia de programação](programming-guide.md)
- [Modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md)
- [Aprendendo com explicações passo a passo](learning-by-walkthroughs.md)
- [Como: personalizar classes de entidade usando o editor de códigos](how-to-customize-entity-classes-by-using-the-code-editor.md)
- [Mapeamento baseado em atributos](attribute-based-mapping.md)
- [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [Mapeamento externo](external-mapping.md)
- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
- [Criando o modelo de objeto](creating-the-object-model.md)
