---
title: 'NETSDK1079: o pacote Microsoft. AspNetCore. All não tem suporte ao direcionar o .NET Core 3,0 ou superior.'
description: Como resolver a migração para fora do Microsoft. AspNetCore. app
author: dsplaisted
ms.topic: error-reference
ms.date: 10/09/2020
f1_keywords:
- NETSDK1079
ms.openlocfilehash: e0b7aba909dbd2931f755238a2de2418d294751d
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94445743"
---
# <a name="netsdk1079-the-microsoftaspnetcoreall-package-is-not-supported-when-targeting-net-core-30-or-higher"></a>NETSDK1079: o pacote Microsoft. AspNetCore. All não tem suporte ao direcionar o .NET Core 3,0 ou superior.

**Este artigo aplica-se a:** ✔️ SDK do .NET Core 3.1.100 e versões posteriores

Você pode receber essa mensagem de erro quando:

- Redirecione um projeto ASP.NET Core do .NET Core 2,2 ou anterior para o .NET Core 3,0 ou posterior.
- O projeto usa o pacote Microsoft. AspNetCore. All.

Remova o `PackageReference` para Microsoft. AspNetCore. All.  Talvez você também precise adicionar referências de pacote para pacotes que foram referenciados de Microsoft. AspNetCore. All, mas não estão incluídos na estrutura compartilhada ASP.NET Core.  Esses pacotes estão listados aqui: [migrando do Microsoft. AspNetCore. All para Microsoft. AspNetCore. app](/aspnet/core/fundamentals/metapackage#migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp).

Consulte também [migrar de ASP.NET Core 2,2 para 3,0](/aspnet/core/migration/22-to-30)
