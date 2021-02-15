---
title: Wrappers COM
description: Os clientes COM e os objetos .NET interagem usando um COM Callable Wrapper e um wrapper callable com tempo de execução. O CLR cria wrappers automaticamente.
ms.date: 03/30/2017
helpviewer_keywords:
- wrapper classes
- COM interop, COM wrappers
- COM wrappers
- COM, wrappers
- interoperation with unmanaged code, COM wrappers
- COM callable wrappers
ms.assetid: e56c485b-6b67-4345-8e66-fd21835a6092
ms.openlocfilehash: 17a303cde5fa51cd940b0375d2c6657fcd354dc5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706320"
---
# <a name="com-wrappers"></a>Wrappers COM

O COM difere do modelo de objeto de runtime do .NET de várias maneiras importantes:  
  
- Os clientes de objetos COM devem gerenciar o tempo de vida desses objetos; o Common Language Runtime gerencia o tempo de vida de objetos em seu ambiente.  
  
- Os clientes de objetos COM descobrem se um serviço está disponível solicitando uma interface que fornece esse serviço e recebendo um ponteiro de interface ou não. Os clientes de objetos .NET podem obter uma descrição da funcionalidade de um objeto usando a reflexão.  
  
- Os objetos .NET residem na memória gerenciada pelo ambiente de execução do runtime do .NET. O ambiente de execução pode mover objetos na memória por motivos de desempenho e atualizar todas as referências nos objetos movidos por ele. Os clientes não gerenciados, depois de obter um ponteiro para um objeto, dependem do objeto para permanecerem no mesmo local. Esses clientes não têm nenhum mecanismo para lidar com um objeto cujo local não é fixo.  
  
 Para superar essas diferenças, o runtime fornece classes wrapper para fazer com que os clientes gerenciados e não gerenciados acreditem que estão chamando objetos em seus respectivos ambientes. Sempre que o cliente gerenciado chama um método em um objeto COM, o tempo de execução cria um [RCW](runtime-callable-wrapper.md) (Runtime Callable Wrapper). Os RCWs eliminam as diferenças entre os mecanismos de referência gerenciada e não gerenciada, entre outras coisas. O runtime também cria um [CCW](com-callable-wrapper.md) (COM Callable Wrapper) para reverter o processo, permitindo que um cliente COM chame um método em um objeto .NET diretamente. Como mostra a ilustração a seguir, a perspectiva do código de chamada determina qual classe wrapper é criada pelo runtime.  
  
 ![Visão geral do wrapper COM](./media/com-wrappers/bidirectional-com-overview.gif)  
  
 Na maioria dos casos, o RCW (Runtime Callable Wrapper) padrão ou o CCW gerado pelo tempo de execução fornece o marshaling adequado para chamadas que cruzam o limite entre o COM e o tempo de execução do .NET. Usando atributos personalizados, opcionalmente, você pode ajustar a maneira como o runtime representa o código gerenciado e não gerenciado.  
  
## <a name="see-also"></a>Confira também

- [Interoperabilidade COM avançada no .NET Framework](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))
- [RCW (Runtime Callable Wrapper)](runtime-callable-wrapper.md)
- [COM Callable Wrapper](com-callable-wrapper.md)
- [Como personalizar wrappers padrão no .NET Framework](/previous-versions/dotnet/netframework-4.0/h7hx9abd(v=vs.100))
- [Como personalizar wrappers callable em tempo de execução no .NET Framework](/previous-versions/dotnet/netframework-4.0/56kh4hy7(v=vs.100))
