---
description: 'Saiba mais sobre: tratamento de erro no Windows Communication Foundation (WCF)'
title: Tratamento de erros
ms.date: 03/30/2017
ms.assetid: c948841a-7db9-40ae-9b78-587d216cbcaf
ms.openlocfilehash: e09c07037e2b3398e2f82307242032a29c356ce5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704765"
---
# <a name="error-handling-in-windows-communication-foundation-wcf"></a>Tratamento de erro no Windows Communication Foundation (WCF)

Quando um serviço encontra uma exceção inesperada ou um erro, há várias maneiras de criar uma solução de manipulação de exceção. Embora não haja uma única solução de tratamento de erros "correta" ou "prática recomendada", há vários caminhos válidos a serem considerados. Normalmente, é recomendável que um implemente uma solução híbrida que combine várias abordagens da lista abaixo, dependendo da complexidade da implementação do WCF, do tipo e da frequência das exceções, da natureza manipulada versus sem tratamento das exceções e de quaisquer requisitos associados de rastreamento, registro ou política.

Essas soluções são explicadas mais profundamente no restante desta seção.

## <a name="the-microsoft-enterprise-library"></a>O Microsoft Enterprise Library

O bloco de aplicativos de tratamento de exceções do Microsoft Enterprise Library ajuda a implementar padrões de design comuns e a criar uma estratégia consistente para o processamento de exceções que ocorrem em todas as camadas de arquitetura de um aplicativo empresarial. Ele foi projetado para dar suporte ao código típico contido em instruções Catch em componentes de aplicativos. Em vez de repetir esse código (como código que registra informações de exceção) em blocos catch idênticos em um aplicativo, o bloco de aplicativo de tratamento de exceção permite aos desenvolvedores encapsular essa lógica como manipuladores de exceção reutilizáveis.

Essa biblioteca inclui um manipulador de exceção de contrato de falha pronto para uso. Esse manipulador de exceção é projetado para ser usado em limites de serviço WCF e gera um novo contrato de falha da exceção.

Os blocos de aplicativos visam incorporar as práticas recomendadas comumente usadas e fornecer uma abordagem comum para a manipulação de exceções em todo o seu aplicativo. Por outro lado, os manipuladores de erro personalizados e os contratos de falha desenvolvidos em um deles também podem ser muito úteis. Por exemplo, os manipuladores de erro personalizados fornecem uma excelente oportunidade para promover automaticamente todas as exceções para FaultExceptions e também para adicionar recursos de registro em log ao seu aplicativo.

Para obter mais informações, consulte [Microsoft Enterprise Library](/previous-versions/msp-n-p/ff632023(v=pandp.10)).

## <a name="dealing-with-expected-exceptions"></a>Lidando com exceções esperadas

O curso de ação apropriado é capturar as exceções esperadas em cada operação ou ponto de extensibilidade relevante, decidir se elas podem ser recuperadas e retornar a falha personalizada adequada em uma FaultException \<T> .
  
## <a name="dealing-with-unexpected-exceptions-using-an-ierrorhandler"></a>Lidando com exceções inesperadas usando um IErrorHandler

Para lidar com exceções inesperadas, o curso recomendado de ação é "conectar" um IErrorHandler. Os manipuladores de erro capturam exceções apenas no nível de tempo de execução do WCF (a camada "modelo de serviço"), não na camada de canal. A única maneira de conectar um IErrorHandler no nível de canal é criar um canal personalizado, que não é recomendado na maioria dos cenários.

Uma "exceção inesperada" geralmente não é uma exceção irrecuperável nem uma exceção de processamento; em vez disso, é uma exceção de usuário inesperada. Uma exceção irrecuperável (como uma exceção de memória insuficiente) – uma geralmente manipulada pelo [manipulador de exceção do modelo de serviço](xref:System.ServiceModel.Dispatcher.ExceptionHandler) , em geral, não pode ser manipulada normalmente, e o único motivo para tratar tal exceção pode ser fazer log adicional ou retornar uma exceção padrão ao cliente. Uma exceção de processamento ocorre no processamento da mensagem – por exemplo, no nível de serialização, codificador ou formatador – geralmente não pode ser tratada em um IErrorHandler, porque geralmente é muito cedo ou tarde demais para que o manipulador de erro interfira no momento em que essas exceções ocorrem. Da mesma forma, exceções de transporte não podem ser manipuladas em um IErrorHandler.

Com um IErrorHandler, você pode controlar explicitamente o comportamento do seu aplicativo quando uma exceção é gerada. Você pode:  

1. Decida se deseja ou não enviar uma falha ao cliente.

2. Substitua uma exceção por uma falha.

3. Substitua uma falha por outra falha.

4. Executar registro em log ou rastreamento.

5. Execute outras atividades personalizadas.

É possível instalar um manipulador de erro personalizado adicionando-o à propriedade ErrorHandlers dos distribuidores de canal para seu serviço.  É possível ter mais de um manipulador de erros e eles são chamados na ordem em que são adicionados a essa coleção.

IErrorHandler. ProvideFault controla a mensagem de falha que é enviada ao cliente. Esse método é chamado independentemente do tipo da exceção gerada por uma operação em seu serviço. Se nenhuma operação for executada aqui, o WCF assumirá seu comportamento padrão e continuará como se não houvesse nenhum manipulador de erro personalizado em vigor.

Uma área que você poderia usar essa abordagem é quando deseja criar um local central para converter exceções em falhas antes que elas sejam enviadas ao cliente (garantindo que a instância não seja descartada e o canal não seja movido para o estado com falha).

O método IErrorHandler. HandleError geralmente é usado para implementar comportamentos relacionados a erros, como log de erros, notificações do sistema, desligamento do aplicativo etc. IErrorHandler. HandleError pode ser chamado em vários locais dentro do serviço e, dependendo de onde o erro é gerado, o método HandleError pode ou não ser chamado pelo mesmo thread que a operação; nenhuma garantia é feita nesse aspecto.

## <a name="dealing-with-exceptions-outside-wcf"></a>Lidando com exceções fora do WCF

Muitas vezes, exceções de configuração, exceções de cadeia de conexão de banco de dados e outras exceções semelhantes podem ocorrer dentro do contexto de um aplicativo WCF, mas não são exceções causadas pelo modelo de serviço ou pelo próprio serviço Web. Essas exceções são exceções "regulares" externas ao serviço Web e devem ser manipuladas da mesma forma que outras exceções externas no ambiente devem ser tratadas.

## <a name="tracing-exceptions"></a>Exceções de rastreamento

O rastreamento é o único local "capturar tudo" onde um pode potencialmente ver todas as exceções. Para obter mais informações sobre rastreamento e log de exceções, consulte rastreamento e registro em log.

## <a name="uri-template-errors-when-using-webgetattribute-and-webinvokeattribute"></a>Erros de modelo de URI ao usar WebGetAttribute e WebInvokeAttribute

Os atributos WebGet e WebInvoke permitem que você especifique um modelo de URI que mapeia os componentes do endereço de solicitação para os parâmetros de operação. Por exemplo, o modelo de URI "clima/{State}/{City}" mapeia o endereço de solicitação em tokens literais, um parâmetro chamado State e um parâmetro chamado City. Esses parâmetros podem então ser associados por nome a alguns dos parâmetros formais da operação.

Os parâmetros de modelo aparecem na forma de cadeias de caracteres dentro do URI, enquanto os parâmetros formais de um contrato tipado podem ser de tipos que não são de cadeia de caracteres. Portanto, uma conversão precisa ocorrer antes que a operação possa ser chamada. Uma [tabela de formatos de conversão](wcf-web-http-programming-model-overview.md) está disponível.

No entanto, se a conversão falhar, não há como deixar a operação saber que algo deu errado. A conversão de tipo é, em vez disso, superfícies na forma de uma falha de expedição.

Uma falha de expedição de conversão de tipo pode ser inspecionada da mesma forma que com muitos outros tipos de falhas de expedição instalando um manipulador de erro. O ponto de extensibilidade IErrorHandler é chamado para manipular exceções de nível de serviço. A partir daí, a resposta a ser enviada de volta ao chamador – bem como a execução de tarefas e relatórios personalizados – pode ser escolhida.

## <a name="see-also"></a>Consulte também

- [Programação de WCF básica](../basic-wcf-programming.md)
