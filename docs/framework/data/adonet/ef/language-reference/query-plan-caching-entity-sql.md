---
description: 'Saiba mais sobre: cache de plano de consulta (Entity SQL)'
title: Armazenamento em cache do plano de consulta (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 90b0c685-5ef2-461b-98b4-c3c0a2b253c7
ms.openlocfilehash: eee8e3afcd6f97b7e6021389d59a8ce03507fb9f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802093"
---
# <a name="query-plan-caching-entity-sql"></a>Armazenamento em cache do plano de consulta (Entity SQL)

Sempre que uma tentativa de executar uma consulta é feita, o pipeline de consulta pesquisa seu cache do plano de consulta para ver se a consulta exata já está compilada e disponível. Em caso afirmativo, reutiliza o plano armazenado em cachê em vez de criar um novo. Se uma correspondência não for encontrada no cache do plano de consulta, a consulta é criada e armazenadas em cachê. Uma consulta é identificada por sua coleção de texto e o parâmetro de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] (nomes e tipos). Todas as comparações de texto diferenciam maiúsculas de minúsculas.  
  
## <a name="configuration"></a>Configuração  

 O cachê do plano de consulta é configurável com <xref:System.Data.EntityClient.EntityCommand>.  
  
 Para ativar ou desativar a consulta planejar o cachê com <xref:System.Data.EntityClient.EntityCommand.EnablePlanCaching%2A?displayProperty=nameWithType>, defina essa propriedade como `true` ou a `false`. Desativar o cachê de fundo para consultas dinâmicos individuais que são improvável de ser usado mais uma vez em melhora o desempenho.  
  
 Você pode ativar o cachê do plano de consulta com <xref:System.Data.Objects.ObjectQuery.EnablePlanCaching%2A>.  
  
## <a name="recommended-practice"></a>Prática recomendada  

 Consultas dinâmicos devem ser evitadas, geralmente. O exemplo a seguir dinâmica de consulta é vulnerável a ataques de injeção SQL, porque recebe entrada do usuário diretamente sem qualquer validação.  
  
 ```csharp
 var query = "SELECT sp.SalesYTD FROM AdventureWorksEntities.SalesPerson as sp WHERE sp.EmployeeID = " + employeeTextBox.Text;  
 ```

 Se você usar consultas gerados dinamicamente, considere desativar o cachê do plano de consulta para evitar desnecessário consumo de memória para as entradas de cache que são improvável de ser reutilizado.  
  
 Consulte o cachê de fundo em consultas estáticos e consultas parametrizadas podem fornecer benefícios de desempenho. A seguir está um exemplo de uma consulta estático:  
  
```csharp
var query = "SELECT sp.SalesYTD FROM AdventureWorksEntities.SalesPerson as sp";  
```  
  
 Para que as consultas são igualadas corretamente pelo cache do plano de consulta, devem estar de acordo com os seguintes requisitos:  
  
- O texto da consulta deve ser um padrão constante, de preferência um cadeia de caracteres constante ou um recurso.  
  
- <xref:System.Data.EntityClient.EntityParameter> ou <xref:System.Data.Objects.ObjectParameter> devem ser usados em qualquer lugar que um valor de fornecido deve ser passado.  
  
 Você deve evitar os seguintes padrões de consulta, que consomem desnecessariamente slots no cache do plano de consulta:  
  
- Alterações em caso de letra em texto.  
  
- Alterações no espaço em branco.  
  
- Alterações em valores literais.  
  
- Alterações ao texto dentro de comentários.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
