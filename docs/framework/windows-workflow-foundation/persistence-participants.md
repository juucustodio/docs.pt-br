---
description: 'Saiba mais sobre: participantes da persistência'
title: Participantes de persistência
ms.date: 03/30/2017
ms.assetid: f84d2d5d-1c1b-4f19-be45-65b552d3e9e3
ms.openlocfilehash: 66f39bfe5b9efcae5d8377fda9415efd4cab9468
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742050"
---
# <a name="persistence-participants"></a>Participantes de persistência

Um participante de persistência pode participar em uma operação de persistência (salvar) ou carregamento disparada por um aplicativo host. O [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] é fornecido com duas classes abstratas, **PersistenceParticipant** e **PersistenceIOParticipant**, que você pode usar para criar um participante de persistência. Um participante de persistência deriva de uma dessas classes, implementa-se os métodos de interesse, e então adiciona uma instância da classe à coleção de <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A> em <xref:System.ServiceModel.Activities.WorkflowServiceHost> . O aplicativo host pode procurar essas extensões de fluxo de trabalho para manter uma instância de fluxo de trabalho e chama métodos apropriados nos participantes de persistência em momentos apropriadas.  
  
 A lista a seguir descreve as tarefas executadas pelo subsistema de persistência em diferentes estágios da operação persistir (salvar). Os participantes de persistência são usados em terceira e quartas etapas. Se o participante for um participante de e/s (um participante de persistência que também participa de operações de e/s), o participante também será usado no sexto estágio.  
  
1. Obtém os valores internos, incluindo o estado de fluxo de trabalho, indexadores, variáveis mapeados, e carimbo de data/hora.  
  
2. Coleta todos os participantes de persistência que foram adicionados à coleção de extensão associada com a instância de fluxo de trabalho.  
  
3. Chama o método de <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> implementado por todos os participantes de persistência.  
  
4. Chama o método de <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> implementado por todos os participantes de persistência.  
  
5. Persistir ou salvar o fluxo de trabalho no armazenamento de persistência.  
  
6. Invoca o <xref:System.Activities.Persistence.PersistenceIOParticipant.BeginOnSave%2A> método em todos os participantes de e/s de persistência. Se o participante não for um participante de e/s, essa tarefa será ignorada. Se o episódio de persistência é transacional, a transação é fornecida na propriedade de Transaction.Current.  
  
7. Aguarda que todos os participantes de persistência terminem. Se todos os participantes são bem-sucedidas em manter dados de instância, confirmações a transação.  
  
 Um participante de persistência deriva da classe **PersistenceParticipant** e pode implementar os métodos **CollectValues** e **MapValues** . Um participante de e/s de persistência deriva da classe **PersistenceIOParticipant** e pode implementar o método **BeginOnSave** , além de implementar os métodos **CollectValues** e **MapValues** .  
  
 Cada etapa é concluída antes que a fase seguir inicia. Por exemplo, os valores são coletados de **todos os** participantes de persistência no primeiro estágio. Todos os valores coletados na primeira etapa são fornecidos na todos os participantes de persistência na segunda etapa mapeando. Em todos os valores coletados e mapeados no primeiro e na segunda etapas são fornecidos para o provedor de persistência na terceira etapa, e assim por diante.  
  
 A lista a seguir descreve as tarefas executadas pelo subsistema de persistência em diferentes estágios da operação de carregamento. Os participantes de persistência são usados na quarta fase. Os participantes de e/s de persistência (participantes de persistência que também participam de operações de e/s) também são usados no terceiro estágio.  
  
1. Coleta todos os participantes de persistência que foram adicionados à coleção de extensão associada com a instância de fluxo de trabalho.  
  
2. Carrega o fluxo de trabalho do armazenamento de persistência.  
  
3. Invoca o <xref:System.Activities.Persistence.PersistenceIOParticipant.BeginOnLoad%2A> em todos os participantes de e/s de persistência e aguarda a conclusão de todos os participantes da persistência. Se o episódio de persistência é transacional, a transação é fornecida em Transaction.Current.  
  
4. Carrega a instância de fluxo de trabalho na memória com base nos dados recuperados do armazenamento de persistência.  
  
5. Chama o <xref:System.Activities.Persistence.PersistenceParticipant.PublishValues%2A> em cada participante de persistência.  
  
 Um participante de persistência deriva da classe **PersistenceParticipant** e pode implementar o método **PublishValues** . Um participante de e/s de persistência deriva da classe **PersistenceIOParticipant** e pode implementar o método **BeginOnLoad** , além da implementação do método **PublishValues** .  
  
 Ao carregar uma instância de fluxo de trabalho o provedor de persistência cria um bloqueio nessa instância. Isso impede que a instância é carregada por mais de um host em um cenário com vários nós. Se você tentar carregar uma instância de fluxo de trabalho que ela é bloqueada verão uma exceção como o seguinte: A exceção “System.ServiceModel.Persistence.InstanceLockException: A operação solicitada não pôde completar porque o bloqueio “00000000-0000-0000-0000-000000000000” não pôde ser encontrado”. Esse erro é causado quando ocorre um destes procedimentos:  
  
- Em um cenário com vários nós a instância é carregada por outro host.  Há algumas maneiras diferentes para resolver esses tipos de conflitos: encaminhar o processamento para o nó que possui o bloqueio e a nova tentativa, ou forçar a carga que fará com que o outro host é possível de salvar seu trabalho.  
  
- Em um cenário de único nó e no host falhou.  Quando o host inicia anterior novamente (um processo reciclar ou criando uma nova factory do provedor de persistência) o novo host tenta carregar uma instância que é bloqueada ainda pelo host antigo porque o bloqueio ainda não expirou.  
  
- Em um cenário de único nó e na instância em questão foi anuladas em algum ponto e uma nova instância do provedor de persistência é criada que tenha uma identificação diferente do host  
  
 O valor de tempo limite de bloqueio tem um valor padrão de 5 minutos, você pode especificar um valor de tempo limite diferente ao chamar <xref:System.ServiceModel.Persistence.PersistenceProvider.Load%2A>.  
  
## <a name="in-this-section"></a>Nesta seção  
  
- [Como: criar um participante de persistência personalizado](how-to-create-a-custom-persistence-participant.md)  
  
## <a name="see-also"></a>Consulte também

- [Extensibilidade de Store](store-extensibility.md)
