---
description: 'Saiba mais sobre: estendendo a hospedagem usando o ServiceHostFactory'
title: Estendendo a hospedagem com ServiceHostFactory
ms.date: 03/30/2017
ms.assetid: bcc5ae1b-21ce-4e0e-a184-17fad74a441e
ms.openlocfilehash: cd7749a153f23586bbf570eaf97f5ae849fc522d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735134"
---
# <a name="extending-hosting-using-servicehostfactory"></a>Estendendo a hospedagem com ServiceHostFactory

A <xref:System.ServiceModel.ServiceHost> API padrão para hospedar serviços no Windows Communication Foundation (WCF) é um ponto de extensibilidade na arquitetura do WCF. Os usuários podem derivar suas próprias classes de host do <xref:System.ServiceModel.ServiceHost> , geralmente para substituir <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening> para usar <xref:System.ServiceModel.Description.ServiceDescription> para adicionar pontos de extremidade padrão imperativos ou modificar comportamentos, antes de abrir o serviço.  
  
 No ambiente de hospedagem interna, você não precisa criar um personalizado <xref:System.ServiceModel.ServiceHost> porque escreve o código que instancia o host e, em seguida, chama-o <xref:System.ServiceModel.ICommunicationObject.Open> depois de instanciá-lo. Entre essas duas etapas, você pode fazer aquilo que desejar. Você pode, por exemplo, adicionar um novo <xref:System.ServiceModel.Description.IServiceBehavior> :  
  
```csharp
public static void Main()  
{  
   ServiceHost host = new ServiceHost( typeof( MyService ) );  
   host.Description.Add( new MyServiceBehavior() );  
   host.Open();  
  
   ...  
}  
```  
  
 Essa abordagem não é reutilizável. O código que manipula a descrição é codificado no programa de host (nesse caso, a função main ()), portanto, é difícil reutilizar essa lógica em outros contextos. Também há outras maneiras de adicionar um <xref:System.ServiceModel.Description.IServiceBehavior> que não exige código imperativo. Você pode derivar um atributo de <xref:System.ServiceModel.ServiceBehaviorAttribute> e colocá-lo em seu tipo de implementação de serviço ou pode tornar um comportamento personalizado configurável e Compose-lo dinamicamente usando a configuração.  
  
 No entanto, uma pequena variação do exemplo também pode ser usada para resolver esse problema. Uma abordagem é mover o código que adiciona o próprio comportamento de `Main()` e para o <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> método de um derivado personalizado de <xref:System.ServiceModel.ServiceHost> :  
  
```csharp
public class DerivedHost : ServiceHost  
{  
   public DerivedHost( Type t, params Uri baseAddresses ) :  
      base( t, baseAddresses ) {}  
  
   public override void OnOpening()  
   {  
  this.Description.Add( new MyServiceBehavior() );  
   }  
}  
```  
  
 Em seguida, dentro de `Main()` você pode usar:  
  
```csharp
public static void Main()  
{  
   ServiceHost host = new DerivedHost( typeof( MyService ) );  
   host.Open();  
  
   ...  
}  
```  
  
 Agora você encapsula a lógica personalizada em uma abstração limpa que pode ser facilmente reutilizada em vários executáveis de host diferentes.  
  
 Não é imediatamente óbvio como usar esse personalizado <xref:System.ServiceModel.ServiceHost> de dentro do serviços de informações da Internet (IIS) ou do WAS (serviço de ativação de processos do Windows). Esses ambientes são diferentes do ambiente de auto-host, pois o ambiente de hospedagem é o que instancia o <xref:System.ServiceModel.ServiceHost> em nome do aplicativo. A infraestrutura do IIS e do WAS de hospedagem não sabe nada sobre o seu <xref:System.ServiceModel.ServiceHost> derivado personalizado.  
  
 O <xref:System.ServiceModel.Activation.ServiceHostFactory> foi projetado para resolver esse problema de acesso ao seu personalizado <xref:System.ServiceModel.ServiceHost> de dentro do IIS ou was. Como um host personalizado derivado do <xref:System.ServiceModel.ServiceHost> é configurado dinamicamente e potencialmente de vários tipos, o ambiente de hospedagem nunca o instancia diretamente. Em vez disso, o WCF usa um padrão de fábrica para fornecer uma camada de indireção entre o ambiente de hospedagem e o tipo concreto do serviço. A menos que você diga ao contrário, ele usa uma implementação padrão do <xref:System.ServiceModel.Activation.ServiceHostFactory> que retorna uma instância do <xref:System.ServiceModel.ServiceHost> . Mas você também pode fornecer sua própria fábrica que retorna o host derivado especificando o nome do tipo CLR da sua implementação de fábrica na @ServiceHost diretiva.  
  
 A intenção é que, para os casos básicos, implementar sua própria fábrica deve ser um exercício direto. Por exemplo, aqui está um personalizado <xref:System.ServiceModel.Activation.ServiceHostFactory> que retorna uma derivada <xref:System.ServiceModel.ServiceHost> :  
  
```csharp
public class DerivedFactory : ServiceHostFactory  
{  
   public override ServiceHost CreateServiceHost( Type t, Uri[] baseAddresses )  
   {  
      return new DerivedHost( t, baseAddresses )  
   }  
}  
```  
  
 Para usar essa fábrica em vez da fábrica padrão, forneça o nome do tipo na @ServiceHost diretiva da seguinte maneira:  
  
`<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>`  
  
 Embora não haja nenhum limite técnico para fazer o que você deseja <xref:System.ServiceModel.ServiceHost> retornar <xref:System.ServiceModel.Activation.ServiceHostFactory.CreateServiceHost%2A> , sugerimos que você mantenha suas implementações de fábrica o mais simples possível. Se você tiver muita lógica personalizada, é melhor colocar essa lógica dentro do seu host, em vez de dentro da fábrica, para que ela possa ser reutilizável.  
  
 Há mais uma camada para a API de hospedagem que deve ser mencionada aqui. O WCF também tem <xref:System.ServiceModel.ServiceHostBase> e <xref:System.ServiceModel.Activation.ServiceHostFactoryBase> , de onde <xref:System.ServiceModel.ServiceHost> e <xref:System.ServiceModel.Activation.ServiceHostFactory> derivar, respectivamente. Existem para cenários mais avançados em que você deve trocar partes grandes do sistema de metadados por suas próprias criações personalizadas.
