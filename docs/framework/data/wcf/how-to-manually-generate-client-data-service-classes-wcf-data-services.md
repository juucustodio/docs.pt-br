---
description: 'Saiba mais sobre: como gerar manualmente classes de serviço de dados do cliente (WCF Data Services)'
title: 'Como: gerar manualmente classes de serviço de dados do cliente (WCF Data Services)'
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- WCF Data Services, client library
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
ms.openlocfilehash: 6fe878e1177055540a29fb84252eddaa4d97e536
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765198"
---
# <a name="how-to-manually-generate-client-data-service-classes-wcf-data-services"></a>Como: gerar manualmente classes de serviço de dados do cliente (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

O WCF Data Services integra-se com o Visual Studio para permitir que você gere automaticamente classes de serviço de dados do cliente quando você usa a caixa de diálogo **Adicionar referência de serviço** para adicionar uma referência a um serviço de dados em um projeto do Visual Studio. Para obter mais informações, consulte [como: adicionar uma referência de serviço de dados](how-to-add-a-data-service-reference-wcf-data-services.md). Você também pode gerar manualmente as mesmas classes de serviço de dados do cliente usando a ferramenta de geração de código, `DataSvcUtil.exe` . Essa ferramenta, que é incluída com o WCF Data Services, gera .NET Framework classes da definição do serviço de dados. Ele também pode ser usado para gerar classes de serviço de dados do arquivo de modelo conceitual (. CSDL) e do arquivo. edmx que representa um modelo de Entity Framework em um projeto do Visual Studio.

 O exemplo neste tópico cria classes de serviço de dados do cliente com base no serviço de dados de exemplo Northwind. Esse serviço é criado quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md). Alguns exemplos neste tópico exigem o arquivo de modelo conceitual para o modelo Northwind. Para obter mais informações, consulte [como: usar EdmGen.exe para gerar o modelo e os arquivos de mapeamento](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md). Alguns exemplos neste tópico exigem o arquivo. edmx para o modelo Northwind. Para obter mais informações, consulte [visão geral do arquivo. edmx](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)).

### <a name="to-generate-c-classes-that-support-data-binding"></a>Para gerar classes C# que dão suporte à vinculação de dados

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > Você deve substituir o valor fornecido para o `/uri:` parâmetro com o URI de sua instância do serviço de dados de exemplo Northwind.

### <a name="to-generate-visual-basic-classes-that-support-data-binding"></a>Para gerar Visual Basic classes que dão suporte à associação de dados

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > Você deve substituir o valor fornecido para o `/uri:` parâmetro com o URI de sua instância do serviço de dados de exemplo Northwind.

### <a name="to-generate-c-classes-based-on-the-service-uri"></a>Para gerar classes C# com base no URI do serviço

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > Você deve substituir o valor fornecido para o `/uri:` parâmetro com o URI de sua instância do serviço de dados de exemplo Northwind.

### <a name="to-generate-visual-basic-classes-based-on-the-service-uri"></a>Para gerar Visual Basic classes com base no URI do serviço

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > Você deve substituir o valor fornecido para o `/uri:` parâmetro com o URI de sua instância do serviço de dados de exemplo Northwind.

### <a name="to-generate-c-classes-based-on-the-conceptual-model-file-csdl"></a>Para gerar classes C# com base no arquivo de modelo conceitual (CSDL)

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-conceptual-model-file-csdl"></a>Para gerar Visual Basic classes com base no arquivo de modelo conceitual (CSDL)

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb
    ```

### <a name="to-generate-c-classes-based-on-the-edmx-file"></a>Para gerar classes C# com base no arquivo. edmx

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-edmx-file"></a>Para gerar Visual Basic classes com base no arquivo. edmx

- No prompt de comando, execute o seguinte comando sem quebras de linha:

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb
    ```

## <a name="see-also"></a>Consulte também

- [Gerar a biblioteca de clientes do serviço de dados](generating-the-data-service-client-library-wcf-data-services.md)
- [Como: adicionar uma referência de serviço de dados](how-to-add-a-data-service-reference-wcf-data-services.md)
- [Utilitário de cliente do WCF Data Service (DataSvcUtil.exe)](wcf-data-service-client-utility-datasvcutil-exe.md)
