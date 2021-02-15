---
ms.openlocfilehash: 3164233f1ac056de385faa119143d75d3c2dc50c
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224338"
---
> [!CAUTION]
> CAS (segurança de acesso a código) e código parcialmente confiável
>
> O .NET Framework fornece um mecanismo para a imposição de níveis variáveis de confiança em códigos diferentes em execução no mesmo aplicativo chamado CAS (Segurança de Acesso do Código).
>
> **Não há suporte para CAS no .NET Core, no .NET 5 ou em versões posteriores. Não há suporte para CAS em versões do C# posteriores a 7,0.**
>
> As CAS no .NET Framework não devem ser usadas como um mecanismo para impor limites de segurança com base na origem do código ou em outros aspectos de identidade. Não há suporte para CAS e código de Security-Transparent como um limite de segurança com código parcialmente confiável, especialmente código de origem desconhecida. Não aconselhamos carregar e executar códigos de origens desconhecidas sem a adoção de medidas de segurança alternativas no local. .NET Framework não emitirá patches de segurança para quaisquer explorações de elevação de privilégio que possam ser descobertas na área restrita do CAS.
>
> Essa política é aplicável à todas as versões do .NET Framework, mas não é aplicável ao .NET Framework incluído no Silverlight.
