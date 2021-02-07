---
description: 'Saiba mais sobre: ServiceBehaviorAttribute'
title: ServiceBehaviorAttribute
ms.date: 03/30/2017
ms.assetid: 5faa266f-587f-4e03-828d-1c7dd5acfe65
ms.openlocfilehash: 57ffa9103523618db752b3be6d43bb16603d1728
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715568"
---
# <a name="servicebehaviorattribute"></a>ServiceBehaviorAttribute

ServiceBehaviorAttribute  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceBehaviorAttribute : Behavior  
{  
  boolean AutomaticSessionShutdown;  
  string ConcurrencyMode;  
  string ConfigurationName;  
  boolean IgnoreExtensionDataObject;  
  boolean IncludeExceptionDetailInFaults;  
  string InstanceContextMode;  
  sint32 MaxItemsInObjectGraph;  
  string Name;  
  string Namespace;  
  boolean ReleaseServiceInstanceOnTransactionComplete;  
  boolean TransactionAutoCompleteOnSessionClose;  
  string TransactionIsolationLevel;  
  datetime TransactionTimeout;  
  boolean UseSynchronizationContext;  
  boolean ValidateMustUnderstand;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceBehaviorAttribute não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceBehaviorAttribute tem as seguintes propriedades:  
  
### <a name="automaticsessionshutdown"></a>AutomaticSessionShutdown  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Indica se uma sessão será fechada automaticamente quando um cliente fechar uma sessão de saída.  
  
### <a name="concurrencymode"></a>ConcurrencyMode  

 Tipo de dados: cadeia de caracteres  
Tipo de acesso: Somente leitura  
  
 Indica se um serviço dá suporte a um thread, a vários threads ou a chamadas reentrantes.  
  
### <a name="configurationname"></a>ConfigurationName  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome da configuração do serviço.  
  
### <a name="ignoreextensiondataobject"></a>IgnoreExtensionDataObject  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se é para enviar dados de serialização desconhecidos para a conexão.  
  
### <a name="includeexceptiondetailinfaults"></a>IncludeExceptionDetailInFaults  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se as informações de exceção gerenciadas devem ser incluídas nos detalhes de falhas de SOAP retornadas aos clientes para fins de depuração.  
  
### <a name="instancecontextmode"></a>InstanceContextMode  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Especifica quando um novo objeto de serviço é criado.  
  
### <a name="maxitemsinobjectgraph"></a>MaxItemsInObjectGraph  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de itens permitidos em um objeto serializado.  
  
### <a name="name"></a>Nome  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O atributo Name do serviço no WSDL.  
  
### <a name="namespace"></a>Namespace  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O namespace de destino do serviço no WSDL.  
  
### <a name="releaseserviceinstanceontransactioncomplete"></a>ReleaseServiceInstanceOnTransactionComplete  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se o objeto de serviço é reciclado quando a transação atual é concluída.  
  
### <a name="transactionautocompleteonsessionclose"></a>TransactionAutoCompleteOnSessionClose  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se as transações pendentes são concluídas quando a sessão atual é fechada.  
  
### <a name="transactionisolationlevel"></a>TransactionIsolationLevel  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Especifica o nível de isolamento da transação.  
  
### <a name="transactiontimeout"></a>TransactionTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O período no qual uma transação deve ser concluída.  
  
### <a name="usesynchronizationcontext"></a>UseSynchronizationContext  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se o contexto de sincronização atual deve ser usado para escolher a execução do thread.  
  
### <a name="validatemustunderstand"></a>ValidateMustUnderstand  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se o sistema ou o aplicativo impõe o processamento de cabeçalho MustUnderstand SOAP.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.ServiceBehaviorAttribute>
