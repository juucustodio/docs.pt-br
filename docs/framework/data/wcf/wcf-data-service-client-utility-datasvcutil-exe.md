---
description: 'Saiba mais sobre: utilitário cliente do WCF Data Service (DataSvcUtil.exe)'
title: Utilitário de cliente do WCF Data Service (DataSvcUtil.exe)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, generating client data classes
- WCF Data Services, client library
- WCF Data Services, consuming
ms.assetid: 9d0af606-929b-4c03-b307-3ef5f705afce
ms.openlocfilehash: 1e232538284072d82eed3f1b9e8d41f2ae950adf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791693"
---
# <a name="wcf-data-service-client-utility-datasvcutilexe"></a>Utilitário de cliente do WCF Data Service (DataSvcUtil.exe)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

DataSvcUtil.exe é uma ferramenta de linha de comando fornecida por WCF Data Services que consome um feed Protocolo Open Data (OData) e gera as classes de serviço de dados do cliente que são necessárias para acessar um serviço de dados de um aplicativo cliente .NET Framework. Esse utilitário pode gerar classes de dados usando as seguintes fontes de metadados:

- O URI raiz de um serviço de dados. O utilitário solicita o documento de metadados de serviço, que descreve o modelo de dados exposto pelo serviço de dados. Para obter mais informações, consulte [AtomPub (RFC5023)](https://tools.ietf.org/html/rfc5023#section-8).

- Um arquivo de modelo de dados (. CSDL) definido usando o CSDL (linguagem de definição de esquema conceitual), conforme definido na especificação de [ \[ formato de arquivo de definição de esquema MC-CSDL \] : conceitual](/openspecs/windows_protocols/mc-csdl/c03ad8c3-e8b7-4306-af96-a9e52bb3df12) .

- Um arquivo. edmx criado usando as ferramentas de Modelo de Dados de Entidade fornecidas com o Entity Framework. Para obter mais informações, consulte o [ \[ MC-EDMX \] : modelo de dados de entidade para especificação de formato de empacotamento de serviços de dados](/openspecs/windows_protocols/mc-edmx/5dff5e25-56a1-408b-9d44-bff6634c7d16) .

Para obter mais informações, consulte [como: gerar manualmente classes de serviço de dados do cliente](how-to-manually-generate-client-data-service-classes-wcf-data-services.md).

A ferramenta de DataSvcUtil.exe é instalada no diretório .NET Framework. Em muitos casos, isso está localizado em *C:\Windows\Microsoft.NET\Framework\v4.0*. Para sistemas de 64 bits, isso está localizado em *C:\Windows\Microsoft.NET\Framework64\v4.0*. Você também pode acessar a ferramenta de DataSvcUtil.exe do Prompt de Comando do Desenvolvedor para o Visual Studio.

## <a name="syntax"></a>Sintaxe

```console
datasvcutil /out:file [/in:file | /uri:serviceuri] [/dataservicecollection] [/language:devlang] [/nologo] [/version:ver] [/help]
```

## <a name="parameters"></a>parâmetros

|Opção|Descrição|
|------------|-----------------|
|`/dataservicecollection`|Especifica que o código necessário para associar objetos a controles também é gerado.|
|`/help`<br /><br /> -ou-<br /><br /> `/?`|Exibe sintaxe de comando e opções para a ferramenta.|
|`/in:` *\<file>*|Especifica o arquivo. CSDL ou. edmx ou um diretório onde o arquivo está localizado.|
|`/language:`[VB&#124;CSharp]|Especifica a linguagem dos arquivos de código-fonte gerados. A linguagem volta automaticamente para C#.|
|`/nologo`|Suprime a notificação de direitos autorais da exibição.|
|`/out:` *\<file>*|Especifica o nome do arquivo de código-fonte que contém as classes de serviço de dados do cliente geradas.|
|`/uri:` *\<string>*|O URI do feed OData.|
|`/version:`[1,0&#124;2,0]|Especifica a versão mais aceita do OData. A versão é determinada com base no `DataServiceVersion` atributo do elemento DataService nos metadados do serviço de dados retornados. Para obter mais informações, consulte [controle de versão do serviço de dados](data-service-versioning-wcf-data-services.md). Ao especificar o `/dataservicecollection` parâmetro, você também deve especificar `/version:2.0` para habilitar a vinculação de dados.|

## <a name="see-also"></a>Consulte também

- [Gerar a biblioteca de clientes do serviço de dados](generating-the-data-service-client-library-wcf-data-services.md)
- [Como: adicionar uma referência de serviço de dados](how-to-add-a-data-service-reference-wcf-data-services.md)
