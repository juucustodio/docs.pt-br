---
title: Controle de versão do assembly
description: Saiba mais sobre o controle de versão de assemblies .NET. Todas as versões de assemblies que usam o CLR são feitas no nível do assembly.
ms.date: 08/20/2019
helpviewer_keywords:
- informational versions
- version numbers, assemblies
- assemblies [.NET], versioning
- resolving assembly binding requests
- versioning, assemblies
ms.assetid: 775ad4fb-914f-453c-98ef-ce1089b6f903
ms.openlocfilehash: c94e0c74b8beed29537b53d7476715e2cacb7b80
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687643"
---
# <a name="assembly-versioning"></a>Controle de versão do assembly

Todo o controle de versão de assemblies que usam o Common Language Runtime é feito no nível do assembly. A versão específica de um assembly e as versões de assemblies dependentes são registradas no manifesto do assembly. A política de versão padrão do runtime diz que aplicativos só são executados com as versões com que foram compilados e testados, a menos que essa política de versão seja substituída pela política de versão explícita em arquivos de configuração (o arquivo de configuração do aplicativo, o arquivo de política do editor e o arquivo de configuração do administrador do computador).  
  
> [!NOTE]
> O controle de versão só é feito em assemblies com nomes fortes.  
  
O ambiente de runtime realiza várias etapas para resolver uma solicitação de associação de assembly:  
  
1. Verifica a referência ao assembly original para determinar a versão do assembly a ser associada.  
  
2. Verifica todos os arquivos de configuração aplicáveis para aplicar uma política de versão.  
  
3. Determina o assembly correto com base na referência do assembly original e qualquer redirecionamento especificado nos arquivos de configuração, além de determinar a versão que deve ser associada ao assembly de chamada.  
  
4. Verifica o cache de assembly global, codebases especificados em arquivos de configuração e, em seguida, verifica o diretório e os subdiretórios do aplicativo usando as regras de investigação explicadas em [como o tempo de execução localiza assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).  
  
A seguinte ilustração mostra estas etapas:  
  
![Diagrama que mostra as etapas na resolução da solicitação de associação de assembly.](./media/versioning/resolve-assembly-binding-request.gif)
  
Para obter mais informações sobre como configurar aplicativos, consulte [configurar aplicativos](../../framework/configure-apps/index.md). Para obter mais informações sobre a política de associação, consulte [como o tempo de execução localiza assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).  
  
## <a name="version-information"></a>Informações da versão  

Cada assembly tem duas maneiras diferentes de expressar informações de versão:  
  
- O número de versão do assembly que, com o nome e a cultura do assembly, faz parte da identidade do assembly. Esse número é usado pelo runtime para impor a política de versão e desempenha um papel fundamental no processo de resolução do tipo no runtime.  
  
- Uma versão informativa, uma cadeia de caracteres que representa informações de versão adicionais incluída apenas para fins informativos.  
  
### <a name="assembly-version-number"></a>Número de versão do assembly  

Cada assembly tem um número de versão como parte de sua identidade. Dessa forma, dois assemblies que diferem pelo número de versão são considerados pelo ambiente de runtime assemblies completamente diferentes. Esse número de versão é representado fisicamente como uma cadeia de caracteres em quatro partes com o seguinte formato:  
  
\<*major version*>.\<*minor version*>.\<*build number*>.\<*revision*>  
  
Por exemplo, a versão 1.5.1254.0 indica que 1 é a versão principal, 5 é a versão secundária, 1254 é o número da versão e 0 é o número de revisão.  
  
O número da versão é armazenado no manifesto do assembly com outras informações de identidade, incluindo o nome e a chave pública do assembly, bem como informações sobre relacionamentos e identidades de outros assemblies conectados ao aplicativo.  
  
Quando um assembly é compilado, a ferramenta de desenvolvimento registra as informações de dependência de cada assembly referenciado no manifesto do assembly. O runtime usa esses números de versão, com informações de configuração definidas por um administrador, por um aplicativo ou por um editor, para carregar a versão apropriada de um assembly referenciado.  
  
O runtime diferencia assemblies regulares de assemblies com nomes fortes para fins de controle de versão. A verificação de versão só ocorre em assemblies com nomes fortes.  
  
Para obter informações sobre como especificar políticas de associação de versão, consulte [configurar aplicativos](../../framework/configure-apps/index.md). Para obter informações sobre como o tempo de execução usa informações de versão para localizar um assembly específico, consulte [como o tempo de execução localiza assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).  
  
### <a name="assembly-informational-version"></a>Versão informativa do assembly  

A versão informativa é uma cadeia de caracteres que anexa informações adicionais de versão a um assembly apenas para fins informativos; essa informação não é usada no tempo de execução. A versão informativa com base em texto corresponde à literatura de marketing, ao empacotamento ou ao nome do produto e não é usada pelo runtime. Por exemplo, uma versão informativa poderia ser "Common Language Runtime versão 1.0" ou "NET Control SP 2". Na guia Versão da caixa de diálogo de propriedades do arquivo no Microsoft Windows, essas informações são exibidas no item "Versão do Produto".  
  
> [!NOTE]
> Embora você possa especificar qualquer texto, uma mensagem de aviso aparecerá durante a compilação se a cadeia de caracteres não estiver no formato usado pelo número de versão do assembly ou se ela estiver no formato correto, mas contiver curingas. Esse aviso é inofensivo.  
  
A versão informativa é representada usando-se o atributo personalizado <xref:System.Reflection.AssemblyInformationalVersionAttribute?displayProperty=nameWithType>. Para obter mais informações sobre o atributo versão informativa, consulte [set Assembly Attributes](set-attributes.md).  
  
## <a name="see-also"></a>Veja também

- [Como o tempo de execução localiza assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [Configurar aplicativos](../../framework/configure-apps/index.md)
- [Definir atributos do assembly](set-attributes.md)
- [Assemblies no .NET](index.md)
