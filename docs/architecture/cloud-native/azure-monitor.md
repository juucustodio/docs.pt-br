---
title: Azure Monitor
description: Usar Azure Monitor para obter visibilidade do seu sistema está em execução.
ms.date: 01/19/2021
ms.openlocfilehash: a93b71db642e05a830b20b80d8387c24d35ea8c1
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506169"
---
# <a name="azure-monitor"></a>Azure Monitor

Nenhum outro provedor de nuvem tem o mesmo que uma solução de monitoramento de aplicativo em nuvem que foi encontrada no Azure. Azure Monitor é um nome abrangente para uma coleção de ferramentas projetadas para fornecer visibilidade do estado do seu sistema. Ele ajuda a entender como os serviços nativos de nuvem estão sendo executados e identifica de forma proativa os problemas que os afetam. A Figura 7-12 apresenta um alto nível de exibição de Azure Monitor.

![Exibição de alto nível de Azure Monitor. ](./media/azure-monitor.png)
 **Figura 7-12**. Exibição de alto nível de Azure Monitor.

## <a name="gathering-logs-and-metrics"></a>Coletando logs e métricas

A primeira etapa em qualquer solução de monitoramento é reunir o máximo de dados possível. Quanto mais dados forem coletados, mais profundo é o Insight. Os sistemas de instrumentação tradicionalmente eram difíceis. O SNMP (Simple Network Management Protocol) era o protocolo Gold padrão para coletar informações no nível do computador, mas exigia uma grande quantidade de conhecimento e configuração. Felizmente, grande parte desse trabalho árduo foi eliminado, pois as métricas mais comuns são coletadas automaticamente pelo Azure Monitor.

Os eventos e as métricas de nível de aplicativo não são possíveis para instrumentar automaticamente porque são específicos do aplicativo que está sendo implantado. Para reunir essas métricas, há [SDKs e APIs disponíveis](/azure/azure-monitor/app/api-custom-events-metrics) para relatar diretamente essas informações, como quando um cliente se inscreve ou conclui um pedido. As exceções também podem ser capturadas e relatadas de volta para Azure Monitor por meio de Application Insights. Os SDKs dão suporte à maioria de todos os idiomas encontrados em aplicativos nativos de nuvem, incluindo Go, Python, JavaScript e linguagens .NET.

O objetivo final da coleta de informações sobre o estado do seu aplicativo é garantir que seus usuários finais tenham uma boa experiência. Qual é a melhor maneira de saber se os usuários estão enfrentando problemas do que fazer [testes da Web externos](/azure/azure-monitor/app/monitor-web-app-availability)? Esses testes podem ser tão simples quanto executar ping em seu site de locais em todo o mundo ou se envolver como os agentes fazem logon no site e simulam ações do usuário.

## <a name="reporting-data"></a>Dados de relatórios

Depois que os dados são coletados, eles podem ser manipulados, resumidos e plotados em gráficos, o que permite que os usuários vejam instantaneamente quando há problemas. Esses gráficos podem ser coletados em painéis ou em pastas de trabalho, um relatório de várias páginas projetado para contar uma história sobre algum aspecto do sistema.

Nenhum aplicativo moderno estaria completo sem alguma inteligência artificial ou aprendizado de máquina. Para esse fim, os dados [podem ser passados](https://www.youtube.com/watch?v=Cuza-I1g9tw) para as várias ferramentas de aprendizado de máquina no Azure para permitir que você extraia tendências e informações que, de outra forma, seriam ocultas.

Application Insights fornece uma linguagem de consulta poderosa (semelhante ao SQL) chamada *Kusto* , que pode consultar registros, resumir e até mesmo gráficos de plotagem. Por exemplo, a consulta a seguir localizará todos os registros do mês de novembro de 2007, agrupá-los por Estado e plotar os 10 primeiros como um gráfico de pizza.

```kusto
StormEvents
| where StartTime >= datetime(2007-11-01) and StartTime < datetime(2007-12-01)
| summarize count() by State
| top 10 by count_
| render piechart
```

A Figura 7-13 mostra os resultados dessa Application Insights consulta.

![Application Insights resultados da consulta, ](./media/application_insights_example.png)
 **Figura 7-13**. Application Insights resultados da consulta.

Há um [playground para experimentar as consultas do Kusto](https://dataexplorer.azure.com/clusters/help/databases/Samples) . A leitura de [consultas de exemplo](/azure/kusto/query/samples) também pode ser instrutiva.

## <a name="dashboards"></a>Dashboards

Há várias tecnologias de painel diferentes que podem ser usadas para trazer as informações de Azure Monitor. Talvez a mais simples seja apenas executar consultas em Application Insights e [plotar os dados em um gráfico](/azure/azure-monitor/learn/tutorial-app-dashboards).

![Um exemplo de gráficos de Application Insights incorporados no painel principal do Azure, ](./media/azure_dashboard.png)
 **Figura 7-14**. Um exemplo de gráficos de Application Insights incorporados no painel principal do Azure.

Esses gráficos podem então ser inseridos no portal do Azure apropriado pelo uso do recurso de painel. Para usuários com mais requisitos de ação, como a possibilidade de fazer uma busca detalhada em várias camadas de dados, Azure Monitor dados estão disponíveis para [Power bi](https://powerbi.microsoft.com/). Power BI é uma ferramenta de classe empresarial, líder do setor, business intelligence que pode agregar dados de várias fontes de dados diferentes.

![Um exemplo Power BI Dashboard](./media/powerbidashboard.png)

**Figura 7-15**. Um exemplo Power BI Dashboard.

## <a name="alerts"></a>Alertas

Às vezes, ter painéis de dados é insuficiente. Se ninguém estiver atento a assistir aos painéis, ele ainda poderá ser muitas horas antes que um problema seja resolvido ou até mesmo detectado. Para esse fim, Azure Monitor também fornece uma solução de [alerta](/azure/azure-monitor/platform/alerts-overview)de entalhe superior. Os alertas podem ser disparados por uma ampla gama de condições, incluindo:

- Valores métricos
- Consultas da pesquisa de logs
- Eventos do Log de Atividades
- Integridade da plataforma subjacente do Azure
- Testes de disponibilidade do site

Quando disparado, os alertas podem executar uma ampla variedade de tarefas. No lado simples, os alertas podem apenas enviar uma notificação por email para uma lista de endereçamento ou uma mensagem de texto para um indivíduo. Alertas mais envolvidos podem disparar um fluxo de trabalho em uma ferramenta como PagerDuty, que reconhece quem está em chamada para um determinado aplicativo. Os alertas podem disparar ações no [Microsoft Flow](https://flow.microsoft.com/) desbloqueando possibilidades ilimitadas para fluxos de trabalho.

Como as causas comuns dos alertas são identificadas, os alertas podem ser aprimorados com detalhes sobre as causas comuns dos alertas e as etapas a serem seguidas para resolvê-los. Implantações de aplicativo nativas de nuvem altamente maduras podem optar por disparar tarefas de auto-recuperação, que executam ações como remover nós com falha de um conjunto de dimensionamento ou disparar uma atividade de dimensionamento automático. Eventualmente, talvez não seja mais necessário ativar o pessoal de chamada em 2AM para resolver um problema de site ativo, pois o sistema poderá se ajustar para compensar ou pelo menos limp até que alguém chegue ao trabalho na manhã seguinte.

Azure Monitor aproveita automaticamente o aprendizado de máquina para entender os parâmetros operacionais normais dos aplicativos implantados. Essa abordagem permite que a ti detecte serviços que estão operando fora de seus parâmetros normais. Por exemplo, o tráfego de dia da semana típico no site pode ser 10.000 solicitações por minuto. E, em seguida, em uma determinada semana, repentinamente, o número de solicitações atinge um 20.000 de solicitações altamente incomuns por minuto. A [detecção inteligente](/azure/azure-monitor/app/proactive-diagnostics) notará esse desvio da norma e disparará um alerta. Ao mesmo tempo, a análise de tendência é inteligente o suficiente para evitar o acionamento de falsos positivos quando a carga de tráfego é esperada.

## <a name="references"></a>Referências

- [Azure Monitor](/azure/azure-monitor/overview)

>[!div class="step-by-step"]
>[Anterior](monitoring-azure-kubernetes.md) 
> [Avançar](identity.md)
