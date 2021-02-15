---
description: 'Saiba mais sobre: segurança de SQL Server'
title: Segurança do SQL Server
ms.date: 03/30/2017
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.openlocfilehash: 73e5d72dfacb1f856056ba733c4ff06823ae08d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767200"
---
# <a name="sql-server-security"></a>Segurança do SQL Server

O SQL Server tem muitos recursos que oferecem suporte à criação de aplicativos de banco de dados seguros.  
  
 As considerações de segurança comuns são aplicáveis, como o roubo de dados ou o vandalismo, independentemente da versão do SQL Server que você está usando. A integridade dos dados também deve ser considerada um problema de segurança. Se os dados não estiverem protegidos, possivelmente se tornarão inúteis se a manipulação de dados ad hoc for permitida e os dados forem modificados inadvertida ou maliciosamente com valores incorretos ou excluídos inteiramente. Além disso, geralmente há requisitos legais que devem ser cumpridos, como o armazenamento correto de informações confidenciais. O armazenamento de alguns tipos de dados pessoais é totalmente prescrito, dependendo das leis aplicáveis em uma determinada jurisdição.  
  
 Cada versão do SQL Server tem recursos de segurança diferentes, assim como cada versão do Windows, com versões mais recentes que aprimoram a funcionalidade das mais antigas. É importante entender que os recursos de segurança sozinhos não podem garantir um aplicativo de banco de dados seguro. Cada aplicativo de banco de dados é único em seus requisitos, em seu ambiente de execução, em seu modelo de implantação, em sua localização física e em sua população de usuários. Alguns aplicativos com escopo local podem precisar somente de segurança mínima, enquanto outros aplicativos locais ou aplicativos implantados pela Internet podem exigir medidas de segurança rígidas e monitoramento e avaliação contínuos.  
  
 Os requisitos de segurança de um aplicativo de banco de dados do SQL Server devem ser considerados em tempo de design, não depois. A avaliação de ameaças no início do ciclo de desenvolvimento oferece a oportunidade de reduzir possíveis danos sempre que uma vulnerabilidade é detectada.  
  
 Mesmo se o projeto inicial de um aplicativo estiver correto, novas ameaças poderão surgir à medida que o sistema evoluir. Com a criação de várias linhas de defesa ao redor do seu banco de dados, você poderá minimizar os danos infligidos por uma violação de segurança. Sua primeira linha de defesa é reduzir a área da superfície de ataque nunca concedendo mais permissões do que o realmente necessário.  
  
 Os tópicos nesta seção descrevem resumidamente os recursos de segurança do SQL Server que são relevantes para os desenvolvedores, com links para tópicos relevantes nos Manuais Online do SQL Server e outros recursos que fornecem uma cobertura mais detalhada.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Visão geral de segurança do SQL Server](overview-of-sql-server-security.md)  
 Descreve a arquitetura e os recursos de segurança do SQL Server.  
  
 [Cenários de Segurança de Aplicativo no SQL Server](application-security-scenarios-in-sql-server.md)  
 Contém os tópicos que abordam vários cenários de segurança de aplicativos para o ADO.NET e aplicativos do SQL Server.  
  
 [Segurança de SQL Server Express](sql-server-express-security.md)  
 Descreve considerações de segurança para o SQL Server Express.  
  
## <a name="related-sections"></a>Seções relacionadas  

[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](/sql/relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database)  
Descreve as considerações de segurança para o SQL Server e o Banco de Dados SQL do Azure.

[Considerações sobre segurança para uma instalação do SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation)  
Descreve as preocupações de segurança a serem consideradas antes de instalar o SQL Server.

## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [SQL Server e ADO.NET](index.md)
