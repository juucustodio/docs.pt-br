---
title: Chamando uma função de DLL
description: Examine os problemas sobre como chamar uma função DLL que pode parecer confusa. O processo de chamada de função difere dependendo se o tipo de retorno é blittable.
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged functions, calling
- unmanaged functions
- COM interop, platform invoke
- platform invoke, calling unmanaged functions
- interoperation with unmanaged code, platform invoke
- DLL functions
ms.assetid: 113646de-7ea0-4f0e-8df0-c46dab3e8733
ms.openlocfilehash: 09dd9d30c29660231feee6c624a025ade1fda1d3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96282945"
---
# <a name="calling-a-dll-function"></a>Chamando uma função de DLL

Embora a chamada a funções de DLL não gerenciadas seja quase idêntica à chamada de outro código gerenciado, há diferenças que podem fazer com que as funções de DLL pareçam confusas a princípio. Esta seção apresenta tópicos que descrevem alguns dos problemas incomuns relacionados a chamadas.  
  
 Estruturas retornadas de chamadas de invocação de plataforma devem ser tipos de dados que têm a mesma representação em um código gerenciado e não gerenciado. Esses tipos são chamados de *tipos blittable* porque não exigem conversão (consulte [Tipos blittable e não blittable](blittable-and-non-blittable-types.md)). Para chamar uma função que tem uma estrutura não blittable como seu tipo de retorno, é possível definir um tipo de auxiliar blittable do mesmo tamanho do tipo não blittable e converter os dados depois que a função é retornada.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Passando estruturas](passing-structures.md)  
 Identifica os problemas de passar estruturas de dados com um layout predefinido.  
  
 [Funções de retorno de chamada](callback-functions.md)  
 Fornece informações básicas sobre as funções de retorno de chamada.  
  
 [Como: Implementar funções de retorno de chamada](how-to-implement-callback-functions.md)  
 Descreve como implementar funções de retorno de chamada em um código gerenciado.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Consumindo funções de DLL não gerenciadas](consuming-unmanaged-dll-functions.md)  
 Descreve como chamar funções de DLL não gerenciadas usando a invocação de plataforma.  
  
 [Marshaling de dados com invocação de plataforma](marshaling-data-with-platform-invoke.md)  
 Descreve como declarar parâmetros de método e passar argumentos para funções exportadas por bibliotecas não gerenciadas.
