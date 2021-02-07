---
description: 'Saiba mais sobre: visão geral de segurança'
title: Visão geral da segurança
ms.date: 03/30/2017
ms.assetid: 33e09965-61d5-48cc-9e8c-3b047cc4f194
ms.openlocfilehash: 3aa6e5cbe444e9cfc417d79defce7e89a2034f71
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718818"
---
# <a name="security-overview"></a>Visão geral da segurança

Proteger um aplicativo é um processo contínuo. Nunca haverá um ponto em que um desenvolvedor possa garantir que um aplicativo seja protegido contra todos os ataques, pois é impossível prever que tipos de ataques futuros novas tecnologias irão trazer. Por outro lado, apenas porque ninguém ainda descobriu (ou publicou) falhas de segurança em um sistema não significa que nenhum exista ou que possa existir. Você precisa planejar a segurança durante a fase de design do projeto, bem como planejar como a segurança será mantida durante o tempo de vida do aplicativo.

## <a name="design-for-security"></a>Design de segurança

 Um dos maiores problemas no desenvolvimento de aplicativos seguros é que a segurança é, com freqüência, uma prioridade, algo a ser implementado após a conclusão do código do projeto. A não criação de segurança em um aplicativo no início leva a aplicativos inseguros porque poucas idéias foram dadas ao que torna um aplicativo seguro.

 A implementação de segurança de último minuto leva a mais bugs, pois o software é interrompido sob as novas restrições ou precisa ser reescrito para acomodar a funcionalidade inesperada. Cada linha de código revisado contém a possibilidade de introduzir um novo bug. Por esse motivo, você deve considerar a segurança no início do processo de desenvolvimento para que possa prosseguir em conjunto com o desenvolvimento de novos recursos.

### <a name="threat-modeling"></a>Modelagem de ameaças

 Não é possível proteger um sistema contra ataques, a menos que você compreenda todos os ataques potenciais aos quais ele está exposto. O processo de avaliação de ameaças de segurança, chamado de *modelagem de ameaças*, é necessário para determinar a probabilidade e as ramificações de violações de segurança em seu aplicativo ADO.net.

 A modelagem de risco é composta de três etapas de alto nível: compreendendo a exibição do adversário, caracterizando a segurança do sistema e determinando as ameaças.

 A modelagem de ameaças é uma abordagem iterativa para avaliar vulnerabilidades em seu aplicativo para encontrar as que são mais perigosas porque expõem os dados mais confidenciais. Depois de identificar as vulnerabilidades, você as classifica em ordem de gravidade e cria um conjunto priorizado de contramedidas para combater as ameaças.

Para obter mais informações, consulte os seguintes recursos:

|Recurso|Descrição|
|--------------|-----------------|
|O site de [modelagem de ameaças](https://www.microsoft.com/securityengineering/sdl/threatmodeling) no portal de engenharia de segurança|Os recursos nesta página ajudarão você a entender o processo de modelagem de ameaças e a criar modelos de ameaças que você pode usar para proteger seus próprios aplicativos|

## <a name="the-principle-of-least-privilege"></a>O princípio de privilégios mínimos

 Ao projetar, criar e implantar seu aplicativo, você deve pressupor que seu aplicativo será atacado. Geralmente, esses ataques são provenientes de código mal-intencionado que é executado com as permissões do usuário que está executando o código. Outras podem se originar com código bem intencional que foi explorado por um invasor. Ao planejar a segurança, sempre presuma que o cenário de pior caso ocorrerá.

 Uma medida de contador que você pode empregar é tentar colocar o máximo possível de paredes em seu código executando com privilégios mínimos. O princípio de menos privilégios diz que qualquer privilégio concedido deve ser concedido à quantidade mínima de código necessária para a duração mais curta necessária para realizar o trabalho.

 A prática recomendada para a criação de aplicativos seguros é iniciar sem nenhuma permissão e, em seguida, adicionar as permissões mais estreitas para a tarefa específica que está sendo executada. Por outro lado, a partir de todas as permissões e, em seguida, a negação de pontos individuais leva a aplicativos inseguros que são difíceis de testar e manter, pois podem existir brechas de segurança de conceder, de forma não intencional, mais permissões do que o necessário.

Para obter mais informações sobre como proteger seus aplicativos, consulte os seguintes recursos:

|Recurso|Descrição|
|--------------|-----------------|
|[Protegendo aplicativos](/visualstudio/ide/securing-applications)|Contém links para tópicos de segurança geral. Também contém links para tópicos para proteger aplicativos distribuídos, aplicativos Web, aplicativos móveis e aplicativos de área de trabalho.|

## <a name="code-access-security-cas"></a>CAS (segurança de acesso ao código)

A CAS (segurança de acesso ao código) é um mecanismo que ajuda a limitar o acesso que o código tem a recursos e operações protegidos. No .NET Framework, o CAS executa as seguintes funções:

- Define permissões e conjuntos de permissões que representam o direito de acessar vários recursos do sistema.

- Permite que os administradores configurem a política de segurança associando conjuntos de permissões a grupos de código (grupos de código).

- Permite que o código solicite as permissões necessárias para ser executado, bem como as permissões que seriam úteis e especifica quais permissões o código nunca deve ter.

- Concede permissões a cada assembly que é carregado, com base nas permissões solicitadas pelo código e nas operações permitidas pela política de segurança.

- Permite que o código exija que seus chamadores tenham permissões específicas.

- Permite que o código exija que seus chamadores possuam uma assinatura digital, permitindo que somente os chamadores de uma determinada organização ou site chamem o código protegido.

- Impõe restrições no código em tempo de execução, comparando as permissões concedidas de cada chamador na pilha de chamadas para as permissões que os chamadores devem ter.

Para minimizar a quantidade de danos que podem ocorrer se um ataque for realizado com sucesso, escolha um contexto de segurança para seu código que conceda acesso apenas aos recursos de que ele precisa para realizar seu trabalho e não mais.

Para obter mais informações, consulte os seguintes recursos:

|Recurso|Descrição|
|--------------|-----------------|
|[Segurança de acesso do código e o ADO.NET](code-access-security.md)|Descreve as interações entre a segurança de acesso ao código, a segurança baseada em função e os ambientes parcialmente confiáveis da perspectiva de um aplicativo ADO.NET.|
|[Segurança de acesso do código](../../misc/code-access-security.md)|Contém links para tópicos adicionais que descrevem o CAS no .NET Framework.|

## <a name="database-security"></a>Segurança do Banco de Dados

O princípio de menos privilégios também se aplica à fonte de dados. Algumas diretrizes gerais para segurança de banco de dados incluem:

- Crie contas com os privilégios mais baixos possíveis.

- Não permita que os usuários acessem contas administrativas apenas para obter o código funcionando.

- Não retornar mensagens de erro do lado do servidor para aplicativos cliente.

- Valide todas as entradas no cliente e no servidor.

- Use comandos com parâmetros e evite instruções SQL dinâmicas.

- Habilite a auditoria de segurança e o log do banco de dados que você está usando para que você seja alertado sobre violações de segurança.

Para obter mais informações, consulte os seguintes recursos:

|Recurso|Descrição|
|--------------|-----------------|
|[Segurança do SQL Server](./sql/sql-server-security.md)|Fornece uma visão geral de SQL Server segurança com cenários de aplicativo que fornecem diretrizes para criar aplicativos ADO.NET seguros direcionados SQL Server.|
|[Recomendações para estratégias de acesso a dados](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))|Fornece recomendações para o acesso a dados e a execução de operações de Database.|

## <a name="security-policy-and-administration"></a>Política de segurança e administração

Administrar incorretamente a política de CAS (segurança de acesso do código) pode potencialmente criar pontos fracos de segurança. Depois que um aplicativo é implantado, as técnicas para segurança de monitoramento devem ser usadas e os riscos avaliados à medida que novas ameaças surgem.

Para obter mais informações, consulte os seguintes recursos:

|Recurso|Descrição|
|--------------|-----------------|
|[Gerenciamento de política de segurança](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))|Fornece informações sobre como criar e administrar a política de segurança.|
|[Práticas recomendadas de política de segurança](/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100))|Fornece links que descrevem como administrar a política de segurança.|

## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](securing-ado-net-applications.md)
- [Segurança no .NET](../../../standard/security/index.md)
- [Segurança do SQL Server](./sql/sql-server-security.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
