---
title: Configurar um servidor proxy ao usar o SDK do Azure para .NET
description: Usar HTTP [S] _PROXY variáveis de ambiente para definir um proxy para o SDK do Azure para .NET
ms.date: 12/10/2020
ms.topic: conceptual
ms.custom: devx-track-dotnet
ms.openlocfilehash: 64d525f8a6c277a5ac383dfded828f2fd3cfd744
ms.sourcegitcommit: 3d6d6595a03915f617349781f455f838a44b0f44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97701057"
---
# <a name="configure-a-proxy-server-when-using-the-azure-sdk-for-net"></a>Configurar um servidor proxy ao usar o SDK do Azure para .NET

Se sua organização exigir o uso de um servidor proxy para acessar recursos da Internet, será necessário definir uma variável de ambiente com as informações do servidor proxy para usar o SDK do Azure para .NET.  

## <a name="configuration-using-environment-variables"></a>Configuração usando variáveis de ambiente

Dependendo de se o servidor proxy usar HTTP ou HTTPS, você definirá a variável de ambiente `HTTP_PROXY` ou, `HTTPS_PROXY` respectivamente. A URL do servidor proxy tem o formato `http[s]://[username:password@]<ip_address_or_hostname>:<port>/` em que a `username:password` combinação é opcional. Para obter o endereço IP, o nome do host, a porta e as credenciais do servidor proxy, consulte o administrador da rede.

Os exemplos a seguir mostram como definir as variáveis de ambiente apropriadas em ambientes Shell de comando (Windows) e bash (Linux/Mac).  Definir a variável de ambiente apropriada fará com que o SDK do Azure para .NET use o servidor proxy em tempo de execução.

### <a name="cmd"></a>[cmd](#tab/cmd)

```cmd
rem Non-authenticated HTTP server:
set HTTP_PROXY=http://10.10.1.10:1180

rem Authenticated HTTP server:
set HTTP_PROXY=http://username:password@10.10.1.10:1180

rem Non-authenticated HTTPS server:
set HTTPS_PROXY=http://10.10.1.10:1180

rem Authenticated HTTPS server:
set HTTPS_PROXY=http://username:password@10.10.1.10:1180
```

### <a name="bash"></a>[Bash](#tab/bash)

```bash
# Non-authenticated HTTP server:
HTTP_PROXY=http://10.10.1.10:1180

# Authenticated HTTP server:
HTTP_PROXY=http://username:password@10.10.1.10:1180

# Non-authenticated HTTPS server:
HTTPS_PROXY=http://10.10.1.10:1180

# Authenticated HTTPS server:
HTTPS_PROXY=http://username:password@10.10.1.10:1180
```

---
