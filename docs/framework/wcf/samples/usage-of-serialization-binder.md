---
description: 'Saiba mais sobre: uso do associador de serialização'
title: Utilização do associador de serialização
ms.date: 03/30/2017
ms.assetid: ab46c087-200c-45bf-9c95-5a6cda6e8b98
ms.openlocfilehash: ee00d8049ae644525f8013801dc7c453b9ad5aeb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798167"
---
# <a name="usage-of-serialization-binder"></a>Utilização do associador de serialização

Este exemplo mostra como usar o <xref:System.Runtime.Serialization.SerializationBinder> para alterar a versão de um tipo genérico quando ele é serializado.  
  
## <a name="demonstrates"></a>Demonstra  

 <xref:System.Runtime.Serialization.SerializationBinder>, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>  
  
## <a name="discussion"></a>Discussão  

 Este exemplo mostra como duas entidades que se destinam a diferentes versões do .NET Framework podem se comunicar usando o formatador binário e o associador de serialização.  
  
Este exemplo foi desenvolvido usando a comunicação remota do .NET. Ele consiste em um servidor de destino .NET Framework 4, que implementa um contrato com tipos genéricos e dois clientes diferentes, um direcionamento .NET Framework 2,0 e outro direcionamento .NET Framework 4.  
  
 O servidor anexa um <xref:System.Runtime.Serialization.SerializationBinder> ao formatador binário para poder alterar a versão dos tipos de acordo com a serialização, para que ambos os clientes possam desserializar esses tipos corretamente.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar e executar o exemplo  
  
1. Para executar o cliente, clique com o botão direito do mouse na solução, SBGenericsVTS (6 projetos) e selecione **Propriedades**.  
  
2. Em **Propriedades comuns**, selecione **projeto de inicialização** e, em seguida, selecione **vários projetos de inicialização**.  
  
3. Selecione primeiro **servidor** , em seguida, **Client20** e **Client40**. Selecione a ação **Iniciar** para esses três projetos e deixe o REST definido como **nenhum**.  
  
4. Clique em **OK** e pressione F5 para executar o exemplo.
