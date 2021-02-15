---
title: Manifesto do assembly
description: Um manifesto de assembly .NET especifica seus requisitos de versão, identidade de segurança e escopo do assembly e informações para resolver referências.
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest
- dynamic assemblies, assembly manifest
- metadata, assembly manifest
- culture, assembly manifest
- assemblies [.NET], metadata
ms.assetid: 8e40fab9-549d-4731-aec2-ffa47a382de0
ms.openlocfilehash: 365c21c6ea35683d7d3fad777cab3527103903c3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731508"
---
# <a name="assembly-manifest"></a>Manifesto do assembly

Cada assembly, seja estático ou dinâmico, contém uma coleção de dados que descreve como os elementos do assembly se relacionam. O manifesto do assembly contém esses metadados do assembly. O manifesto de um assembly contém todos os metadados necessários para especificar os requisitos de versão e a identidade de segurança, além de todos os metadados necessários para definir o escopo do assembly e resolver referências a recursos e classes. O manifesto do assembly pode ser armazenado em um arquivo PE (um *. exe* ou *. dll*) com o código MSIL (Microsoft Intermediate Language) ou em um arquivo PE autônomo que contém apenas informações de manifesto do assembly.  
  
 A ilustração a seguir mostra as diferentes maneiras nas quais o manifesto pode se armazenado.  
  
 ![Diagrama que mostra o manifesto em uma configuração de assembly de arquivo único e de assembly de vários arquivos.](./media/manifest/assembly-types-diagram.gif)  
  
 Para um assembly com um arquivo associado, o manifesto é incorporado ao arquivo PE para formar um assembly de arquivo único. Você pode criar um assembly de vários arquivos com um arquivo de manifesto autônomo ou com o manifesto incorporado a um dos arquivos PE do assembly.  
  
 Cada manifesto de um assembly executa as seguintes funções:  
  
- Enumera os arquivos que compõem o assembly.  
  
- Determina como as referências a tipos e recursos do assembly são mapeadas para arquivos que contenham suas declarações e implementações.  
  
- Enumera outros assemblies dos quais o assembly depende.  
  
- Fornece um nível de indireção entre consumidores do assembly e detalhes da implementação do assembly.  
  
- Renderiza o assembly autodescritivo.  
  
## <a name="assembly-manifest-contents"></a>Conteúdo do manifesto do assembly  

 A tabela a seguir mostra as informações contidas no manifesto do assembly. Os quatro primeiros itens: nome do assembly, número de versão, cultura e informações de nome forte compõem a identidade do assembly.  
  
|Informações|Descrição|  
|-----------------|-----------------|  
|Nome do assembly|Uma cadeia de caracteres de texto especificando o nome do assembly.|  
|Número de versão|Um número de versão principal e secundário, além de um número de revisão e de compilação. O Common Language Runtime usa esses números para impor uma política de versões.|  
|Cultura|Informações sobre a cultura ou a linguagem compatível com o assembly. Essas informações só devem ser usadas para designar um assembly como um assembly satélite contendo informações específicas de cultura ou de linguagem. (Um assembly com informações de cultura é automaticamente considerado um assembly satélite.)|  
|Informações sobre nome forte|A chave pública do editor, caso tenha sido dado ao assembly um nome forte.|  
|Lista de todos os arquivos no assembly|Um hash de cada arquivo contido no assembly e um nome de arquivo. Observe que todos os arquivos que compõem o assembly devem estar no mesmo diretório que o arquivo que contém o manifesto do assembly.|  
|Informações de referência de tipo|Informações usadas pelo ambiente de runtime para mapear a referência de um tipo para o arquivo que contém sua declaração e implementação. Usado em tipos que são exportados do assembly.|  
|Informações sobre assemblies referenciados|Uma lista de outros assemblies que são referenciados estaticamente pelo assembly. Cada referência inclui o nome do assembly dependente, metadados do assembly (versão, cultura, sistema operacional etc.) e chave pública, caso o assembly possua um nome forte.|  
  
 Você pode adicionar ou alterar informações do manifesto do assembly usando os atributos do assembly em seu código. Você pode alterar informações sobre versão e atributos informativos, incluindo marca comercial, direitos autorais, produto, empresa e versão informativa. Para obter uma lista completa de atributos de assembly, consulte [set Assembly Attributes](set-attributes.md).  
  
## <a name="see-also"></a>Confira também

- [Conteúdos do assembly](contents.md)
- [Controle de versão do assembly](versioning.md)
- [Criar assemblies satélite](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
- [Assemblies de nome forte](strong-named.md)
