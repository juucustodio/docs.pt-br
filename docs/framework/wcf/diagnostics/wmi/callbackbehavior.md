---
description: 'Saiba mais sobre: CallbackBehavior'
title: CallbackBehavior
ms.date: 03/30/2017
ms.assetid: 42acd302-2b62-4849-a2d1-a03084343ecd
ms.openlocfilehash: fa9e403324afe818e247d1f751cce0ce7d5a6fb6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757755"
---
# <a name="callbackbehavior"></a>CallbackBehavior

CallbackBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class CallbackBehavior : Behavior  
{  
  boolean AutomaticSessionShutdown;  
  string ConcurrencyMode;  
  boolean IgnoreExtensionDataObject;  
  boolean IncludeExceptionDetailInFaults;  
  boolean MaxItemsInObjectGraph;  
  boolean UseSynchronizationContext;  
  boolean ValidateMustUnderstand;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe CallbackBehavior não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe CallbackBehavior tem as seguintes propriedades:  
  
### <a name="automaticsessionshutdown"></a>AutomaticSessionShutdown  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Quando true, a sessão é fechada automaticamente quando um serviço fecha uma sessão duplex.  
  
### <a name="concurrencymode"></a>ConcurrencyMode  

 Tipo de dados: cadeia de caracteres  
Tipo de acesso: Somente leitura  
  
 Especifica se o serviço dá suporte a um thread, vários threads ou chamadas reentrantes.  
  
### <a name="ignoreextensiondataobject"></a>IgnoreExtensionDataObject  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que especifica se os dados de serialização desconhecidos devem ser enviados para a conexão.  
  
### <a name="includeexceptiondetailinfaults"></a>IncludeExceptionDetailInFaults  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Quando habilitado, os detalhes sobre as exceções no retorno de chamada são anexados às falhas retornadas ao serviço.  
  
### <a name="maxitemsinobjectgraph"></a>MaxItemsInObjectGraph  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 O número máximo de itens permitidos em um objeto serializado.  
  
### <a name="usesynchronizationcontext"></a>UseSynchronizationContext  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se o contexto de sincronização atual deve ser usado para escolher o thread de execução.  
  
### <a name="validatemustunderstand"></a>ValidateMustUnderstand  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se o sistema ou o aplicativo impõe o processamento de cabeçalho MustUnderstand SOAP.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.CallbackBehaviorAttribute>
