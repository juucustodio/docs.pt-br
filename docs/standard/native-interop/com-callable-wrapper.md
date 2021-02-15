---
title: COM Callable Wrapper
description: Quando um cliente COM chama um objeto .NET, o CLR cria o objeto gerenciado e um COM Callable Wrapper para ele. Os clientes COM chamam o wrapper para o objeto.
ms.date: 10/23/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CCW
- COM interop, COM wrappers
- COM wrappers
- callable wrappers
- interoperation with unmanaged code, COM wrappers
- COM callable wrappers
ms.assetid: d04be3b5-27b9-4f5b-8469-a44149fabf78
ms.openlocfilehash: cc27ba47c88d424a80eb47aaa310bdfd6d18433a
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187912"
---
# <a name="com-callable-wrapper"></a>COM Callable Wrapper

Quando um cliente COM chama um objeto .NET, o Common Language Runtime cria o objeto gerenciado e um CCW (COM Callable Wrapper) para o objeto. Se não é possível referenciar um objeto .NET diretamente, os clientes COM usam o CCW como um proxy do objeto gerenciado.

O runtime cria exatamente um CCW para um objeto gerenciado, independentemente do número de clientes COM que solicita seus serviços. Como mostra a ilustração a seguir, vários clientes COM podem conter uma referência ao CCW que expõe a interface INew. O CCW, por sua vez, contém uma única referência ao objeto gerenciado que implementa a interface e é coletada como lixo. Os clientes COM e .NET podem fazer solicitações no mesmo objeto gerenciado simultaneamente.

![Vários clientes COM que contêm uma referência ao CCW que expõe INew.](./media/com-callable-wrapper/com-callable-wrapper-clients.gif)

Os COM Callable Wrappers são invisíveis para outras classes em execução no runtime do .NET. Sua finalidade principal é realizar marshaling de chamadas entre o código gerenciado e não gerenciado; no entanto, os CCWs também gerenciam a identidade e o tempo de vida dos objetos gerenciados encapsulados por eles.

## <a name="object-identity"></a>Identidade do objeto

O runtime aloca memória para o objeto .NET em seu heap coletado como lixo, que permite ao runtime mover o objeto na memória, conforme necessário. Por outro lado, o runtime aloca memória para o CCW em um heap não coletado, possibilitando que os clientes COM referenciem o wrapper diretamente.

## <a name="object-lifetime"></a>Tempo de vida do objeto

Ao contrário do cliente .NET encapsulado por ele, o CCW é contado por referência no modo tradicional do COM. Quando a contagem de referência do CCW chega a zero, o wrapper libera sua referência no objeto gerenciado. Um objeto gerenciado sem referências restantes é coletado durante o próximo ciclo de coleta de lixo.

## <a name="simulating-com-interfaces"></a>Simulando Interfaces COM

O CCW expõe todas as interfaces públicas visíveis para o COM, os tipos de dados e os valores retornados para clientes COM de uma maneira consistente com a exigência do COM em relação à interação baseada em interface. Para um cliente COM, a invocação de métodos em um objeto .NET é idêntica à invocação de métodos em um objeto COM.

Para criar essa abordagem direta, o CCW fabrica interfaces COM tradicionais, como **IUnknown** e **IDispatch** . Como mostra a ilustração a seguir, o CCW mantém uma única referência no objeto .NET encapsulado por ele. O cliente COM e o objeto .NET interagem mutuamente por meio do proxy e da construção de stub do CCW.

![Diagrama que mostra como a CCW fabrica interfaces COM.](./media/com-callable-wrapper/com-callable-wrapper-interfaces.gif)

Além de expor as interfaces que são implementadas explicitamente por uma classe no ambiente gerenciado, o runtime do .NET fornece implementações das interfaces COM listadas na tabela a seguir em nome do objeto. Uma classe .NET pode substituir o comportamento padrão fornecendo sua própria implementação dessas interfaces. No entanto, o runtime sempre fornece a implementação para as interfaces **IUnknown** e **IDispatch** .

|Interface|Descrição|
|---------------|-----------------|
|**IDispatch**|Fornece um mecanismo de associação tardia ao tipo.|
|**IErrorInfo**|Fornece uma descrição textual do erro, sua origem, um arquivo de Ajuda, um contexto de Ajuda e o GUID da interface que definiu o erro (sempre **GUID_NULL** para classes do .NET).|
|**IProvideClassInfo**|Permite aos clientes COM obter acesso à interface **ITypeInfo** implementada por uma classe gerenciada. Retorna `COR_E_NOTSUPPORTED` no .NET Core para tipos não importados do COM. |
|**ISupportErrorInfo**|Permite a um cliente COM determinar se o objeto gerenciado dá suporte à interface **IErrorInfo** . Nesse caso, permite ao cliente obter um ponteiro para o último objeto de exceção. Todos os tipos gerenciados dão suporte à interface **IErrorInfo** .|
|**ITypeInfo** (somente .NET Framework)|Fornece informações de tipo de uma classe que são exatamente iguais às informações de tipo produzidas pelo Tlbexp.exe.|
|**IUnknown**|Fornece a implementação padrão da interface **IUnknown** com a qual o cliente COM gerencia o tempo de vida do CCW e fornece a coerção de tipo.|

 Uma classe gerenciada também pode fornecer as interfaces COM descritas na tabela a seguir.

|Interface|Descrição|
|---------------|-----------------|
|A interface de classe (\_*classname* )|Interface, exposta pelo runtime e não definida explicitamente, que expõe todas as interfaces públicas, métodos, propriedades e campos que são expostos explicitamente em um objeto gerenciado.|
|**IConnectionPoint** e **IConnectionPointContainer**|Interface para objetos que dão origem a eventos baseados em representante (uma interface para o registro de assinantes do evento).|
|**IDispatchEx** (somente .NET Framework)|Interface fornecida pelo runtime se a classe implementa **IExpando** . A interface **IDispatchEx** é uma extensão da interface **IDispatch** que, ao contrário de **IDispatch** , permite a enumeração, adição, exclusão e chamada de membros que diferencia maiúsculas de minúsculas.|
|**IEnumVARIANT**|Interface para classes de tipo de coleção, que enumera os objetos na coleção, se a classe implementa **IEnumerable** .|

## <a name="introducing-the-class-interface"></a>Introdução à interface de classe

A interface de classe, que não é definida explicitamente no código gerenciado, é uma interface que expõe todos os métodos públicos, propriedades, campos e eventos que são expostos explicitamente no objeto .NET. Essa interface pode ser uma interface dupla ou somente de expedição. A interface de classe recebe o nome da própria classe do .NET, precedido por um sublinhado. Por exemplo, para a classe Mammal, a interface de classe é \_Mammal.

Para classes derivadas, a interface de classe também expõe todos os métodos públicos, propriedades e campos da classe base. A classe derivada também expõe uma interface de classe para cada classe base. Por exemplo, se a classe Mammal estende a classe MammalSuperclass, que, por sua vez, estende System.Object, o objeto do .NET expõe para os clientes COM três interfaces de classe chamadas \_Mammal, \_MammalSuperclass e \_Object.

Por exemplo, considere a seguinte classe do .NET:

```vb
' Applies the ClassInterfaceAttribute to set the interface to dual.
<ClassInterface(ClassInterfaceType.AutoDual)> _
' Implicitly extends System.Object.
Public Class Mammal
    Sub Eat()
    Sub Breathe()
    Sub Sleep()
End Class
```

```csharp
// Applies the ClassInterfaceAttribute to set the interface to dual.
[ClassInterface(ClassInterfaceType.AutoDual)]
// Implicitly extends System.Object.
public class Mammal
{
    public void Eat() {}
    public void Breathe() {}
    public void Sleep() {}
}
```

O cliente COM pode obter um ponteiro para uma interface de classe chamada `_Mammal`. No .NET Framework, você pode usar a ferramenta [Exportador da Biblioteca de Tipos (Tlbexp.exe)](../../framework/tools/tlbexp-exe-type-library-exporter.md) para gerar uma biblioteca de tipos que contém a definição de interface `_Mammal`. Não há suporte para o Exportador da Biblioteca de Tipos no .NET Core. Se a classe `Mammal` tiver implementado uma ou mais interfaces, as interfaces aparecerão na coclass.

```console
[odl, uuid(…), hidden, dual, nonextensible, oleautomation]
interface _Mammal : IDispatch
{
    [id(0x00000000), propget] HRESULT ToString([out, retval] BSTR*
        pRetVal);
    [id(0x60020001)] HRESULT Equals([in] VARIANT obj, [out, retval]
        VARIANT_BOOL* pRetVal);
    [id(0x60020002)] HRESULT GetHashCode([out, retval] short* pRetVal);
    [id(0x60020003)] HRESULT GetType([out, retval] _Type** pRetVal);
    [id(0x6002000d)] HRESULT Eat();
    [id(0x6002000e)] HRESULT Breathe();
    [id(0x6002000f)] HRESULT Sleep();
}
[uuid(…)]
coclass Mammal
{
    [default] interface _Mammal;
}
```

A geração da interface de classe é opcional. Por padrão, a interoperabilidade COM gera uma interface somente de expedição para cada classe exportada para uma biblioteca de tipos. É possível impedir ou modificar a criação automática dessa interface aplicando o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> à classe. Embora a interface de classe possa facilitar a tarefa de exposição das classes gerenciadas ao COM, seus usos são limitados.

> [!CAUTION]
> O uso da interface de classe, em vez da definição explícita de sua própria, pode complicar o controle futuro de versão da classe gerenciada. Leia as diretrizes a seguir antes de usar a interface de classe.

### <a name="define-an-explicit-interface-for-com-clients-to-use-rather-than-generating-the-class-interface"></a>Defina uma interface explícita para uso dos clientes COM, em vez de gerar a interface de classe.

Como a interoperabilidade COM gera uma interface de classe automaticamente, alterações posteriores à versão na classe podem alterar o layout da interface de classe exposta pelo Common Language Runtime. Já que os clientes COM não estão normalmente preparados para manipular as alterações no layout de uma interface, eles são interrompidos se o layout de membro da classe é alterado.

Esta diretriz reforça a noção de que as interfaces expostas para os clientes COM devem permanecer inalteráveis. Para reduzir o risco de interromper os clientes COM reordenando inadvertidamente o layout da interface, isole todas as alterações na classe do layout da interface definindo interfaces explicitamente.

Use o **ClassInterfaceAttribute** para desativar a geração automática da interface de classe e implementar uma interface explícita para a classe, como mostra o seguinte fragmento de código:

```vb
<ClassInterface(ClassInterfaceType.None)>Public Class LoanApp
    Implements IExplicit
    Sub M() Implements IExplicit.M
…
End Class
```

```csharp
[ClassInterface(ClassInterfaceType.None)]
public class LoanApp : IExplicit
{
    int IExplicit.M() { return 0; }
}
```

O valor **ClassInterfaceType.None** impede que a interface de classe seja gerada quando os metadados da classe são exportados para uma biblioteca de tipos. No exemplo anterior, os clientes COM podem acessar a classe `LoanApp` somente pela interface `IExplicit`.

### <a name="avoid-caching-dispatch-identifiers-dispids"></a>Evitar o cache de identificadores de expedição (DispIds)

O uso da interface de classe é uma opção aceitável para os clientes com script, os clientes do Microsoft Visual Basic 6.0 ou qualquer cliente de associação tardia que não armazena em cache os DispIds dos membros da interface. Os DispIds identificam os membros da interface para habilitar a associação tardia.

Para a interface de classe, a geração dos DispIds se baseia na posição do membro na interface. Se você alterar a ordem do membro e exportar a classe para uma biblioteca de tipos, você alterará os DispIds gerados na interface de classe.

Para evitar a interrupção de clientes COM de associação tardia ao usar a interface de classe, aplique o **ClassInterfaceAttribute** ao valor **ClassInterfaceType.AutoDispatch** . Esse valor implementa uma interface de classe somente de expedição, mas omite a descrição da interface na biblioteca de tipos. Sem uma descrição da interface, os clientes não conseguem armazenar em cache os DispIds em tempo de compilação. Embora esse seja o tipo de interface padrão para a interface de classe, é possível aplicar o valor do atributo explicitamente.

```vb
<ClassInterface(ClassInterfaceType.AutoDispatch)> Public Class LoanApp
    Implements IAnother
    Sub M() Implements IAnother.M
…
End Class
```

```csharp
[ClassInterface(ClassInterfaceType.AutoDispatch)]
public class LoanApp
{
    public int M() { return 0; }
}
```

Para obter o DispId de um membro da interface em tempo de execução, os clientes COM podem chamar **IDispatch.GetIdsOfNames** . Para invocar um método na interface, passe o DispId retornado como um argumento para **IDispatch.Invoke** .

### <a name="restrict-using-the-dual-interface-option-for-the-class-interface"></a>Restrinja o uso da opção de interface dupla para a interface de classe.

Interfaces duplas permitem a associação inicial e tardia a membros da interface por clientes COM. Em tempo de design e durante o teste, talvez seja útil definir a interface de classe como dupla. Para uma classe gerenciada (e suas classes base) que nunca serão modificadas, essa opção também é aceitável. Em todos os outros casos, evite definir a interface de classe como dupla.

Uma interface dupla gerada automaticamente pode ser apropriada em casos raros. No entanto, com mais frequência, ela cria complexidade relacionada à versão. Por exemplo, os clientes COM que usam a interface de classe de uma classe derivada podem ser facilmente interrompidos com alterações na classe base. Quando um terceiro fornece a classe base, o layout da interface de classe fica fora de seu controle. Além disso, ao contrário de uma interface somente de expedição, uma interface dupla ( **ClassInterfaceType.AutoDual** ) fornece uma descrição da interface de classe na biblioteca de tipos exportada. Uma descrição como essa incentiva os clientes de associação tardia a armazenarem em cache os DispIds em tempo de compilação.

### <a name="ensure-that-all-com-event-notifications-are-late-bound"></a>Verifique se todas as notificações de evento COM têm associação tardia.

Por padrão, informações de tipo COM são incorporadas diretamente em assemblies gerenciados, o que elimina a necessidade de PIAS (assemblies de interoperabilidade primários). No entanto, uma das limitações das informações de tipo inseridas é que elas não são compatíveis com a entrega de notificações de eventos COM por chamadas early-bound (vtable), mas apenas com chamadas `IDispatch::Invoke` de associação tardia.

Se o seu aplicativo exigir chamadas early-bound para métodos de interface de eventos COM, defina a propriedade **Embed Interop Types** no Visual Studio como `true`, ou inclua o seguinte elemento no arquivo de projeto:

```xml
<EmbedInteropTypes>True</EmbedInteropTypes>
```

## <a name="see-also"></a>Confira também

- <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>
- [Wrappers COM](com-wrappers.md)
- [Expondo componentes do .NET Framework para COM](../../framework/interop/exposing-dotnet-components-to-com.md)
- [Como expor componentes do .NET Core ao COM](../../core/native-interop/expose-components-to-com.md)
- [Qualificando tipos do .NET para interoperação](qualify-net-types-for-interoperation.md)
- [RCW (Runtime Callable Wrapper)](runtime-callable-wrapper.md)
