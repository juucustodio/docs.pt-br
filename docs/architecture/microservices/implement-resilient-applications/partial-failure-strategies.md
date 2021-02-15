---
title: Estratégias para tratar falhas parciais
description: Conheça várias estratégias para tratar falhas parciais normalmente.
ms.date: 10/16/2018
ms.openlocfilehash: 948870aedec7bef4e7db0ed3752fb5185ed134b2
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429228"
---
# <a name="strategies-to-handle-partial-failure"></a>Estratégias para tratar falhas parciais

As estratégias para lidar com falhas parciais incluem o seguinte.

**Usar a comunicação assíncrona (por exemplo, comunicação baseada em mensagens) entre microsserviços internos**. É altamente recomendado não criar cadeias longas de chamadas HTTP síncronas entre os microsserviços internos, porque esse design incorreto poderá se tornar a principal causa de interrupções incorretas. Pelo contrário, exceto pelas comunicações de front-end entre os aplicativos cliente e o primeiro nível de microsserviços ou Gateways de API refinados, é recomendado usar apenas a comunicação assíncrona (com base em mensagem) uma vez após o ciclo inicial de resposta/solicitação, entre os microsserviços internos. Consistência eventual e arquiteturas orientadas a eventos ajudarão a minimizar os efeitos de ondulação. Essas abordagens impõem um nível mais alto de autonomia do microsserviço e, portanto, previnem contra o problema observado aqui.

**Usar novas tentativas com retirada exponencial**. Essa técnica ajuda a evitar falhas curtas e intermitentes executando novas tentativas de chamada um determinado número de vezes, caso o serviço não tivesse estado disponível apenas por um curto período de tempo. Isso pode ocorrer devido a problemas de rede intermitentes ou quando um microsserviço/contêiner é movido para um nó diferente em um cluster. No entanto, se essas novas tentativas não foram criadas corretamente com disjuntores, os efeitos de ondulação poderão ser agravados e, em último caso, poderá até haver uma [DoS (Negação de Serviço)](https://en.wikipedia.org/wiki/Denial-of-service_attack).

**Solução alternativa para tempos limite de rede**. Em geral, os clientes devem ser criados para não serem bloqueados indefinidamente e para sempre usar tempos limite ao aguardar uma resposta. Usar tempos limite garante que os recursos nunca fiquem bloqueados indefinidamente.

**Use o padrão de disjuntor**. Nessa abordagem, o processo do cliente rastreia o número de solicitações com falha. Se a taxa de erro exceder um limite configurado, um "disjuntor" percursos para que outras tentativas falhem imediatamente. (Se um grande número de solicitações estiver falhando, isso sugere que o serviço não está disponível e que o envio de solicitações é inútil.) Após um período de tempo limite, o cliente deve tentar novamente e, se as novas solicitações forem bem-sucedidas, feche o disjuntor.

**Fornecer fallbacks**. Nessa abordagem, o processo de cliente executa a lógica de fallback quando uma solicitação falha, como retornar dados armazenados em cache ou um valor padrão. Essa é uma abordagem adequada para consultas e é mais complexa para atualizações ou comandos.

**Limitar o número de solicitações na fila**. Os clientes também devem impor um limite superior no número de solicitações pendentes que um microsserviço cliente pode enviar para um serviço específico. Se o limite for atingido, provavelmente será ineficaz fazer mais solicitações. As tentativas falharão imediatamente. Em termos de implementação, a política [Isolamento do bulkhead](https://github.com/App-vNext/Polly/wiki/Bulkhead) da Polly pode ser usada para atender a esse requisito. Essa abordagem é essencialmente uma restrição de paralelização com <xref:System.Threading.SemaphoreSlim> como a implementação. Ela também permite uma "fila" fora do bulkhead. É possível lançar proativamente uma carga excessiva mesmo antes da execução (por exemplo, devido à capacidade ser considerada cheia). Isso torna sua resposta a determinados cenários de falha mais rápida do que um disjuntor seria, uma vez que o disjuntor aguarda as falhas. O objeto BulkheadPolicy na [Polly](https://thepollyproject.azurewebsites.net/) expõe se o bulkhead e a fila estão cheios e oferece eventos em estouro, portanto, ele também pode ser usado para permitir a escala horizontal automatizada.

## <a name="additional-resources"></a>Recursos adicionais

- **Padrões de resiliência**\
  [https://docs.microsoft.com/azure/architecture/patterns/category/resiliency](/azure/architecture/patterns/category/resiliency)

- **Adicionando resiliência e otimizando o desempenho**\
  <https://docs.microsoft.com/previous-versions/msp-n-p/jj591574(v=pandp.10)>

- **Bulkhead.** Repositório do GitHub. Implementação com a política Polly.\
  <https://github.com/App-vNext/Polly/wiki/Bulkhead>

- **Criando aplicativos resilientes para o Azure**\
  [https://docs.microsoft.com/azure/architecture/resiliency/](/azure/architecture/resiliency/)

- **Tratamento de falhas transitórias**\
  [https://docs.microsoft.com/azure/architecture/best-practices/transient-faults](/azure/architecture/best-practices/transient-faults)

>[!div class="step-by-step"]
>[Anterior](handle-partial-failure.md) 
> [Avançar](implement-retries-exponential-backoff.md)
