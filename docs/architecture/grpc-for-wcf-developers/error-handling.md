---
title: Tratamento de erro-gRPC para desenvolvedores do WCF
description: A SER ESCRITO
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 3535a00aad49f532eb5f5f778116454a12bfd639
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184452"
---
# <a name="error-handling"></a><span data-ttu-id="89085-103">Tratamento de erros</span><span class="sxs-lookup"><span data-stu-id="89085-103">Error handling</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="89085-104">O WCF `FaultException<T>` usa `FaultContract` e para fornecer informações detalhadas de erro, incluindo suporte ao padrão de falha de SOAP.</span><span class="sxs-lookup"><span data-stu-id="89085-104">WCF uses `FaultException<T>` and `FaultContract` to provide detailed error information, including supporting the SOAP Fault standard.</span></span>

<span data-ttu-id="89085-105">Infelizmente, a versão atual do gRPC não tem a sofisticação encontrada com o WCF e só tem tratamento de erro interno limitado com base em códigos de status e metadados simples.</span><span class="sxs-lookup"><span data-stu-id="89085-105">Unfortunately, the current version of gRPC lacks the sophistication found with WCF and only has limited built-in error handling based on simple status codes and metadata.</span></span> <span data-ttu-id="89085-106">A tabela a seguir é um guia rápido para os códigos de status mais usados:</span><span class="sxs-lookup"><span data-stu-id="89085-106">The following table is a quick guide to the most commonly used status codes:</span></span>

| <span data-ttu-id="89085-107">Código de status</span><span class="sxs-lookup"><span data-stu-id="89085-107">Status Code</span></span> | <span data-ttu-id="89085-108">Problema</span><span class="sxs-lookup"><span data-stu-id="89085-108">Problem</span></span> |
| ----------- | ------- |
| `GRPC_STATUS_UNIMPLEMENTED` | <span data-ttu-id="89085-109">O método não foi gravado.</span><span class="sxs-lookup"><span data-stu-id="89085-109">Method hasn’t been written.</span></span> |
| `GRPC_STATUS_UNAVAILABLE` | <span data-ttu-id="89085-110">Problema com o serviço inteiro.</span><span class="sxs-lookup"><span data-stu-id="89085-110">Problem with the whole service.</span></span> |
| `GRPC_STATUS_UNKNOWN` | <span data-ttu-id="89085-111">Resposta inválida.</span><span class="sxs-lookup"><span data-stu-id="89085-111">Invalid response.</span></span> |
| `GRPC_STATUS_INTERNAL` | <span data-ttu-id="89085-112">Problema com codificação/decodificação.</span><span class="sxs-lookup"><span data-stu-id="89085-112">Problem with encoding/decoding.</span></span> |
| `GRPC_STATUS_UNAUTHENTICATED` | <span data-ttu-id="89085-113">Falha na autenticação.</span><span class="sxs-lookup"><span data-stu-id="89085-113">Authentication failed.</span></span> |
| `GRPC_STATUS_PERMISSION_DENIED` | <span data-ttu-id="89085-114">Falha na autorização.</span><span class="sxs-lookup"><span data-stu-id="89085-114">Authorization failed.</span></span> |
| `GRPC_STATUS_CANCELLED` | <span data-ttu-id="89085-115">A chamada foi cancelada, geralmente pelo chamador.</span><span class="sxs-lookup"><span data-stu-id="89085-115">Call was canceled, usually by the caller.</span></span> |

## <a name="raising-errors-in-aspnet-core-grpc"></a><span data-ttu-id="89085-116">Gerando erros no ASP.NET Core gRPC</span><span class="sxs-lookup"><span data-stu-id="89085-116">Raising errors in ASP.NET Core gRPC</span></span>

<span data-ttu-id="89085-117">Um serviço gRPC do ASP.NET Core pode enviar uma resposta de erro lançando um `RpcException`, que pode ser capturado pelo cliente como se estivesse no mesmo processo.</span><span class="sxs-lookup"><span data-stu-id="89085-117">An ASP.NET Core gRPC service can send an error response by throwing an `RpcException`, which can be caught by the client as if it were in the same process.</span></span> <span data-ttu-id="89085-118">O `RpcException` deve incluir um código de status e uma descrição e pode, opcionalmente, incluir metadados e uma mensagem de exceção mais longa.</span><span class="sxs-lookup"><span data-stu-id="89085-118">The `RpcException` must include a status code and description, and can optionally include metadata and a longer exception message.</span></span> <span data-ttu-id="89085-119">Os metadados podem ser usados para enviar dados de suporte, de forma `FaultContract` semelhante a como os objetos podem transportar dados adicionais para erros do WCF.</span><span class="sxs-lookup"><span data-stu-id="89085-119">The metadata can be used to send supporting data, similar to how `FaultContract` objects could carry additional data for WCF errors.</span></span>

```csharp
public async Task<GetPortfolioResponse> GetPortfolio(GetPortfolioRequest request, ServerCallContext context)
{
    var user = context.GetHttpContext().User;
    if (!ValidateUser(user))
    {
        var metadata = new Metadata
        {
            { "User", user.Identity.Name }
        };
        throw new RpcException(new Status(StatusCode.PermissionDenied, "Permission denied"), metadata);
    }
}
```

## <a name="catching-errors-in-grpc-clients"></a><span data-ttu-id="89085-120">Capturando erros em clientes gRPC</span><span class="sxs-lookup"><span data-stu-id="89085-120">Catching errors in gRPC clients</span></span>

<span data-ttu-id="89085-121">Assim como os clientes WCF podem <xref:System.ServiceModel.FaultException%601> capturar erros, um cliente gRPC pode capturar `RpcException` um para lidar com erros.</span><span class="sxs-lookup"><span data-stu-id="89085-121">Just like WCF clients can catch <xref:System.ServiceModel.FaultException%601> errors, a gRPC client can catch an `RpcException` to handle errors.</span></span> <span data-ttu-id="89085-122">Como `RpcException` não é um tipo genérico, você não pode capturar tipos de erro diferentes em blocos diferentes, mas C#você pode usar o recurso de filtros `catch` de *exceção* para declarar blocos separados para códigos de status diferentes, conforme mostrado a seguir exemplo</span><span class="sxs-lookup"><span data-stu-id="89085-122">Since `RpcException` isn't a generic type, you can't catch different error types in different blocks, but you can use C#'s *exception filters* feature to declare separate `catch` blocks for different status codes, as shown in the following example:</span></span>

```csharp
try
{
    var portfolio = await client.GetPortfolioAsync(new GetPortfolioRequest { Id = id });
}
catch (RpcException ex) when (ex.StatusCode == StatusCode.PermissionDenied)
{
    var userEntry = ex.Trailers.FirstOrDefault(e => e.Key == "User");
    Console.WriteLine($"User '{userEntry.Value}' does not have permission to view this portfolio.");
}
catch (RpcException) 
{
    // Handle any other error type ...
}
```

> [!IMPORTANT]
> <span data-ttu-id="89085-123">Ao fornecer metadados adicionais para erros, certifique-se de documentar as chaves e os valores relevantes na documentação da API ou em comentários em `.proto` seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="89085-123">When you provide additional metadata for errors, be sure to document the relevant keys and values in your API documentation, or in comments in your `.proto` file.</span></span>

## <a name="grpc-richer-error-model"></a><span data-ttu-id="89085-124">Modelo de erro gRPC mais rico</span><span class="sxs-lookup"><span data-stu-id="89085-124">gRPC Richer Error Model</span></span>

<span data-ttu-id="89085-125">Olhando adiante, o Google desenvolveu um [modelo de erro mais rico](https://cloud.google.com/apis/design/errors#error_model) que é mais parecido com o [FaultContract](xref:System.ServiceModel.FaultContractAttribute)do WCF, mas C# ainda não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="89085-125">Looking ahead, Google has developed a [richer error model](https://cloud.google.com/apis/design/errors#error_model) that is more like WCF's [FaultContract](xref:System.ServiceModel.FaultContractAttribute), but isn't supported in C# yet.</span></span> <span data-ttu-id="89085-126">Atualmente, ele está disponível apenas para go, Java, Python e C++, mas o suporte C# para é esperado no próximo ano.</span><span class="sxs-lookup"><span data-stu-id="89085-126">Currently, it's only available for Go, Java, Python and C++, but support for C# is expected to come next year.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="89085-127">[Anterior](metadata.md)
>[Próximo](ws-protocols.md)</span><span class="sxs-lookup"><span data-stu-id="89085-127">[Previous](metadata.md)
[Next](ws-protocols.md)</span></span>