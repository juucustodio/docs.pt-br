---
description: 'Saiba mais sobre: depuração do Silverlight'
title: Depuração Silverlight
ms.date: 03/30/2017
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
ms.assetid: 5e903e04-17d0-4014-ac9a-a43330ec8b1c
ms.openlocfilehash: 54a3f7f4b2de867509ff94dafa25c067a78b3ee6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800533"
---
# <a name="silverlight-debugging"></a>Depuração Silverlight

Os tópicos nesta seção descrevem o ambiente e as interfaces que o Common Language Runtime (CLR) fornece para dar suporte à depuração de aplicativos baseados no Silverlight que estão em execução no sistema operacional Windows ou na plataforma Macintosh.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Função EnumerateCLRs](enumerateclrs-function.md)  
 Fornece um mecanismo para enumerar o CLRs em um processo.  
  
 [Função CloseCLREnumeration](closeclrenumeration-function.md)  
 Fecha qualquer evento válido de inicialização de continuidade do CLR localizado em uma matriz de identificadores retornada pela [função EnumerateCLRs](enumerateclrs-function.md)e libera a memória para as matrizes de caminho de cadeia de caracteres e identificador.  
  
 [Função CreateCoreClrDebugTarget](createcoreclrdebugtarget-function.md)  
 Cria uma conexão com um destino remoto para enumeração de processo e tempo de execução.  
  
 [Função CreateCordbObject](createcordbobject-function.md)  
 Cria uma interface do depurador que fornece funcionalidade para instanciar uma sessão de depuração gerenciada em um processo remoto.  
  
 [Função CreateVersionStringFromModule](createversionstringfrommodule-function.md)  
 Cria uma cadeia de caracteres de versão a partir de um caminho CLR em um processo de destino.  
  
 [Função CreateDebuggingInterfaceFromVersion](createdebugginginterfacefromversion-function-for-silverlight.md)  
 Aceita uma cadeia de caracteres de versão do CLR retornada da função de [função CreateVersionStringFromModule](createversionstringfrommodule-function.md)e retorna uma interface de depurador correspondente.  
  
 [Estrutura CoreClrDebugProcInfo](coreclrdebugprocinfo-structure.md)  
 Representa um processo que está sendo executado em um computador remoto.  
  
 [Estrutura CoreClrDebugRuntimeInfo](coreclrdebugruntimeinfo-structure.md)  
 Representa uma instância do CLR que é carregada em um processo em um computador remoto.  
  
 [Função GetStartupNotificationEvent](getstartupnotificationevent-function.md)  
 Cria ou abre um identificador de evento que será sinalizado por qualquer Common Language Runtime (CLR) que esteja carregando no processo de destino especificado.  
  
 [Interface ICoreClrDebugTarget](icoreclrdebugtarget-interface.md)  
 Cria uma conexão com um destino remoto para enumeração de processo e tempo de execução.  
  
 [Função InitDbgTransportManager](initdbgtransportmanager-function.md)  
 Inicializa o Gerenciador de transporte para se conectar a um destino remoto para enumeração de processo e tempo de execução.  
  
 [Função ShutdownDbgTransportManager](shutdowndbgtransportmanager-function.md)  
 Desliga o Gerenciador de transporte para uma conexão a um computador de destino remoto.  
  
## <a name="see-also"></a>Consulte também

- [Depurando coclasses](debugging-coclasses.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depurando funções estáticas globais](debugging-global-static-functions.md)
- [Declarando enumerações](debugging-enumerations.md)
- [Estruturas de depuração](debugging-structures.md)
