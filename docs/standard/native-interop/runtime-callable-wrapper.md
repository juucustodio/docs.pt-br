---
title: RCW (Runtime Callable Wrapper)
description: O CLR expõe objetos COM por meio de um wrapper chamado de Runtime, que gerencia chamadas entre um cliente .NET e um objeto COM.
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, COM wrappers
- RCW
- COM wrappers
- runtime callable wrappers
- interoperation with unmanaged code, COM wrappers
ms.assetid: 7e542583-1e31-4e10-b523-8cf2f29cb4a4
ms.openlocfilehash: 985f6e5057a06ac9dcadc0e2c1e4d7743d96f035
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730221"
---
# <a name="runtime-callable-wrapper"></a>RCW (Runtime Callable Wrapper)

O common language runtime expõe objetos COM através de um proxy chamado RCW (Runtime Callable Wrapper). Embora o RCW pareça ser um objeto comum para clientes .NET, a função principal dele é realizar marshaling de chamadas entre um cliente .NET e um objeto COM.  
  
 O runtime cria exatamente um RCW para cada objeto COM, independentemente do número de referências que existem nesse objeto. O runtime mantém um único RCW por processo para cada objeto.  Se você criar um RCW em um domínio de aplicativo ou apartment e, em seguida, passar uma referência a outro domínio de aplicativo ou apartment, um proxy para o primeiro objeto será usado.  Conforme mostra a ilustração a seguir, qualquer número de clientes pode conter uma referência a objetos COM que expõem interfaces INew e INewer.  

A seguinte imagem mostra o processo para acessar objetos COM por meio do RCW (Runtime Callable Wrapper):

 ![Processo para acessar objetos COM por meio do RCW.](./media/runtime-callable-wrapper/runtime-callable-wrapper.gif)  

 Usando metadados derivados de uma biblioteca de tipos, o runtime cria o objeto COM que está sendo chamado e um wrapper para esse objeto. Cada RCW mantém um cache de ponteiros de interface no objeto COM que ele encapsula e, além disso, libera sua referência no objeto COM quando o RCW não é mais necessário. O runtime executa a coleta de lixo no RCW.  
  
 Entre outras atividades, o RCW realiza marshaling de dados entre código gerenciado e não gerenciado, em nome do objeto encapsulado. Especificamente, o RCW fornece marshaling para argumentos de método e valores retornados do método sempre que o cliente e o servidor têm representações diferentes dos dados transmitidos entre eles.  
  
 O wrapper padrão impõe regras de marshaling internas. Por exemplo, quando um cliente .NET passa um tipo de cadeia de caracteres como parte de um argumento para um objeto não gerenciado, o wrapper converte a cadeia de caracteres em um tipo BSTR. Se o objeto COM retornar um BSTR ao chamador gerenciado, o chamador receberá uma cadeia de caracteres. Tanto o cliente quanto o servidor enviam e recebem dados com os quais estão familiarizados. Outros tipos não exigem conversão. Por exemplo, um wrapper padrão sempre passará um inteiro de 4 bytes entre código gerenciado e não gerenciado sem converter o tipo.  
  
## <a name="marshaling-selected-interfaces"></a>Marshaling de interfaces selecionadas  

 A meta principal do [RCW](runtime-callable-wrapper.md) (Runtime Callable Wrapper) é ocultar as diferenças entre os modelos de programação gerenciado e não gerenciado. Para criar uma transição suave, o RCW consome interfaces COM selecionadas sem expô-las ao cliente .NET, conforme mostrado na ilustração a seguir.

 A seguinte imagem mostra as interfaces COM e o RCW (Runtime Callable Wrapper):
  
 ![Captura de tela do RCW (Runtime Callable Wrapper) com interfaces.](./media/runtime-callable-wrapper/runtime-callable-wrapper-interfaces.gif)  
  
 Quando criado como um objeto associado precocemente, o RCW é um tipo específico. Ele implementa as interfaces que o objeto COM implementa e expõe os métodos, propriedades e eventos das interfaces do objeto. Na ilustração, o RCW expõe a interface INew mas consome as interfaces **IUnknown** e **IDispatch**. Além disso, o RCW expõe todos os membros da interface INew para o cliente .NET.  
  
 O RCW consome as interfaces listadas na tabela a seguir, as quais são expostas pelo objeto que ele encapsula.  
  
|Interface|Descrição|  
|---------------|-----------------|  
|**IDispatch**|Para associação tardia a objetos COM por meio de reflexão.|  
|**IErrorInfo**|Fornece uma descrição textual do erro, sua origem, um arquivo de Ajuda, um contexto de Ajuda e o GUID da interface que definiu o erro (sempre **GUID_NULL** para classes do .NET).|  
|**IProvideClassInfo**|Se o objeto COM sendo empacotado implementa **IProvideClassInfo**, o RCW extrai as informações de tipo dessa interface para fornecer uma melhor identidade de tipo.|  
|**IUnknown**|Para gerenciamento do tempo de vida, coerção de tipo e identidade de objeto:<br /><br /> – Identidade de objeto<br />     O runtime faz distinção entre os objetos COM, comparando o valor da interface **IUnknown** para cada objeto.<br />– Coerção de tipo<br />     O RCW reconhece a descoberta de tipo dinâmico executada pelo método **QueryInterface**.<br />– Gerenciamento do tempo de vida<br />     Usando o **QueryInterface** método RCW obtém e mantém uma referência a um objeto não gerenciado até o runtime executar a coleta de lixo no wrapper, que libera o objeto não gerenciado.|  
  
 O RCW, opcionalmente, consome as interfaces listadas na tabela a seguir, as quais são expostas pelo objeto que ele encapsula.  
  
|Interface|Descrição|  
|---------------|-----------------|  
|**IConnectionPoint** e **IConnectionPointContainer**|O RCW converte objetos que expõem o estilo do evento de ponto de conexão para eventos com base em delegado.|  
|**IDispatchEx** (somente .NET Framework) |Se a classe implementa **IDispatchEx**, o RCW implementa **IExpando**. A interface **IDispatchEx** é uma extensão da interface **IDispatch** que, ao contrário de **IDispatch**, permite a enumeração, adição, exclusão e chamada de membros que diferencia maiúsculas de minúsculas.|  
|**IEnumVARIANT**|Permite que os tipos COM que dão suporte a enumerações sejam tratados como coleções.|  
  
## <a name="see-also"></a>Confira também

- [Wrappers COM](com-wrappers.md)
- [COM Callable Wrapper](com-callable-wrapper.md)
- [Resumo da conversão de bibliotecas de tipos em assemblies](/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))
- [Importando uma biblioteca de tipos como um assembly](../../framework/interop/importing-a-type-library-as-an-assembly.md)
