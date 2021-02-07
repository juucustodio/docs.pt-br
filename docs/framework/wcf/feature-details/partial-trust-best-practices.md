---
description: 'Saiba mais sobre: práticas recomendadas de confiança parcial'
title: Práticas recomendadas de confiança parcial
ms.date: 03/30/2017
ms.assetid: 0d052bc0-5b98-4c50-8bb5-270cc8a8b145
ms.openlocfilehash: abdc0fbbb84581b302bca8d514a5f8f5cc2703e6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733548"
---
# <a name="partial-trust-best-practices"></a>Práticas recomendadas de confiança parcial

Este tópico descreve as práticas recomendadas ao executar o Windows Communication Foundation (WCF) em um ambiente de confiança parcial.

## <a name="serialization"></a>Serialização

Aplique as seguintes práticas ao usar o <xref:System.Runtime.Serialization.DataContractSerializer> em um aplicativo parcialmente confiável.

- Todos os tipos serializáveis devem ser marcados explicitamente com o `[DataContract]` atributo. Não há suporte para as seguintes técnicas em um ambiente de confiança parcial:

- Marcando classes a serem serializadas com o <xref:System.SerializableAttribute> .

- Implementar a <xref:System.Runtime.Serialization.ISerializable> interface para permitir que uma classe controle seu processo de serialização.

### <a name="using-datacontractserializer"></a>Usando o DataContractSerializer

- Todos os tipos marcados com o `[DataContract]` atributo devem ser públicos. Tipos não públicos não podem ser serializados em um ambiente de confiança parcial.

- Todos os `[DataContract]` Membros em um `[DataContract]` tipo serializável devem ser públicos. Um tipo com um não público `[DataMember]` não pode ser serializado em um ambiente de confiança parcial.

- Métodos que manipulam eventos de serialização (como `OnSerializing` ,, `OnSerialized` `OnDeserializing` e `OnDeserialized` ) devem ser declarados como públicos. No entanto, as implementações explícitas e implícitas do <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%28System.Object%29> têm suporte.

- `[DataContract]` os tipos implementados em assemblies marcados com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> não devem executar ações relacionadas à segurança no construtor de tipos, pois o <xref:System.Runtime.Serialization.DataContractSerializer> não chama o construtor do objeto instanciado recentemente durante a desserialização. Especificamente, as seguintes técnicas comuns de segurança devem ser evitadas para `[DataContract]` tipos:

- Tentativa de restringir o acesso de confiança parcial tornando o construtor do tipo interno ou privado.

- Restringindo o acesso ao tipo adicionando um `[LinkDemand]` ao construtor do tipo.

- Supondo que, como o objeto foi instanciado com êxito, todas as verificações de validação impostas pelo Construtor passaram com êxito.

### <a name="using-ixmlserializable"></a>Usando IXmlSerializable

As seguintes práticas recomendadas se aplicam a tipos que implementam <xref:System.Xml.Serialization.IXmlSerializable> e são serializados usando <xref:System.Runtime.Serialization.DataContractSerializer> :

- As <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> implementações do método estático devem ser `public` .

- Os métodos de instância que implementam a <xref:System.Xml.Serialization.IXmlSerializable> interface devem ser `public` .

## <a name="using-wcf-from-fully-trusted-platform-code-that-allows-calls-from-partially-trusted-callers"></a>Usando o WCF de Fully-Trusted código de plataforma que permite chamadas de chamadores parcialmente confiáveis

O modelo de segurança de confiança parcial do WCF pressupõe que qualquer chamador de um método público ou Propriedade do WCF esteja sendo executado no contexto de CAS (segurança de acesso do código) do aplicativo de hospedagem. O WCF também pressupõe que existe apenas um contexto de segurança de aplicativo para cada um <xref:System.AppDomain> , e que esse contexto é estabelecido no <xref:System.AppDomain> momento da criação por um host confiável (por exemplo, por uma chamada para <xref:System.AppDomain.CreateDomain%2A> ou pelo gerenciador de aplicativos ASP.net).

Esse modelo de segurança se aplica a aplicativos escritos pelo usuário que não podem declarar permissões de CAS adicionais, como o código do usuário em execução em um aplicativo ASP.NET de confiança média. No entanto, o código de plataforma totalmente confiável (por exemplo, um assembly de terceiros que é instalado no cache de assembly global e aceita chamadas de código parcialmente confiável) deve tomar um cuidado explícito ao chamar o WCF em nome de um aplicativo parcialmente confiável para evitar a introdução de vulnerabilidades de segurança no nível do aplicativo.

O código de confiança total deve evitar alterar o conjunto de permissões CAS do thread atual (chamando <xref:System.Security.PermissionSet.Assert%2A> , <xref:System.Security.PermissionSet.PermitOnly%2A> ou <xref:System.Security.PermissionSet.Deny%2A> ) antes de chamar as APIs do WCF em nome de código parcialmente confiável. A declaração, a negação ou a criação de um contexto de permissão específico do thread que seja independente do contexto de segurança no nível do aplicativo pode resultar em um comportamento inesperado. Dependendo do aplicativo, esse comportamento pode resultar em vulnerabilidades de segurança no nível do aplicativo.

O código que chama o WCF usando um contexto de permissão específico de thread deve estar preparado para lidar com as seguintes situações que podem ocorrer:

- O contexto de segurança específico do thread pode não ser mantido durante a operação, o que resulta em possíveis exceções de segurança.

- O código WCF interno, bem como qualquer retorno de chamada fornecido pelo usuário, pode ser executado em um contexto de segurança diferente daquele em que a chamada foi originalmente iniciada. Esses contextos incluem:

  - O contexto de permissão do aplicativo.

  - Qualquer contexto de permissão específico de thread criado anteriormente por outros threads de usuário usados para chamar o WCF durante o tempo de vida do em execução no momento <xref:System.AppDomain> .

O WCF garante que o código parcialmente confiável não possa obter permissões de confiança total, a menos que essas permissões sejam declaradas por um componente totalmente confiável antes de chamar as APIs públicas do WCF. No entanto, ele não garante que os efeitos da declaração de confiança total sejam isolados para um determinado thread, operação ou ação do usuário.

Como prática recomendada, Evite criar o contexto de permissão específico do thread chamando <xref:System.Security.PermissionSet.Assert%2A> , <xref:System.Security.PermissionSet.PermitOnly%2A> ou <xref:System.Security.PermissionSet.Deny%2A> . Em vez disso, conceda ou negue o privilégio ao próprio aplicativo, de modo que não <xref:System.Security.PermissionSet.Assert%2A> , <xref:System.Security.PermissionSet.Deny%2A> ou <xref:System.Security.PermissionSet.PermitOnly%2A> seja necessário.

## <a name="see-also"></a>Confira também

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.IXmlSerializable>
