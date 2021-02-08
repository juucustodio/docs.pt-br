---
description: 'Saiba mais sobre: escopo e visibilidade da definição de atividade'
title: Escopo e visibilidade de definição de atividades
ms.date: 03/30/2017
ms.assetid: ccdffa07-9503-4eea-a61b-17f1564368b7
ms.openlocfilehash: ab779fe36473a8888ee0fb0c1b94f1ea6324f991
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787962"
---
# <a name="activity-definition-scoping-and-visibility"></a>Escopo e visibilidade de definição de atividades

O escopo e a visibilidade de definição de atividade, assim como o escopo e a visibilidade de um objeto, são a capacidade de objetos ou outras atividades para acessar membros da atividade. A definição da atividade é executada por implementações seguintes:  
  
1. Determinando os membros (<xref:System.Activities.Argument>, <xref:System.Activities.Variable>, e objetos de <xref:System.Activities.ActivityDelegate> , e atividades filho) expõe de uma atividade para os usuários.  
  
2. Implementando lógica de execução de atividades  
  
 A implementação pode envolver os membros que não são expostos aos consumidores de atividade, mas é um pouco detalhes de implementação.  Semelhante à definição de tipo, o modelo de atividade permite que um autor qualifica a visibilidade de um membro da atividade em relação à definição da atividade sendo definida.  Controla a visibilidade aspectos do membro, como o escopo de dados.  
  
## <a name="scope"></a>Escopo  

 Além do escopo de dados, visibilidade modelo de atividade pode restringir o acesso a outros aspectos da atividade, como validação, a depuração, o rastreamento, ou o rastreamento. As propriedades de execução usam a visibilidade e o escopo para características de execução em um escopo específico de definição. As raízes secundários usam a visibilidade e o escopo para restringir o estado capturado por <xref:System.Activities.Statements.CompensableActivity> escopo de definição em que as atividades compensáveis são usadas.  
  
## <a name="definition-and-usage"></a>Definição e uso  

 Um fluxo de trabalho é escrito pela criação de novas atividades por meio da herança de classes de atividade base e usando atividades da [biblioteca de atividades interna](net-framework-4-5-built-in-activity-library.md). Para usar uma atividade, o autor de atividade deve configurar a visibilidade de cada componente de sua definição.  
  
### <a name="activity-members"></a>Membros de atividades  

 O modelo de atividade define argumentos, variáveis, representantes, e as atividades filhos que a atividade torna disponíveis para os consumidores. Cada um desses membros pode ser declarado como `public` ou `private`. Os membros públicos são configurados pelo consumidor de atividade, enquanto os membros de `private` usam uma implementação fixa pelo autor de atividade. As regras de visibilidade para o escopo de dados são:  
  
1. Os membros públicos e membros públicos de atividades filhos públicas podem referenciar variáveis públicas.  
  
2. Os membros particulares e membros públicos de atividades filhos públicas podem referenciar argumentos e variáveis privadas.  
  
 Um membro que pode ser definido pelo consumidor de uma atividade nunca deve ser feito particular.  
  
### <a name="authoring-models"></a>Criando modelos  

 As atividades personalizados são definidas usando <xref:System.Activities.NativeActivity>, <xref:System.Activities.Activity>, <xref:System.Activities.CodeActivity>, ou <xref:System.Activities.AsyncCodeActivity>. As atividades que derivam dessas classes podem expor tipos diferentes de membro com visibilidades diferentes.  
  
#### <a name="nativeactivity"></a>NativeActivity  

 As atividades que derivam de <xref:System.Activities.NativeActivity> têm o comportamento que é escrito em código obrigatórias, e opcionalmente podem ser definidas usando atividades existentes. Derivando de atividades concede acesso de <xref:System.Activities.NativeActivity> a todos os recursos expostos em runtime. Qualquer membro de uma atividade pode ser definido usando a visibilidade pública ou privadas, exceto os argumentos, que só podem ser declarados como `public`.  
  
 Membros de classes derivadas de <xref:System.Activities.NativeActivity> são declarados em runtime usando a estrutura de <xref:System.Activities.NativeActivityMetadata> passado para o método de <xref:System.Activities.NativeActivity.CacheMetadata%2A> .  
  
#### <a name="activity"></a>Atividade  

 As atividades criadas usando <xref:System.Activities.Activity> têm o comportamento que é criado com estritamente composto outras atividades. A classe de <xref:System.Activities.Activity> tem uma atividade filho de implementação, obtida em runtime usando <xref:System.Activities.Activity.Implementation%2A>. Uma atividade que deriva de <xref:System.Activities.Activity> pode definir argumentos públicos, variáveis públicas, ActivityDelegates importado, e atividades importados.  
  
 ActivityDelegates importado e as atividades são declarados como filhos públicos de atividade, mas não podem ser agendados diretamente pela atividade. Essa informação é usada durante a validação para evitar executar validações pais suporte em locais onde a atividade nunca será executado. Além disso, os filhos importados, assim como filhos públicos, podem ser referenciados e agendada pela implementação de atividade. Isso significa que uma atividade que importe uma atividade chamada Activity1 pode conter <xref:System.Activities.Statements.Sequence> em sua implementação que agenda Activity1.  
  
#### <a name="codeactivity-asynccodeactivity"></a>CodeActivity/AsyncCodeActivity  

 Essa classe base é usada criando o comportamento no código obrigatório. As atividades que derivam dessa classe só tem acesso aos argumentos que expõe. Isso significa que os únicos membros que essas atividades podem expor são argumentos públicos. Nenhuma outra membro ou visibilidade se aplicam às atividades.  
  
#### <a name="summary-of-visibilities"></a>Resumo de visibilidades  

 A tabela a seguir resume informações anteriormente nesta seção.  
  
|Tipo do membro|NativeActivity|Atividade|CodeActivity/AsyncCodeActivity|  
|-----------------|--------------------|--------------|--------------------------------------|  
|Argumentos|Público particular|Público|não aplicável|  
|Variáveis|Público particular|Público|não aplicável|  
|Atividades filhos|Público particular|Público, um filho particular corrigido definido na implementação.|não aplicável|  
|ActivityDelegates|Público particular|Público|não aplicável|  
  
 Em geral, um membro que não pode ser definido pelo consumidor de uma atividade não deve ser feito público.  
  
### <a name="execution-properties"></a>Propriedades de execução  

 Em alguns cenários, é útil o escopo de uma propriedade específica de execução para filhos públicos de uma atividade. A coleção de <xref:System.Activities.ExecutionProperties> fornece esse recurso com o método de <xref:System.Activities.ExecutionProperties.Add%2A> . Este método possui a indicação booleana de um parâmetro de se uma determinada propriedade é o escopo para todos os filhos, ou apenas aqueles que são públicos. Se esse parâmetro é definido como `true`, a propriedade será visível somente a membros públicos e a membros públicos de seus filhos públicos.  
  
### <a name="secondary-roots"></a>Raízes secundários  

 Uma raiz new é o mecanismo do runtime interno para gerenciar o estado para atividades de compensação. Quando <xref:System.Activities.Statements.CompensableActivity> terminou de executar, seu estado não está limpado imediatamente. Em vez disso, o estado é mantido em runtime em uma raiz new até que o episódio de compensação terminar. Os ambientes de local capturados com a raiz new correspondem ao escopo de definição em que a atividade compensável é usada.
