---
description: 'Saiba mais sobre: nome forte (referência de API não gerenciada)'
title: Nomenclatura forte (referência de API não gerenciada)
ms.date: 03/30/2017
helpviewer_keywords:
- strong naming [.NET Framework], using the unmanaged API
- native API reference [.NET Framework], strong naming
- unmanaged API reference [.NET Framework], strong naming
ms.assetid: 428c68b6-a7b4-44be-b280-75905f46612c
ms.openlocfilehash: 058cc51d8e9eb2ef4a2d0670811aefcd32dafb6e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646355"
---
# <a name="strong-naming-unmanaged-api-reference"></a>Nomenclatura forte (referência de API não gerenciada)

A API de nomenclatura forte permite que um cliente administre a assinatura de nome forte para assemblies.  
  
 Assinar um assembly com um nome forte adiciona uma criptografia de chave pública ao arquivo que contém o manifesto do assembly. Assinatura de nome forte ajuda a verificar a exclusividade do nome, a evitar falsificação de nome e a fornecer chamadores com uma identidade exclusiva quando uma referência é resolvida. No entanto, nenhum nível de confiança está associado a um nome forte.  
  
## <a name="in-this-section"></a>Nesta seção  
  
> [!NOTE]
> Todas essas funções foram preteridas a partir do .NET Framework 4. Para alternativas sugeridas, consulte a interface [ICLRStrongName](../hosting/iclrstrongname-interface.md).  
  
 [Função GetHashFromAssemblyFile](gethashfromassemblyfile-function.md)  
 Obtém um hash do arquivo do assembly especificado, usando o algoritmo de hash especificado. Preteridos do .NET Framework 4 em diante.  
  
 [Função GetHashFromAssemblyFileW](gethashfromassemblyfilew-function.md)  
 Obtém um hash do arquivo do assembly especificado como uma cadeia de caracteres Unicode, usando o algoritmo de hash especificado. Preteridos do .NET Framework 4 em diante.  
  
 [Função GetHashFromBlob](gethashfromblob-function.md)  
 Obtém um hash do assembly no endereço de memória especificado, usando o algoritmo de hash especificado. Preteridos do .NET Framework 4 em diante.  
  
 [Função GetHashFromFile](gethashfromfile-function.md)  
 Gera um hash sobre o conteúdo do arquivo especificado.  Preteridos do .NET Framework 4 em diante.  
  
 [Função GetHashFromFileW](gethashfromfilew-function.md)  
 Gera um hash sobre o conteúdo do arquivo especificado por uma cadeia de caracteres Unicode. Preteridos do .NET Framework 4 em diante.  
  
 [Função GetHashFromHandle](gethashfromhandle-function.md)  
 Gera um hash sobre o conteúdo do arquivo com o identificador de arquivo especificado, usando o algoritmo de hash especificado.  Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameCompareAssemblies](strongnamecompareassemblies-function.md)  
 Determina se dois assemblies diferem somente por suas assinaturas de nome forte. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameErrorInfo](strongnameerrorinfo-function.md)  
 Obtém o último código de erro que foi gerado por uma das funções de nome forte.  
  
 [Função StrongNameFreeBuffer](strongnamefreebuffer-function.md)  
 Libera a memória que foi alocada com uma chamada anterior a uma função de nome forte, como [StrongNameGetPublicKey](strongnamegetpublickey-function.md), [StrongNameTokenFromPublicKey](strongnametokenfrompublickey-function.md), ou [StrongNameSignatureGeneration](strongnamesignaturegeneration-function.md).   Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameGetBlob](strongnamegetblob-function.md)  
 Preenche o buffer especificado com a representação binária do arquivo executável no endereço especificado. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameGetBlobFromImage](strongnamegetblobfromimage-function.md)  
 Obtém uma representação binária da imagem do assembly no endereço de memória especificado. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameGetPublicKey](strongnamegetpublickey-function.md)  
 Obtém a chave pública de um par de chaves pública/privada. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameHashSize](strongnamehashsize-function.md)  
 Obtém o tamanho do buffer necessário para um hash, usando o algoritmo de hash especificado.  Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameKeyDelete](strongnamekeydelete-function.md)  
 Exclui o contêiner de chave especificado. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameKeyGen](strongnamekeygen-function.md)  
 Cria um novo par de chaves públicas/privadas para uso de nome forte.  Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameKeyGenEx](strongnamekeygenex-function.md)  
 Gera um novo par de chaves públicas/privadas com o tamanho da chave especificado para o uso de nome forte. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameKeyInstall](strongnamekeyinstall-function.md)  
 Importa um par de chaves públicas/privadas em um contêiner.  Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameSignatureGeneration](strongnamesignaturegeneration-function.md)  
 Gera uma assinatura de nome forte para o assembly especificado.   Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameSignatureGenerationEx](strongnamesignaturegenerationex-function.md)  
 Gera uma assinatura de nome forte para o assembly especificado, com base nos sinalizadores especificados.    Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameSignatureSize](strongnamesignaturesize-function.md)  
 Retorna o tamanho da assinatura de nome forte. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameSignatureVerification](strongnamesignatureverification-function.md)  
 Obtém um valor que indica se o manifesto do assembly no caminho fornecido contém uma assinatura de nome forte, que é verificada de acordo com os sinalizadores especificados. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameSignatureVerificationEx](strongnamesignatureverificationex-function.md)  
 Obtém um valor que indica se o manifesto do assembly no caminho fornecido contém uma assinatura de nome forte.  Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameSignatureVerificationFromImage](strongnamesignatureverificationfromimage-function.md)  
 Verifica se um assembly, que já foi mapeado para a memória, é válido para a chave pública associada. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameTokenFromAssembly](strongnametokenfromassembly-function.md)  
 Cria um token de nome forte do arquivo do assembly especificado.  Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameTokenFromAssemblyEx](strongnametokenfromassemblyex-function.md)  
 Cria um token de nome forte por meio do arquivo do assembly especificado e retorna a chave pública. Preteridos do .NET Framework 4 em diante.  
  
 [Função StrongNameTokenFromPublicKey](strongnametokenfrompublickey-function.md)  
 Obtém um token que representa uma chave pública. Preteridos do .NET Framework 4 em diante.  
  
 [Estrutura PublicKeyBlob](publickeyblob-structure.md)  
 Representa a chave pública de um par de chaves públicas/privadas em formato binário.  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
- [Referência de API não gerenciada](../index.md)
