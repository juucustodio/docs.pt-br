---
ms.openlocfilehash: 15786e6c659a29c5089eee9c8ac365c55b22f7fb
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99531815"
---
| .NET Standard              | [1,0]  | [1.1]  | [1.2] | [1,3] | [1.4] | [1.5]              | [1.6]              | [2.0]               | [2.1] |
|----------------------------|--------|--------|-------|-------|-------|--------------------|--------------------|---------------------|---------------------
| .NET                       | 5.0    | 5.0    | 5.0   | 5.0   | 5.0   | 5.0                | 5.0                | 5.0                 | 5.0 |
| .NET Core                  | 1.0    | 1.0    | 1.0   | 1.0   | 1.0   | 1.0                | 1.0                | 2.0                 | 3.0 |
| .NET Framework <sup>1</sup>| 4.5    | 4.5    | 4.5.1 | 4.6   | 4.6.1 | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup>  | N/A<sup>3</sup> |
| Mono                       | 4.6    | 4.6    | 4.6   | 4.6   | 4.6   | 4.6                | 4.6                | 5.4                 | 6.4 |
| Xamarin.iOS                | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0               | 10.0               | 10.14               | 12.16 |
| Xamarin.Mac                | 3,0    | 3,0    | 3,0   | 3,0   | 3,0   | 3,0                | 3,0                | 3.8                 | 5.16 |
| Xamarin.Android            | 7.0    | 7.0    | 7.0   | 7.0   | 7.0   | 7.0                | 7.0                | 8.0                 | 10.0 |
| Plataforma Universal do Windows | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0.16299         | 10.0.16299         | 10.0.16299          | TBD |
| Unity                      | 2018.1 | 2018.1 | 2018.1| 2018.1| 2018.1| 2018.1             |  2018.1            | 2018.1              | TBD |

<sup>1 as versões listadas para .NET Framework se aplicam ao SDK do .NET Core 2,0 e às versões posteriores das ferramentas. As versões mais antigas usaram um mapeamento diferente para .NET Standard 1,5 e superior. Você pode [baixar ferramentas para o .NET Core Tools para visual studio 2015](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md) se não for possível atualizar para o visual Studio 2017 ou uma versão posterior.</sup>

<sup>2 as versões listadas aqui representam as regras que o NuGet usa para determinar se uma determinada biblioteca de .NET Standard é aplicável. Embora o NuGet considere .NET Framework 4.6.1 como suporte a .NET Standard 1,5 até 2,0, há vários problemas com o consumo de .NET Standard bibliotecas que foram criadas para essas versões de projetos .NET Framework 4.6.1. Para projetos .NET Framework que precisam usar essas bibliotecas, recomendamos que você atualize o projeto para o destino .NET Framework 4.7.2 ou superior.</sup>

<sup>3 .NET Framework não dá suporte a .NET Standard 2,1. Para obter mais informações, consulte o [anúncio do .NET Standard 2,1](https://devblogs.microsoft.com/dotnet/announcing-net-standard-2-1/).</sup>

- As colunas representam versões do .NET Standard. Cada célula de cabeçalho é um link para um documento que mostra quais APIs foram adicionadas a essa versão do .NET Standard.
- As linhas representam as diferentes implementações do .NET.
- O número de versão em cada célula indica a versão *mínima* da implementação de que você precisará para direcionar essa versão do .NET Standard.
- Para obter uma tabela interativa, consulte [Versões do .NET Standard](https://dotnet.microsoft.com/platform/dotnet-standard#versions).

[1,0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.0.md
[1.1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.1.md
[1.2]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.2.md
[1,3]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.3.md
[1.4]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.4.md
[1.5]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.5.md
[1.6]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.6.md
[2.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md
[2.1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.1.md
