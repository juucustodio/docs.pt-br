---
description: 'Saiba mais sobre: rastreamento do SQL'
title: Rastreamento de SQL
ms.date: 03/30/2017
ms.assetid: bcaebeb1-b9e5-49e8-881b-e49af66fd341
ms.openlocfilehash: 2b336839b9c63c0b7bde8b6451add00cb353fec6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741738"
---
# <a name="sql-tracking"></a>Rastreamento do SQL

Este exemplo demonstra como gravar um participante de rastreamento do SQL personalizado que grava registros de rastreamento em um banco de dados SQL. Windows Workflow Foundation (WF) fornece rastreamento de fluxo de trabalho para obter visibilidade da execução de uma instância de fluxo de trabalho. O runtime de rastreamento emite-se registros de acompanhamento de fluxo de trabalho durante a execução de fluxo de trabalho. Para obter mais informações sobre o rastreamento de fluxo de trabalho, consulte rastreamento [e acompanhamento de fluxo de trabalho](../workflow-tracking-and-tracing.md).

## <a name="use-the-sample"></a>Usar o exemplo

1. Verifique têm SQL Server 2008, SQL Server 2008 Express edition ou mais recente instalados. Os scripts agrupados com o exemplo assumem o uso de uma instância do SQL express em seu computador local. Se você tiver uma instância diferente por favor alterar os scripts base de dados - relacionados antes de executar o exemplo.

2. Crie o SQL Server que controla o base de dados executando Trackingsetup.cmd no diretório de scripts (\ \ WF básico rastreamento SqlTracking \ \ \ \ CS scripts). Isso cria um base de dados chamado TrackingSample.

   > [!NOTE]
   > O script cria o base de dados na instância padrão do SQL express. Se você deseja instalá-lo em uma instância diferente de base de dados, editar script de Trackingsetup.cmd.

3. Abra SqlTrackingSample. sln no Visual Studio 2010.

4. Pressione **Ctrl** + **Shift** + **B** para criar a solução.

5. Pressione **F5** para executar o aplicativo.

   A janela do navegador abre e mostra a listagem de diretório para o aplicativo.

6. No navegador, clique StockPriceService.xamlx.

7. O navegador exibe a página de StockPriceService, que contém o endereço de WSDL de serviço local. Copie este endereço.

   Um exemplo do endereço WSDL do serviço local é `http://localhost:65193/StockPriceService.xamlx?wsdl` .

8. Usando o explorador de arquivos, execute o cliente de teste do WCF (WcfTestClient.exe). Ele está localizado no *diretório Microsoft Visual Studio 10.0 \ Common7\IDE*

9. No cliente de teste do WCF, clique no menu **arquivo** e selecione **Adicionar serviço**. Cole o endereço do serviço local na caixa de texto. Clique em **OK** para fechar o diálogo.

10. No cliente de teste do WCF, clique duas vezes em **GetStockPrice**. Isso abre a `GetStockPrice` operação que usa um parâmetro, digita o valor `Contoso` e clica em **invocar**.

11. Os registros emissores de rastreamento são gravados em uma base de dados SQL. Para exibir os registros de rastreamento, abra o base de dados de TrackingSample em SQL Management Studio e navegar para tabelas. Executar uma consulta selecionar as tabelas exibe os dados dentro dos registros de rastreamento armazenados nas tabelas respectivas.

   Para obter mais informações sobre SQL Server Management Studio, consulte [introdução a SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms). Baixe SQL Server Management Studio [aqui](https://aka.ms/ssmsfullsetup).

## <a name="uninstall-the-sample"></a>Desinstalar o exemplo

1. Execute o script theTrackingcleanup. cmd no diretório de exemplo (*\WF\Basic\Tracking\SqlTracking*).

    > [!NOTE]
    > O Trackingcleanup.cmd tentar excluir o base de dados em seu computador local SQL express. Se você estiver usando outra instância do SQL server, editar Trackingcleanup.cmd.

> [!IMPORTANT]
> Os exemplos podem mais ser instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\SqlTracking`

## <a name="see-also"></a>Consulte também

- [AppFabric que monitora Exemplos](/previous-versions/appfabric/ff383407(v=azure.10))
