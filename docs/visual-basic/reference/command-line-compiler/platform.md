---
description: Saiba mais sobre:-Platform (Visual Basic)
title: -platform
ms.date: 03/13/2018
helpviewer_keywords:
- platform compiler option [Visual Basic]
- /platform compiler option [Visual Basic]
- -platform compiler option [Visual Basic]
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
ms.openlocfilehash: 51d7c7882c29310ef1e0c0f5790a63da3bfb91b8
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100432735"
---
# <a name="-platform-visual-basic"></a>-plataforma (Visual Basic)

Especifica qual versão de plataforma do common language runtime (CLR) pode executar o arquivo de saída.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|---|---|  
|`x86`|Compila o assembly para ser executado pelo CLR compatível com x86, de 32 bits.|  
|`x64`|Compila o assembly para ser executado pelo CLR de 64 bits em um computador que oferece suporte ao conjunto de instruções de AMD64 ou EM64T.|  
|`Itanium`|Compila o assembly para ser executado pelo CLR de 64 bits em um computador com um processador Itanium.|  
|`arm`|Compila o assembly para ser executado em um computador com um processador ARM (Advanced RISC Machine).|  
|`anycpu`|Compila o assembly para ser executado em qualquer plataforma. O aplicativo será executado como um aplicativo de 32 bits em versões de 32 bits do Windows e como um aplicativo de 64 bits em versões de 64 bits do Windows. Este sinalizador é o valor padrão.|  
|`anycpu32bitpreferred`|Compila o assembly para ser executado em qualquer plataforma. O aplicativo será executado como um aplicativo de 32 bits em versões de 32 bits e 64 bits do Windows. Esse sinalizador é válido somente para executáveis (. EXE) e requer .NET Framework 4,5.|  
  
## <a name="remarks"></a>Comentários  

 Use a opção `-platform` para especificar o tipo de processador direcionada pelo arquivo de saída.  
  
 Em geral, os assemblies do .NET Framework gravados no Visual Basic serão executados da mesma maneira, independentemente da plataforma. No entanto, existem alguns casos em que se comportam de formas diferentes em plataformas distintas. Esses casos comuns são:  
  
- Estruturas que contêm membros que alteram o tamanho de acordo com a plataforma, como qualquer tipo de ponteiro.  
  
- Aritmética de ponteiro que inclui tamanhos constantes.  
  
- As declarações COM ou de invocação de plataforma incorreta que usam `Integer` para identificadores em vez de <xref:System.IntPtr>.  
  
- Convertendo <xref:System.IntPtr> para `Integer`.  
  
- Usando a invocação de plataforma ou a interoperabilidade COM com os componentes que não existem em todas as plataformas.  
  
 A opção **-Platform** atenuará alguns problemas se você souber que fez suposições sobre a arquitetura em que seu código será executado. Especificamente:  
  
- Se decidir atingir uma plataforma de 64 bits e o aplicativo for executado em uma máquina de 32 bits, a mensagem de erro vem muito mais cedo e mais direcionada ao problema do que o erro que ocorre sem usar essa comutador.  
  
- Se você definir o sinalizador `x86` na opção e, em seguida, o aplicativo for executado em uma máquina de 64 bits, o aplicativo será executado no subsistema WOW em vez de ser executado nativamente.  
  
 Em um sistema operacional do Windows de 64 bits:  
  
- Assemblies compilados com `-platform:x86` serão executados no CLR de 32 bits em execução no WOW64.  
  
- Executáveis compilados com o `-platform:anycpu` serão executados no CLR de 64 bits.  
  
- Uma DLL compilada com o `-platform:anycpu` será executada no mesmo CLR que o processo no qual foi carregado.  
  
- Executáveis compilados com `-platform:anycpu32bitpreferred` serão executados no CLR de 32 bits.  
  
 Para obter mais informações sobre como desenvolver um aplicativo para ser executado em uma versão de 64 bits do Windows, consulte [aplicativos de 64 bits](../../../framework/64-bit-apps.md).  
  
### <a name="to-set--platform-in-the-visual-studio-ide"></a>Para definir a plataforma no IDE do Visual Studio  
  
1. Em **Gerenciador de soluções**, escolha o projeto, abra o menu **projeto** e clique em **Propriedades**.  
  
2. Na guia **Compilar** , marque ou desmarque a caixa de seleção **preferir 32 bits** ou, na lista **CPU de destino** , escolha um valor.  
  
     Para obter mais informações, consulte [Compilar página, designer de projeto (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como usar a opção do compilador `-platform`.  
  
```console
vbc -platform:x86 myFile.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [-Target (Visual Basic)](target.md)
- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
