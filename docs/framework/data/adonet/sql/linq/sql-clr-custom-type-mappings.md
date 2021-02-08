---
description: 'Saiba mais sobre: mapeamentos de tipo personalizado do SQL-CLR'
title: Mapeamentos de tipo personalizados de SQL-CLR
ms.date: 03/30/2017
ms.assetid: d916c7fb-4b56-4214-acbe-5e23365047b2
ms.openlocfilehash: 5ad929ae4a47964b333616867ad01da2892c21af
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803744"
---
# <a name="sql-clr-custom-type-mappings"></a>Mapeamentos de tipo personalizados de SQL-CLR

O mapeamento de classificação entre o SQL Server e o Common Language Runtime (CLR) é especificado automaticamente quando você usa a ferramenta de linha de comando SQLMetal, Object Relational Designer (object relational Designer de Objetos).  
  
 Quando nenhum mapeamento personalizado é executado, essas ferramentas atribuem mapeamentos de tipo padrão, conforme descrito em [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md). Se você desejar digitar de maneira diferente mapeamentos dessas opções, você precisa fazer algumas personalização dos mapeamentos de tipo.  
  
 Para personalizar mapeamentos de tipo, a abordagem recomendada é fazer alterações em um arquivo DBML intermediária. Em seguida, o arquivo DBML personalizado deve ser usado quando você cria o código e arquivos de mapeamento com o SQLMetal ou o object relational Designer de Objetos.  
  
 Uma vez que você instancia o objeto de <xref:System.Data.Linq.DataContext> de código e arquivos de mapeamento, o método de <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> cria um base de dados com base nos mapeamentos de tipo que são especificados. Se não houver nenhum atributo de CLR `type` especificado nos mapeamentos, os mapeamentos de tipo padrão será usado.  
  
## <a name="customization-with-sqlmetal-or-or-designer"></a>Personalização com SQLMetal ou object relational Designer de Objetos  

 Com SQLMetal e object relational Designer de Objetos, você pode criar automaticamente um modelo de objetos que inclui informações de mapeamento de tipo dentro ou fora do arquivo de código. Como esses arquivos são substituídos por SQLMetal ou por object relational Designer de Objetos, cada vez que você recria seus mapeamentos, a abordagem recomendada para especificar mapeamentos de tipo personalizados é personalizar um arquivo DBML.  
  
 Para personalizar mapeamentos de tipo com SQLMetal ou object relational Designer de Objetos, primeiro gerencia um arquivo DBML. Em seguida, antes de gerar o arquivo ou o arquivo de mapeamento de código, modifique o arquivo DBML para identificar os mapeamentos desejados de tipo. Com SQLMetal, você tem que alterar manualmente os atributos de `Type` e de `DbType` no arquivo DBML para fazer suas personalizações de mapeamento de tipo. Com object relational Designer de Objetos, você pode fazer suas alterações no designer. Para obter mais informações sobre o uso do o/R Designer, consulte [ferramentas de LINQ to SQL no Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).  
  
> [!NOTE]
> Alguns mapeamentos de tipo podem resultar em estouro ou exceções de perda de dados ao converter para ou do banco de dados. Examine atentamente a matriz de comportamento de tempo de execução de mapeamento de tipo no [mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md) antes de fazer qualquer personalização.  
  
 Para que as personalizações de mapeamento de tipo são reconhecidas por SQLMetal ou por object relational Designer de Objetos, você precisará certificar-se de que essas ferramentas são fornecidas com o caminho para o arquivo DBML personalizado quando você gerencia o arquivo de código ou arquivos de mapeamento externo. Embora não seja necessário para personalização de mapeamento de tipo, é recomendável que você sempre separa suas informações de mapeamento de tipo do arquivo de código e gerencia o mapeamento de arquivo externo adicional do tipo. Isso deixar alguma flexibilidade não exigem que o arquivo de código seja recompilado.  
  
## <a name="incorporating-database-changes"></a>Inserindo alterações de base de dados  

 Quando seu base de dados, você precisará atualizar o arquivo DBML para refletir as alterações. Uma maneira de fazer isso é automaticamente criar um novo arquivo DBML e novamente faz nas personalizações de mapeamento de tipo. Como alternativa, você pode comparar as diferenças entre seu novo arquivo DBML e o arquivo DBML personalizado e atualizar o arquivo DBML personalizado manualmente para refletir a alteração de base de dados.  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md)
- [Geração de código em LINQ para SQL](code-generation-in-linq-to-sql.md)
