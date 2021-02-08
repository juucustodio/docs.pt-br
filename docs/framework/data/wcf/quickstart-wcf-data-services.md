---
description: 'Saiba mais sobre: início rápido (WCF Data Services)'
title: Guia de Início Rápido (WCF Data Services)
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, quick-start example
- WCF Data Services, Entity Data Model (EDM) service
ms.assetid: 7b18ca1e-d4d6-4c7a-afb9-ce3cebb98a8d
ms.openlocfilehash: 92a1b8882f6a7db2ed33f032ad434efd06400421
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794943"
---
# <a name="quickstart-wcf-data-services"></a>Guia de Início Rápido (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Este guia de início rápido ajuda você a se familiarizar com WCF Data Services e o Protocolo Open Data (OData) por meio de uma série de tarefas que dão suporte aos tópicos em [introdução](getting-started-with-wcf-data-services.md).

## <a name="what-youll-learn"></a>O que você aprenderá

A primeira tarefa neste guia de início rápido mostra como criar um serviço de dados para expor um feed OData do banco de dados de exemplo Northwind. Nos tópicos posteriores, você acessará o feed OData usando um navegador da Web e também criará um aplicativo cliente Windows Presentation Foundation (WPF) que consome o feed OData usando bibliotecas de cliente.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este guia de início rápido, instale os seguintes componentes:

- Visual Studio

- Uma instância de SQL Server. Isso inclui SQL Server Express, que está incluído em uma instalação padrão do Visual Studio 2015 ou como parte da carga de trabalho de **armazenamento e processamento de dados** no visual Studio 2017 ou posterior.

- O banco de dados de exemplo Northwind. Para instalar o banco de dados, execute o script Transact-SQL nos bancos de dados [de exemplo Northwind e pubs para Microsoft SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs).

## <a name="wcf-data-services-quickstart-tasks"></a>Tarefas de início rápido do WCF Data Services

 [Criar o serviço de dados](creating-the-data-service.md)

 Defina o aplicativo ASP.NET, defina o modelo de dados, crie o serviço de dados e habilite o acesso aos recursos.

 [Acessar o serviço de um navegador da Web](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

 Inicie o serviço do Visual Studio e acesse o serviço enviando solicitações HTTP GET por meio de um navegador da Web para o feed exposto.

 [Criar o aplicativo cliente .NET Framework](creating-the-dotnet-client-application-wcf-data-services-quickstart.md)

 Crie um aplicativo WPF para consumir o feed OData, associar dados a controles do Windows, alterar dados nos controles vinculados e enviar as alterações de volta para o serviço de dados.

> [!NOTE]
> Os arquivos de projeto de uma versão concluída do guia de início rápido podem ser baixados do [GitHub](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/WCF%20Data%20Services%20Quickstart%20(OData%20Service%20and%20WPF%20Client)).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Iniciar o início rápido](creating-the-data-service.md)

## <a name="see-also"></a>Consulte também

- [ADO.NET Entity Framework](../adonet/ef/index.md)
