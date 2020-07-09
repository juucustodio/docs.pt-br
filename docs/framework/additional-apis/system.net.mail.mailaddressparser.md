---
title: Classe MailAddressParser (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Mail.MailAddressParser
- System.Net.Mail.MailAddressParser.ParseAddress
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: ff83f6946539fa262ccde980052627f98c75601d
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051344"
---
# <a name="mailaddressparser-class"></a><span data-ttu-id="95a04-102">Classe MailAddressParser</span><span class="sxs-lookup"><span data-stu-id="95a04-102">MailAddressParser class</span></span>

<span data-ttu-id="95a04-103">Analisa endereços de email conforme descrito em RFC 2822.</span><span class="sxs-lookup"><span data-stu-id="95a04-103">Parses email addresses as described in RFC 2822.</span></span> <span data-ttu-id="95a04-104">Esta classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="95a04-104">This class cannot be inherited.</span></span>

```csharp
internal static class MailAddressParser
```

> [!WARNING]
> <span data-ttu-id="95a04-105">Essa classe é interna e não deve ser usada diretamente no seu código.</span><span class="sxs-lookup"><span data-stu-id="95a04-105">This class is internal and is not meant to be used directly in your code.</span></span>
>
> <span data-ttu-id="95a04-106">A Microsoft não oferece suporte ao uso dessa classe em um aplicativo de produção em nenhuma circunstância.</span><span class="sxs-lookup"><span data-stu-id="95a04-106">Microsoft does not support the use of this class in a production application under any circumstance.</span></span>

## <a name="parseaddress-method"></a><span data-ttu-id="95a04-107">Método ParseAddress</span><span class="sxs-lookup"><span data-stu-id="95a04-107">ParseAddress method</span></span>

<span data-ttu-id="95a04-108">Analisa um único endereço de email da cadeia de caracteres especificada.</span><span class="sxs-lookup"><span data-stu-id="95a04-108">Parses a single email address from the specified string.</span></span>

```csharp
internal static MailAddress ParseAddress(string data)
```

### <a name="parameters"></a><span data-ttu-id="95a04-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="95a04-109">Parameters</span></span>

<span data-ttu-id="95a04-110">`data` <xref:System.String></span><span class="sxs-lookup"><span data-stu-id="95a04-110">`data` <xref:System.String></span></span>

<span data-ttu-id="95a04-111">A cadeia de caracteres que contém um endereço de email a ser analisado.</span><span class="sxs-lookup"><span data-stu-id="95a04-111">The string that contains an email address to be parsed.</span></span>

### <a name="return-value"></a><span data-ttu-id="95a04-112">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="95a04-112">Return value</span></span>

<xref:System.Net.Mail.MailAddress>

<span data-ttu-id="95a04-113">Um endereço de email válido.</span><span class="sxs-lookup"><span data-stu-id="95a04-113">A valid email address.</span></span>

### <a name="exceptions"></a><span data-ttu-id="95a04-114">Exceções</span><span class="sxs-lookup"><span data-stu-id="95a04-114">Exceptions</span></span>

<xref:System.FormatException?displayProperty=nameWithType>

<span data-ttu-id="95a04-115">O endereço de email é inválido.</span><span class="sxs-lookup"><span data-stu-id="95a04-115">The email address is invalid.</span></span>

## <a name="requirements"></a><span data-ttu-id="95a04-116">Requisitos</span><span class="sxs-lookup"><span data-stu-id="95a04-116">Requirements</span></span>

<span data-ttu-id="95a04-117">**Namespace:** <xref:System.Net></span><span class="sxs-lookup"><span data-stu-id="95a04-117">**Namespace:** <xref:System.Net></span></span>

<span data-ttu-id="95a04-118">**Assembly:** Sistema (em System.dll)</span><span class="sxs-lookup"><span data-stu-id="95a04-118">**Assembly:** System (in System.dll)</span></span>