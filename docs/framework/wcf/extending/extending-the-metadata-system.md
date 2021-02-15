---
description: 'Saiba mais sobre: estendendo o sistema de metadados'
title: Estendendo o sistema de metadados
ms.date: 03/30/2017
helpviewer_keywords:
- extending metadata [WCF]
ms.assetid: 8c6b3b00-61b8-4589-8fa5-546cc33719bf
ms.openlocfilehash: e8409e29f9dc604ccc6bf399497f3d48f3bcd8f9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685550"
---
# <a name="extending-the-metadata-system"></a>Estendendo o sistema de metadados

O sistema de metadados do Windows Communication Foundation (WCF) é um grupo de classes e interfaces que representam os metadados necessários para implementar aplicativos baseados em serviço. Modifique ou estenda as classes ou implemente e configure as interfaces para exportar e importar metadados personalizados, como extensões WSDL (Web Services Description Language) ou declarações de WS-PolicyAttachments personalizadas.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Exportando metadados personalizados para uma extensão do WCF](exporting-custom-metadata-for-a-wcf-extension.md)  
 Descreve como implementar e usar a <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> interface para inserir declarações de política personalizada em documentos WSDL.  
  
 [Importando metadados personalizados para uma extensão do WCF](importing-custom-metadata-for-a-wcf-extension.md)  
 Descreve como implementar e usar a <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> interface para ler e responder a declarações de política personalizadas em documentos WSDL.  
  
 [Publicando e recuperando metadados através de uma associação personalizada](publishing-and-retrieving-metadata-over-a-custom-binding.md)  
 Descreve como trocar metadados em associações personalizadas.
