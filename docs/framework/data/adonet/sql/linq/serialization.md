---
description: 'Saiba mais sobre: serialização'
title: Serialization2
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a15ae411-8dc2-4ca3-84d2-01c9d5f1972a
ms.openlocfilehash: f4d9ecd63d4d15744fca4c6a6c61d9737cc8a196
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803770"
---
# <a name="serialization"></a>Serialização

Este tópico descreve os [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] recursos de serialização. Os parágrafos que seguem fornecem informações sobre como adicionar em tempo de design a serialização durante a geração de código e o comportamento de serialização de tempo de execução de classes de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] .  
  
 Você pode adicionar código de serialização em tempo de design por qualquer um dos seguintes métodos:  
  
- No Object Relational Designer, altere a propriedade **modo de serialização** para **unidirecional**.  
  
- Na linha de comando SqlMetal, adicione a opção **/Serialization** . Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="overview"></a>Visão geral  

 O código gerado pelo [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornece recursos de carregamento adiados por padrão. A carga adiada é muito conveniente na camada de- mid para o carregamento transparente de dados sob demanda. No entanto, é problemática para serialização, porque o serializador dispara o carregamento adiada se a carga adiada é destinada ou não. Na verdade, quando um objeto é serializado, o fechamento transitivo em todas as referências adiar- carregadas de saída é serializado.  
  
 O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] recurso de serialização aborda esse problema, principalmente por meio de dois mecanismos:  
  
- Um modo de <xref:System.Data.Linq.DataContext> para desativar a carga adiada (<xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A>). Para obter mais informações, consulte <xref:System.Data.Linq.DataContext>.  
  
- Um interruptor da geração para gerar <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> e atributos de <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> em entidades gerados. Este aspecto, incluindo o comportamento de classes de adiar- carregamento na serialização, é o assunto principal deste tópico.  
  
### <a name="definitions"></a>Definições  
  
- *Serializador DataContract*: serializador padrão usado pelo componente Windows Communication Framework (WCF) do .NET Framework 3,0 ou versões posteriores.  
  
- *Serialização unidirecional*: a versão serializada de uma classe que contém apenas uma propriedade de associação unidirecional (para evitar um ciclo). Por convenção, a propriedade no lado pai de uma relação de chave estrangeira que é marcada para serialização. O outro lado em uma associação bidirecional não é serializado.  
  
     A serialização unidirecional é o único tipo de serialização suportados por [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
## <a name="code-example"></a>Exemplo de código  

 O código a seguir usa `Customer` e classes tradicionais de `Order` de base de dados de exemplo Northwind, e mostra como essas classes são decoradas com atributos de serialização.  
  
 [!code-csharp[DLinqSerialization#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#1)]
 [!code-vb[DLinqSerialization#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#1)]  
  
 [!code-csharp[DLinqSerialization#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#2)]
 [!code-vb[DLinqSerialization#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#2)]  
  
 [!code-csharp[DLinqSerialization#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#3)]
 [!code-vb[DLinqSerialization#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#3)]  
  
 Para a classe de `Order` no exemplo a seguir, apenas a propriedade inverso de associação que corresponde à classe de `Customer` é mostrada para abreviar. Não tem um atributo de <xref:System.Runtime.Serialization.DataMemberAttribute> para evitar um ciclo.  
  
 [!code-csharp[DLinqSerialization#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#4)]
 [!code-vb[DLinqSerialization#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#4)]  
  
 [!code-csharp[DLinqSerialization#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#5)]
 [!code-vb[DLinqSerialization#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#5)]  
  
### <a name="how-to-serialize-the-entities"></a>Como serializar as entidades  

 Você pode serializar as entidades em código mostrados na seção anterior como segue;  
  
 [!code-csharp[DLinqSerialization#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/Program.cs#6)]
 [!code-vb[DLinqSerialization#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/Module1.vb#6)]  
  
### <a name="self-recursive-relationships"></a>Relações são recursivos  

 As relações são recursivos seguem o mesmo padrão. A propriedade de associação que corresponde à chave estrangeira não tem um atributo de <xref:System.Runtime.Serialization.DataMemberAttribute> , enquanto a propriedade pai faz.  
  
 Considere a seguinte classe que tem duas relações recursivos são: Employee.Manager/Reports e Employee.Mentor/Mentees.  
  
 [!code-csharp[DLinqSerialization#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#7)]
 [!code-vb[DLinqSerialization#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#7)]  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
- [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [Como: tornar a entidades serializáveis](how-to-make-entities-serializable.md)
