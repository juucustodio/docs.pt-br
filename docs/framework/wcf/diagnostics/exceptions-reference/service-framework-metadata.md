---
description: 'Saiba mais sobre: metadados do Service Framework'
title: Metadados de estrutura de serviço
ms.date: 03/30/2017
ms.assetid: 76afc73a-0770-4084-93f3-6701a757911e
ms.openlocfilehash: d5443627e3bb4f15e0d7bc154e5735c7ef639320
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686200"
---
# <a name="service-framework-metadata"></a>Metadados de estrutura de serviço

Este tópico lista todas as exceções geradas pelos metadados do Service Framework.  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|AsyncEndCalledOnWrongChannel|Uma extremidade assíncrona foi chamada no canal errado.|  
|AsyncEndCalledWithAnIAsyncResult|Uma extremidade assíncrona foi chamada com um IAsyncResult de um método Begin diferente.|  
|AttemptedToGetContractTypeForButThatTypeIs1|Tentativa de obter o tipo de contrato para o especificado. O tipo não é um ServiceContract e não herda um ServiceContract.|  
|CannotHaveTwoOperationsWithTheSameName3|Não é possível ter duas operações no mesmo contrato com o mesmo nome. Os métodos especificados no tipo especificado violam essa regra. Altere o nome de uma das operações alterando o nome do método ou usando a propriedade Name de OperationContractAttribute.|  
|CannotInheritTwoOperationsWithTheSameName3|Não é possível herdar duas operações diferentes com o mesmo nome. A operação especificada dos contratos especificados viola essa regra. Altere o nome de uma das operações alterando o nome do método ou usando a propriedade Name de OperationContractAttribute.|  
|CantCreateChannelWithManualAddressing|Não é possível criar um canal para um contrato que requer uma solicitação/resposta e uma associação que requer endereçamento manual, mas só dá suporte à comunicação duplex.|  
|DuplicateBehavior1|O valor não pode ser adicionado à coleção. A coleção já contém um item do mesmo tipo especificado. Essa coleção dá suporte apenas a uma instância de cada tipo.|  
|InAContractInheritanceHierarchyIfParentHasCallbackChildMustToo|Como o contrato de serviço base especificado tem um contrato de retorno de chamada especificado, o contrato de serviço derivado especificado também deve especificar o tipo especificado ou um tipo derivado como seu contrato de retorno de chamada.|  
|InvalidAsyncBeginMethodSignatureForMethod2|Assinatura de método Begin assíncrona inválida para o método especificado no tipo de ServiceContract especificado. O método Begin deve usar AsyncCallback e um objeto como os dois últimos argumentos e retornar um IAsyncResult.|  
|InvalidAsyncEndMethodSignatureForMethod2|Assinatura de método final assíncrona inválida para o método especificado no tipo de ServiceContract especificado. O método End deve usar IAsyncResult como o último argumento.|  
|MessagePropertiesArraySize0|A matriz passada não tem espaço suficiente para conter todas as propriedades contidas nesta coleção.|  
|OneWayAndFaultsIncompatible2|O método especificado no tipo especificado é marcado como IsOneWay = true e declara um ou mais FaultContractAttributes. Métodos unidirecionais não podem declarar FaultContractAttributes. Altere IsOneWay para false ou remova FaultContractAttributes.|  
|UnsupportedWSDLOnlyOneMessage|Linguagem de descrição de serviços Web sem suporte. Somente uma parte de mensagem tem suporte para mensagens de falha. Essa mensagem de falha se refere a mais de uma parte da mensagem. Se você tiver acesso de edição ao arquivo de linguagem de descrição de serviços Web, poderá corrigir o problema removendo as partes de mensagem extras, de modo que a mensagem de falha faça referência a apenas uma parte.|  
|UnsupportedWSDLTheFault|Linguagem de descrição de serviços Web sem suporte. A parte da mensagem de falha deve fazer referência a um elemento. Essa mensagem de falha não se refere a um elemento. Se você tiver acesso de edição ao documento de linguagem de definição de serviços Web, poderá corrigir o problema referenciando um elemento de esquema usando o atributo ' element '.|  
|WsdlImportErrorDependencyDetail|Ocorreu um erro ao importar o especificado para o qual o outro valor especificado depende. O XPath também é especificado.|  
|XsdMissingRequiredAttribute1|Atributo necessário especificado ausente.|
