---
description: 'Saiba mais sobre: identidade de objeto'
title: Identidade do objeto
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c788f2f9-65cc-4455-9907-e8388a268e00
ms.openlocfilehash: 1e525250e37e697e33ee53ea59b973882633ec15
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695509"
---
# <a name="object-identity"></a>Identidade do objeto

Os objetos em runtime têm identidades exclusivas. Duas variáveis que referem-se ao mesmo objeto realmente referem-se à mesma instância de objeto. Devido ao fato, as alterações feitas por um caminho com uma variável imediatamente são visíveis com o outro.  
  
 As linhas em uma tabela de base de dados relacional não têm identidades exclusivas. Porque cada linha tem uma chave primária exclusivo, não há duas linhas compartilham o mesmo valor principal. No entanto, esse fato restringe somente o conteúdo da tabela de base de dados.  
  
 Na realidade, os dados são trazidos freqüêntemente fora de base de dados e uma camada diferente, onde o aplicativo funciona com ele. Esse é o modelo que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] suporta. Quando dados são trazidos fora de base de dados como linhas, você não tem nenhuma expectativa que duas linhas que representam os mesmos dados realmente correspondem às mesmas instâncias de linha. Se você consultar um cliente específico duas vezes, obterá duas linhas de dados. Cada linha contém as mesmas informações.  
  
 Com objetos você espera algo muito diferentes. Você espera que se você solicitar <xref:System.Data.Linq.DataContext> a mesma informações repetidamente, dará de fato a mesma instância de objeto. Você espera esse comportamento como os objetos têm significado especial para seu aplicativo e os você espera se comportem como objetos. Você os criou como hierarquias ou grafos. Você espera recuperá-los como esta'n e não receber multidões de instâncias replicadas exatamente como você solicitou a mesma coisa mais de uma vez.  
  
 Em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], <xref:System.Data.Linq.DataContext> gerencia a identidade do objeto. Sempre que você recupera uma nova linha de base de dados, a linha é entrada uma tabela de identidade por sua chave primária, e um novo objeto é criado. Sempre que você mesmo que recupera linhas, a instância original de objeto é entregada de volta para o aplicativo. Assim <xref:System.Data.Linq.DataContext> converte o conceito de identidade como mostrado por base de dados (isto é, chaves primárias) no conceito de identidade consultado pela linguagem (isto é, instâncias). O aplicativo considera apenas o objeto no estado que foi recuperado primeiro. Novos dados, se diferentes, são descartados. Para obter mais informações, consulte [recuperando objetos do cache de identidade](retrieving-objects-from-the-identity-cache.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o usa essa abordagem para gerenciar a integridade de objetos locais a fim de oferecer suporte a atualizações otimistas. Porque as únicas alterações que ocorrem após o objeto é criado no início essas são feitas pelo aplicativo, a intenção de aplicativo são claras. Se as alterações por uma parte externo ocorreram em ínterim, são identificadas em `SubmitChanges()` é chamado.  
  
> [!NOTE]
> Se o objeto solicitado pela consulta é facilmente identificável porque se já recuperado, nenhuma consulta é executada. A tabela de identidade atua como um cache de todos os objetos anteriormente recuperados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="object-caching-example-1"></a>Exemplo de cache de objeto 1  

 Nesse exemplo, se você executa a mesma consulta duas vezes, você receberá uma referência ao mesmo objeto na memória todas as vezes.  
  
 [!code-csharp[DLinqObjectIdentity#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#1)]
 [!code-vb[DLinqObjectIdentity#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#1)]  
  
### <a name="object-caching-example-2"></a>Objeto que armazena em cachê o exemplo 2  

 Nesse exemplo, se você executa as diferentes consultas que retornam a mesma linha de base de dados, você receberá uma referência ao mesmo objeto na memória todas as vezes.  
  
 [!code-csharp[DLinqObjectIdentity#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#2)]
 [!code-vb[DLinqObjectIdentity#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
