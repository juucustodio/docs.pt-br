---
title: Alterações da falha e bibliotecas do .NET
description: Práticas recomendadas para navegar por alterações da falha ao criar bibliotecas .NET.
ms.date: 10/02/2018
ms.openlocfilehash: 2cbd9e0a818b52aede6c9b1f60fdf52dcbd7b96f
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223325"
---
# <a name="breaking-changes"></a>Alterações da falha

É importante que uma biblioteca .NET encontre um equilíbrio entre a estabilidade para usuários existentes e a inovação para o futuro. Autores de biblioteca tendem a refatorar e repensar o código até que ele fique perfeito, mas causar falhas para seus usuários existentes tem um impacto negativo, especialmente para bibliotecas de baixo nível.

## <a name="project-types-and-breaking-changes"></a>Tipos de projeto e alterações da falha

O modo como uma biblioteca é usada pela comunidade do .NET altera o efeito das alterações de falha sobre os desenvolvedores para o usuário final.

- **Bibliotecas de nível médio e baixo**, tais como um serializador, analisador HTML, mapeador relacional de objeto de banco de dados ou estrutura da Web, são mais afetados por alterações da falha.

  Pacotes de blocos de construção são usados tanto por desenvolvedores para o usuário final, a fim de criar aplicativos, quanto por outras bibliotecas, como dependências do NuGet. Por exemplo, você está criando um aplicativo e usando um cliente de software livre para chamar um serviço Web. Uma atualização da falha para uma dependência que o cliente usa não é algo que você pode consertar. É o cliente de software livre que precisa ser alterado e você não tem controle sobre ele. Você precisa localizar as versões compatíveis das bibliotecas ou enviar uma correção para a biblioteca de clientes e aguardar uma nova versão. A pior situação é quando você deseja usar duas bibliotecas que dependem de versões mutuamente incompatíveis de uma biblioteca de terceiro.

- **Bibliotecas de alto nível**, tais como um pacote de controles de interface do usuário, são menos sensíveis a alterações da falha.

  Bibliotecas de alto nível são referenciadas diretamente em um aplicativo do usuário final. Se ocorrerem alterações da falha, o desenvolvedor poderá optar por atualizar para a versão mais recente ou poderá modificar seu aplicativo para funcionar com a alteração da falha.

✔️ PENSE em como sua biblioteca será usada. Que efeito as alterações da falha terão sobre aplicativos e bibliotecas que a usam?

✔️ MINIMIZE as alterações interruptivas ao desenvolver uma biblioteca do .NET de baixo nível.

✔️ CONSIDERE a possibilidade de publicar uma nova versão significativamente diferente da biblioteca como um novo pacote do NuGet.

## <a name="types-of-breaking-changes"></a>Tipos de alterações da falha

Alterações da falha se enquadram em categorias diferentes e não são igualmente impactantes.

### <a name="source-breaking-change"></a>Alteração da falha de origem

Uma alteração da falha de origem não afeta a execução do programa, mas causará erros de compilação na próxima vez que o aplicativo for recompilado. Por exemplo, uma nova sobrecarga pode criar ambiguidade em chamadas de método que antes estavam inequívocas ou um parâmetro renomeado interromperá os chamadores que usam parâmetros nomeados.

```csharp
public class Task
{
    // Adding a type called Task could conflict with System.Threading.Tasks.Task at compilation
}
```

Já que uma fonte de alteração da falha só é prejudicial quando os desenvolvedores recompilam seus aplicativos, ela a alteração da falha com menos interrupções. Os desenvolvedores podem consertar facilmente seu próprio código-fonte desfeito.

### <a name="behavior-breaking-change"></a>Alteração da falha de comportamento

Alterações de comportamento são o tipo mais comum de alteração da falha: quase qualquer alteração no comportamento poderia interromper alguém. Alterações na sua biblioteca, tais como assinaturas de método, exceções geradas ou formatos de dados de entrada ou saída, podem todas afetar negativamente seus consumidores de biblioteca. Até mesmo uma correção de bug pode se qualificar como uma alteração da falha se os usuários contavam com o comportamento anteriormente desfeito.

Adicionar recursos e melhorar maus comportamentos são uma coisa boa, mas fazê-lo sem cuidado pode dificultar muito o processo de atualização para os usuários existentes. Uma abordagem para ajudar os desenvolvedores a lidar com alterações da falha de comportamento é ocultá-las atrás de configurações. As configurações permitem que os desenvolvedores atualizem para a versão mais recente da sua biblioteca, optando simultaneamente por aceitar ou recusar alterações significativas. Essa estratégia permite que os desenvolvedores se mantenham atualizados, permitindo ao seu código de consumo adaptar-se ao longo do tempo.

Por exemplo, o ASP.NET Core MVC tem o conceito de uma [versão de compatibilidade](/aspnet/core/mvc/compatibility-version) que modifica os recursos habilitados e desabilitados em `MvcOptions`.

✔️ CONSIDERE a possibilidade de deixar novos recursos desativados por padrão se eles afetam os usuários existentes e permitir que os desenvolvedores escolham usar o recurso com uma configuração.

### <a name="binary-breaking-change"></a>Alteração da falha binária

Uma alteração da falha binária acontece quando você altera a API pública de sua biblioteca, portanto, os assemblies compilados para versões mais antigas da sua biblioteca não são mais capazes de chamar a API. Por exemplo, a alteração de assinatura de um método por meio da adição de um novo parâmetro fará com que assemblies compilados com a versão mais antiga da biblioteca lancem um <xref:System.MissingMethodException>.

Um alteração da falha binária também pode interromper um **assembly inteiro**. Renomear um assembly com `AssemblyName` alterará a identidade do assembly, o que também ocorrerá ao adicionar, remover ou alterar a chave de nomenclatura forte do assembly. Uma alteração da identidade de um assembly interromperá todo o código compilado que o utiliza.

❌ Não altere um nome de assembly.

❌ Não adicione, remova ou altere a chave de nomenclatura forte.

✔️ CONSIDERE a possibilidade de usar classes base abstratas em vez de interfaces.

> Adicionar qualquer coisa a uma interface fará com que os tipos existentes que a implementam falhem. Uma classe base abstrata permite que você adicione uma implementação de virtual padrão.

✔️ CONSIDERE a possibilidade de colocar o <xref:System.ObsoleteAttribute> nos tipos e membros que você pretende remover. O atributo deve ter instruções para atualizar o código para não usar mais a API obsoleta.

> Código que chamar tipos e métodos com o <xref:System.ObsoleteAttribute> gerará um aviso de build com a mensagem fornecida ao atributo. Os avisos dão, às pessoas que usam a superfície de API obsoleta, tempo para migrar, de modo que quando a API obsoleta é removida, a maioria já não está a usando mais.

```csharp
public class Document
{
    [Obsolete("LoadDocument(string) is obsolete. Use LoadDocument(Uri) instead.")]
    public static Document LoadDocument(string uri)
    {
        return LoadDocument(new Uri(uri));
    }

    public static Document LoadDocument(Uri uri)
    {
        // Load the document
    }
}
```

✔️ CONSIDERE a possibilidade de manter os tipos e métodos com o <xref:System.ObsoleteAttribute> indefinidamente em bibliotecas de nível médio e baixo.

> Remover APIs é uma alteração da falha binária. Considere a possibilidade de manter métodos e tipos obsoletos se mantê-los tem baixo custo e não adiciona muitas dívidas técnicas à sua biblioteca. Não remover tipos e métodos pode ajudar a evitar os piores cenários mencionados acima.

## <a name="see-also"></a>Confira também

- [Considerações sobre versão e atualização para os desenvolvedores de C#](../../csharp/whats-new/version-update-considerations.md)
- [Um guia definitivo para as alterações da falha de API no .NET](https://stackoverflow.com/questions/1456785/a-definitive-guide-to-api-breaking-changes-in-net)
- [Regras de alteração interruptiva do .NET](https://github.com/dotnet/runtime/blob/master/docs/coding-guidelines/breaking-change-rules.md)

>[!div class="step-by-step"]
>[Anterior](versioning.md)
