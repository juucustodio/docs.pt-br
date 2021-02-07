---
description: 'Saiba mais sobre: Associação'
title: Binding2
ms.date: 03/30/2017
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
ms.openlocfilehash: 36887a9296bfafd0790105e7f4d513efc3009bf8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757781"
---
# <a name="binding"></a>Associação

Associação WMI  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe de associação não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe de associação tem as propriedades a seguir.  
  
### <a name="bindingelements"></a>BindingElements  

 Tipo de dados: matriz BindingElement  
  
 Tipo de acesso: Somente leitura  
  
 A coleção de elementos de associação implementados pela associação.  
  
### <a name="closetimeout"></a>CloseTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O intervalo de tempo fornecido para a conclusão de uma operação de fechamento.  
  
### <a name="name"></a>Nome  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome da associação.  
  
### <a name="namespace"></a>Namespace  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O namespace XML da associação.  
  
### <a name="opentimeout"></a>OpenTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O intervalo de tempo fornecido para a conclusão de uma operação de abertura.  
  
### <a name="receivetimeout"></a>ReceiveTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O intervalo de tempo fornecido para a conclusão de uma operação de recebimento.  
  
### <a name="scheme"></a>Esquema  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O esquema de transporte de URI que é usado pelas fábricas de canal e ouvinte criadas pela associação.  
  
### <a name="sendtimeout"></a>SendTimeout  

 Tipo de dados: DateTime  
  
 Tipo de acesso: Somente leitura  
  
 O intervalo de tempo fornecido para a conclusão de uma operação de envio.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.Binding>
