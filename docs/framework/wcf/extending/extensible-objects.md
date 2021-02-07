---
description: 'Saiba mais sobre: objetos extensíveis'
title: Objetos extensíveis
ms.date: 03/30/2017
helpviewer_keywords:
- extensible objects [WCF]
ms.assetid: bc88cefc-31fb-428e-9447-6d20a7d452af
ms.openlocfilehash: 80082f4c94adf2d668ff4c241d286959d9a05038
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756689"
---
# <a name="extensible-objects"></a>Objetos extensíveis

O padrão de objeto extensível é usado para estender as classes de tempo de execução existentes com a nova funcionalidade ou para adicionar um novo estado a um objeto. Extensões, anexadas a um dos objetos extensíveis, habilitam comportamentos em estágios muito diferentes no processamento para acessar o estado compartilhado e a funcionalidade anexada a um objeto extensível comum que eles podem acessar.

## <a name="the-iextensibleobjectt-pattern"></a>O \<T> padrão IExtensibleObject

Há três interfaces no padrão de objeto extensível: <xref:System.ServiceModel.IExtensibleObject%601> , <xref:System.ServiceModel.IExtension%601> e <xref:System.ServiceModel.IExtensionCollection%601> .

A <xref:System.ServiceModel.IExtensibleObject%601> interface é implementada por tipos que permitem que os <xref:System.ServiceModel.IExtension%601> objetos personalizem sua funcionalidade.

Os objetos extensíveis permitem a agregação dinâmica de <xref:System.ServiceModel.IExtension%601> objetos. <xref:System.ServiceModel.IExtension%601> os objetos são caracterizados pela seguinte interface:

```csharp
public interface IExtension<T>
where T : IExtensibleObject<T>
{
    void Attach(T owner);
    void Detach(T owner);
}
```

A restrição de tipo garante que as extensões só possam ser definidas para classes que são <xref:System.ServiceModel.IExtensibleObject%601> . <xref:System.ServiceModel.IExtension%601.Attach%2A> e <xref:System.ServiceModel.IExtension%601.Detach%2A> fornecer notificação de agregação ou desagregação.

É válido para as implementações restringir quando podem ser adicionadas e removidas de um proprietário. Por exemplo, você pode desabilitar completamente a remoção, desautorizando a adição ou remoção de extensões quando o proprietário ou a extensão estão em um determinado Estado, não permitir a adição de vários proprietários simultaneamente ou permitir apenas uma única adição seguida de uma única remoção.

<xref:System.ServiceModel.IExtension%601> o não implica nenhuma interação com outras interfaces gerenciadas padrão. Especificamente, o <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> método no objeto do proprietário normalmente não desanexa suas extensões.

Quando uma extensão é adicionada à coleção, <xref:System.ServiceModel.IExtension%601.Attach%2A> é chamada antes de entrar na coleção. Quando uma extensão é removida da coleção, <xref:System.ServiceModel.IExtension%601.Detach%2A> é chamada após ela ser removida. Isso significa (supondo a sincronização apropriada) que uma extensão pode contar apenas na coleção, enquanto está entre <xref:System.ServiceModel.IExtension%601.Attach%2A> e <xref:System.ServiceModel.IExtension%601.Detach%2A> .

O objeto passado para <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> ou <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> não precisa ser <xref:System.ServiceModel.IExtension%601> (por exemplo, você pode passar qualquer objeto), mas a extensão retornada é um <xref:System.ServiceModel.IExtension%601> .

Se nenhuma extensão na coleção for um <xref:System.ServiceModel.IExtension%601> , <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> retornará NULL e <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> retornará uma coleção vazia. Se várias extensões implementarem <xref:System.ServiceModel.IExtension%601> , o <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> retornará um deles. O valor retornado de <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> é um instantâneo.

Há dois cenários principais. O primeiro cenário usa a <xref:System.ServiceModel.IExtensibleObject%601.Extensions%2A> propriedade como um dicionário baseado em tipo para inserir o estado em um objeto para permitir que outro componente o pesquise usando o tipo.

O segundo cenário usa as <xref:System.ServiceModel.IExtension%601.Attach%2A> <xref:System.ServiceModel.IExtension%601.Detach%2A> Propriedades e para permitir que um objeto participe de um comportamento personalizado, como o registro de eventos, a observação de transições de estado e assim por diante.

A <xref:System.ServiceModel.IExtensionCollection%601> interface é uma coleção dos <xref:System.ServiceModel.IExtension%601> objetos que permitem recuperar o <xref:System.ServiceModel.IExtension%601> por seu tipo. <xref:System.ServiceModel.IExtensionCollection%601.Find%2A?displayProperty=nameWithType> Retorna o objeto adicionado mais recentemente que é um <xref:System.ServiceModel.IExtension%601> desse tipo.

### <a name="extensible-objects-in-windows-communication-foundation"></a>Objetos extensíveis no Windows Communication Foundation

Há quatro objetos extensíveis no Windows Communication Foundation (WCF):

- <xref:System.ServiceModel.ServiceHostBase> – Essa é a classe base para o host do serviço.  As extensões dessa classe podem ser usadas para estender o comportamento da <xref:System.ServiceModel.ServiceHostBase> si mesma ou para armazenar o estado de cada serviço.

- <xref:System.ServiceModel.InstanceContext> – Essa classe conecta uma instância do tipo do serviço com o tempo de execução do serviço.  Ele contém informações sobre a instância, bem como uma referência à <xref:System.ServiceModel.InstanceContext> que está contida no <xref:System.ServiceModel.ServiceHostBase> . As extensões dessa classe podem ser usadas para estender o comportamento do <xref:System.ServiceModel.InstanceContext> ou para armazenar o estado de cada serviço.

- <xref:System.ServiceModel.OperationContext> – Essa classe representa as informações de operação que o tempo de execução coleta para cada operação.  Isso inclui informações como os cabeçalhos das mensagens recebidas, as propriedades da mensagem de entrada, a identidade de segurança de entrada e outras informações.  As extensões dessa classe podem estender o comportamento <xref:System.ServiceModel.OperationContext> ou armazenar o estado de cada operação.

- <xref:System.ServiceModel.IContextChannel> – Essa interface permite a inspeção de cada Estado para os canais e proxies criados pelo tempo de execução do WCF.  As extensões dessa classe podem estender o comportamento de <xref:System.ServiceModel.IClientChannel> ou podem usá-lo para armazenar o estado de cada canal.

O exemplo de código a seguir mostra o uso de uma extensão simples para rastrear <xref:System.ServiceModel.InstanceContext> objetos.

[!code-csharp[IInstanceContextInitializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/iinstancecontextinitializer/cs/initializer.cs#1)]

## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.IExtensibleObject%601>
- <xref:System.ServiceModel.IExtension%601>
- <xref:System.ServiceModel.IExtensionCollection%601>
