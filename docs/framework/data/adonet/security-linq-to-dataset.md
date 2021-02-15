---
description: 'Saiba mais sobre: segurança (LINQ to DataSet)'
title: Segurança (LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: 6116b2b8-75f4-4d8b-aea6-c13e55cda50b
ms.openlocfilehash: 30a57980047e38ffca8af6ca5987517619ce0d45
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718844"
---
# <a name="security-linq-to-dataset"></a>Segurança (LINQ to DataSet)

Este tópico discute problemas de segurança no LINQ to DataSet.  
  
## <a name="passing-a-query-to-an-untrusted-component"></a>Passando uma consulta a um componente não confiável  

 Uma consulta LINQ to DataSet pode ser formulada em um ponto de um programa e executada em uma diferente. O ponto onde a consulta é formulada, a consulta pode fazer referência a qualquer elemento que está visível nesse ponto, como membros particulares da classe que o método de chamada pertence, ou de símbolos que representam variáveis locais/argumentos. Em tempo de execução, a consulta poderá efetivamente acessar os membros que foram referenciados pela consulta em formulação, mesmo se o código de chamada não tem a visibilidade neles. O código que executa a consulta não tem a visibilidade adicionada arbitrária, que não pode escolher o que acessar. Restrita poderá acessar o que a consulta acessa, e somente pela consulta própria.  
  
 Isso significa que passar uma referência a uma consulta para uma outra parte do código que o componente que recebe a consulta está sendo confiáveis com acesso a qualquer membros públicos e particulares que se refere a consulta. Em geral, LINQ to DataSet consultas não devem ser passadas para componentes não confiáveis, a menos que a consulta tenha sido cuidadosamente construída para que não exponha informações que devam ser mantidas privadas.  
  
## <a name="external-input"></a>Entrada externo  

 Os aplicativos geralmente têm externo (a entrada de um usuário ou outro agente externa) e executar ações com base na entrada.  No caso de LINQ to DataSet, o aplicativo pode construir uma consulta de uma determinada maneira, com base na entrada externa ou usar entrada externa na consulta. LINQ to DataSet consultas aceitam parâmetros em qualquer lugar que os literais são aceitos. Desenvolvedores de aplicativos devem usar consultas parametrizadas, em vez da o injetar literais de um agente externo diretamente na consulta.  
  
 Qualquer entrada direta ou indiretamente derivado de usuário ou um agente externa pode ter o conteúdo que aproveita a sintaxe de linguagem de destino para executar ações desautorizadas. Isso é conhecido como um ataque de injeção SQL, chamado depois que um padrão de ataque onde o idioma de destino é Transact-SQL. A entrada do usuário injetada diretamente na consulta é usada para soltar uma tabela de base de dados, causa uma negação de serviço, ou caso contrário alterar a natureza da operação que está sendo executada. Embora a composição de consulta seja possível em LINQ to DataSet, ela é executada por meio da API de modelo de objeto. LINQ to DataSet consultas não são compostas usando a manipulação ou a concatenação de cadeias de caracteres, pois elas estão no Transact-SQL e não são suscetíveis a ataques de injeção de SQL no sentido tradicional.  
  
## <a name="see-also"></a>Consulte também

- [Guia de programação](programming-guide-linq-to-dataset.md)
