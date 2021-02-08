---
description: 'Saiba mais sobre: determinando a duração da operação de serviço'
title: Determinando a duração da operação de serviço
ms.date: 03/30/2017
ms.assetid: e8a93a2c-2c20-48b3-8986-57e90e9aa908
ms.openlocfilehash: e9dd9ee4113ee4b4521afb6dfaf6a913e72ea5d0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798804"
---
# <a name="determining-service-operation-duration"></a>Determinando a duração da operação de serviço

Se o rastreamento analítico estiver habilitado em um aplicativo Windows Communication Foundation (WCF), a duração da execução de uma operação de serviço poderá ser facilmente determinada ao examinar o log de eventos.  Este tópico demonstra como determinar a quantidade de tempo que uma operação de serviço leva para ser concluída.  
  
### <a name="determining-service-operation-execution-duration"></a>Determinando a duração da execução da operação de serviço  
  
1. Abra Visualizador de Eventos clicando em **Iniciar**, **executar** e inserindo `eventvwr.exe` .  
  
2. Se você não tiver habilitado o rastreamento analítico, expanda **logs de aplicativos e serviços**, **Microsoft**, **Windows**, **servidor de aplicativos-aplicativos**. Selecione **Exibir**, **Mostrar logs analíticos e de depuração**. Clique com o botão direito do mouse em **analítica** e selecione **habilitar log**. Deixe Visualizador de Eventos aberto para que os rastreamentos possam ser exibidos depois que a operação de serviço for executada.  
  
3. Em seguida, abra um aplicativo WCF que inclui um projeto de serviço e um projeto de cliente que interage com esse serviço.  Você pode criar um aplicativo desse tipo seguindo o [tutorial de introdução](../../getting-started-tutorial.md).  Se você tiver os exemplos do WCF instalados, poderá abrir o [introdução](../../samples/getting-started-sample.md), que contém o projeto concluído criado no tutorial.  
  
4. Execute o aplicativo de servidor pressionando **F5**. Execute o aplicativo cliente clicando com o botão direito do mouse no projeto **cliente** e selecionando **depurar**, **Iniciar nova instância**.  
  
5. No Visualizador de Eventos, atualize o log analítico e classifique os eventos por ID do evento.  Procure eventos com a ID de evento [214-OperationCompleted](214-operationcompleted.md).  Esses eventos mostrarão quais operações foram concluídas e qual será a duração da operação.  O evento a seguir mostra a duração de uma operação de adição.  
  
    ```output  
    An OperationInvoker completed the call to the 'Add' method.  The method call duration was '3' ms.  
    ```
