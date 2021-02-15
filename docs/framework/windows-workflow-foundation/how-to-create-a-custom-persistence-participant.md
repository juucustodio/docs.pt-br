---
description: 'Saiba mais sobre: como criar um participante de persistência personalizado'
title: 'Como: criar um participante de persistência personalizado'
ms.date: 03/30/2017
ms.assetid: 1d9cc47a-8966-4286-94d5-4221403d9c06
ms.openlocfilehash: a0bdd8407bf409e7e485f4f32a0dd3f61e6f82b0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742089"
---
# <a name="how-to-create-a-custom-persistence-participant"></a>Como: criar um participante de persistência personalizado

O seguinte procedimento tem as etapas para criar um participante de persistência. Consulte o tópico [participando da persistência](/previous-versions/dotnet/netframework-4.0/dd699769(v=vs.100)) e a [extensibilidade de armazenamento](store-extensibility.md) para obter exemplos de implementações de participantes de persistência.  
  
1. Crie uma classe que deriva de <xref:System.Activities.Persistence.PersistenceParticipant> ou classe de <xref:System.Activities.Persistence.PersistenceIOParticipant> . A classe PersistenceIOParticipant oferece os mesmos pontos de extensibilidade que a classe PersistenceParticipant, além de ser capaz de participar de operações de e/s. Execute uma ou mais das seguintes etapas.  
  
2. Implementar o método de <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> . O método **CollectValues** tem dois parâmetros de dicionário, um para armazenar valores de leitura/gravação e o outro para armazenar valores somente gravação (usados posteriormente em consultas). Nesse método, você deve preencher esses dicionários com dados que são específicos para um participante de persistência. Cada dicionário contém o nome do valor como a chave e o valor próprio como um objeto de <xref:System.Runtime.DurableInstancing.InstanceValue> .  
  
    Os valores no dicionário readWriteValues são empacotados como objetos **InstanceValue** . Os valores no dicionário somente gravação são empacotados como objetos **InstanceValue** com InstanceValueOptions. optional e InstanceValueOption. WriteOnly definido. Cada **InstanceValue** fornecida pelas implementações de **CollectValues** em todos os participantes de persistência deve ter um nome exclusivo.
  
    ```csharp  
    protected virtual void CollectValues(out IDictionary<XName,Object> readWriteValues, out IDictionary<XName,Object> writeOnlyValues)
    {
    }
    ```  
  
3. Implementar o método de <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> . O método **MapValues** usa dois parâmetros semelhantes aos parâmetros que o método **CollectValues** recebe. Todos os valores coletados no estágio **CollectValues** são passados por meio desses parâmetros de dicionário. Os novos valores adicionados pelo estágio **MapValues** são adicionados aos valores somente gravação.  O dicionário somente gravação é usado para fornecer dados para uma fonte externa associada não diretamente com os valores da instância. Cada valor fornecido pelas implementações do método **MapValues** em todos os participantes da persistência deve ter um nome exclusivo.  
  
    ```csharp  
    protected virtual IDictionary<XName,Object> MapValues(IDictionary<XName,Object> readWriteValues,IDictionary<XName,Object> writeOnlyValues)
    {
    }
    ```  
  
     O método de <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> fornece funcionalidade que o <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> contrário, que permite uma dependência em outro valor fornecido por outro participante de persistência que não é processado pelo <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> ainda.  
  
4. Implemente o método **PublishValues** . O método **PublishValues** recebe um dicionário contendo todos os valores carregados do repositório de persistência.  
  
    ```csharp  
    protected virtual void PublishValues(IDictionary<XName,Object> readWriteValues)
    {
    }
    ```  
  
5. Implemente o método **BeginOnSave** se o participante for um participante de e/s de persistência. Este método é chamado durante uma operação de salvar. Nesse método, você deve executar suplemento de e/s para as instâncias de fluxo de trabalho persistentes (salvando).  Se o host está usando uma transação para o comando correspondente de persistência, a mesma transação é fornecida em Transaction.Current.  Além disso, PersistenceIOParticipants pode anunciar um requisito transacional de consistência, nesse caso o host cria uma transação para o episódio de persistência se não seria usado de outra maneira.  
  
    ```csharp  
    protected virtual IAsyncResult BeginOnSave(IDictionary<XName,Object> readWriteValues, IDictionary<XName,Object> writeOnlyValues, TimeSpan timeout, AsyncCallback callback, Object state)
    {
    }
    ```  
  
6. Implemente o método **BeginOnLoad** se o participante for um participante de e/s de persistência. Este método é chamado durante uma operação de carregamento. Nesse método, você deve executar suplemento de e/s para o carregamento de instâncias de fluxo de trabalho. Se o host está usando uma transação para o comando correspondente de persistência, a mesma transação é fornecida em Transaction.Current. Além disso, os participantes de e/s de persistência podem anunciar um requisito de consistência transacional; nesse caso, o host criará uma transação para o episódio de persistência se, de outra forma, não for usado.  
  
    ```csharp  
    protected virtual IAsyncResult BeginOnLoad(IDictionary<XName,Object> readWriteValues, TimeSpan timeout, AsyncCallback callback, Object state)
    {
    }
    ```
