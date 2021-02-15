---
description: 'Saiba mais sobre: como adicionar uma referência de serviço de dados (WCF Data Services)'
title: 'Como: adicionar uma referência de serviço de dados (WCF Data Services)'
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 62c6f318-3ee1-433a-b7a3-efa234c3034c
ms.openlocfilehash: 907ad9a7dc3710a6e565de55c74a0d279d20e159
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765744"
---
# <a name="how-to-add-a-data-service-reference-wcf-data-services"></a>Como: adicionar uma referência de serviço de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Você pode usar a caixa de diálogo **Adicionar referência de serviço** no Visual Studio para adicionar uma referência a WCF Data Services. Isso permite que você acesse mais facilmente um serviço de dados em um aplicativo cliente que você desenvolve no Visual Studio. Quando você concluir este procedimento, as classes de dados serão geradas com base nos metadados obtidos do serviço de dados. Para obter mais informações, consulte [gerando a biblioteca de cliente do serviço de dados](generating-the-data-service-client-library-wcf-data-services.md).

## <a name="add-a-data-service-reference"></a>Adicionar uma referência de serviço de dados

1. Adicional Se o serviço de dados não fizer parte da solução e ainda não estiver em execução, inicie o serviço de dados e anote o URI do serviço de dados.

2. No Visual Studio, em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto cliente e selecione **Adicionar**  >  **referência de serviço**.

3. Se o serviço de dados fizer parte da solução atual, clique em **descobrir**.

     -ou-

     Na caixa de texto **endereço** , digite a URL base do serviço de dados, como `http://localhost:1234/Northwind.svc` e clique em **ir**.

4. Selecione **OK**.

     Um novo arquivo de código que contém as classes de dados que podem acessar e interagir com os recursos do serviço de dados é adicionado ao projeto.

## <a name="see-also"></a>Consulte também

- [Início rápido](quickstart-wcf-data-services.md)
