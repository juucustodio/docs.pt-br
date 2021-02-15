---
description: 'Saiba mais sobre: como: usar EdmGen.exe para validar arquivos de modelo e de mapeamento'
title: 'Como: usar EdmGen.exe para validar o modelo e arquivos de mapeamento'
ms.date: 03/30/2017
ms.assetid: 2641906a-971a-4d0b-8aee-13fabc02a1cc
ms.openlocfilehash: e729ea36b7ff17dc318f4488a669b968161aea8b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697342"
---
# <a name="how-to-use-edmgenexe-to-validate-model-and-mapping-files"></a>Como: usar EdmGen.exe para validar o modelo e arquivos de mapeamento

Este tópico mostra como usar a ferramenta [gerador de EDM (EdmGen.exe)](edm-generator-edmgen-exe.md) para validar o modelo e os arquivos de mapeamento. Para obter mais informações, consulte [modelo de dados de entidade](../entity-data-model.md).  
  
### <a name="to-validate-the-school-model-using-edmgenexe"></a>Para validar a escola EdmGen.exe do modelo  
  
1. Crie o banco de dados da escola. Para obter mais informações, consulte [criando o banco de dados de exemplo da escola](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100)).  
  
2. Gerencia o modelo de escola. Para obter mais informações, consulte [como: usar EdmGen.exe para gerar o modelo e os arquivos de mapeamento](how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
3. No prompt de comando, execute o seguinte comando sem quebras de linha:  
  
    ```console
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:ValidateArtifacts /inssdl:.\School.ssdl /inmsl:.\School.msl /incsdl:.\School.csdl  
    ```  
  
## <a name="see-also"></a>Consulte também

- [Como configurar manualmente um projeto de Entity Framework](/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))
- [Ferramentas de Modelo de Dados de Entidade de ADO.NET](/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [Como: gerar previamente modos de exibição para melhorar o desempenho da consulta](/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))
- [Como: usar EdmGen.exe para gerar código de objetos camada](how-to-use-edmgen-exe-to-generate-object-layer-code.md)
