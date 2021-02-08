---
description: 'Saiba mais sobre: localizar ferramenta de chave privada (FindPrivateKey.exe)'
title: Encontrar ferramenta de chave privada (FindPrivateKey.exe)
ms.date: 09/11/2017
ms.assetid: b8846a95-3fcc-4e8c-b9c0-128d975a6307
ms.openlocfilehash: 1d87d19e17c1de89c13db6d7ca092eedf630e6ca
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793279"
---
# <a name="find-private-key-tool-findprivatekeyexe"></a>Encontrar ferramenta de chave privada (FindPrivateKey.exe)

Essa ferramenta de linha de comando pode ser usada para recuperar uma chave privada de um repositório de certificados. Por exemplo, *FindPrivateKey.exe* pode ser usado para localizar o local e o nome do arquivo de chave privada associado a um certificado X. 509 específico no repositório de certificados.

> [!IMPORTANT]
> A ferramenta FindPrivateKey é fornecida como um exemplo do WCF. Para obter mais informações sobre onde encontrar o exemplo e como compilá-lo, consulte [FindPrivateKey](./samples/findprivatekey.md).

## <a name="syntax"></a>Sintaxe

```console
FindPrivateKey<storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]
```

## <a name="remarks"></a>Comentários

As tabelas a seguir descrevem os argumentos e as opções que podem ser usadas com a ferramenta localizar chave privada (FindPrivateKey.exe).

|Argumento|Descrição|
|--------------|-----------------|
|`storeName`|Nome do repositório de certificados.|
|`storeLocation`|O local do repositório de certificados.|

|Opção|Descrição|
|------------|-----------------|
|`/n <`*SubjectName*`>`|Especifica o nome da entidade do certificado.|
|`/t <`*impressão digital*`>`|Especifica a impressão digital do certificado. Use Certmgr.exe para recuperar a impressão digital do certificado.|
|`/f`|Gera apenas o nome do arquivo.|
|`/d`|Gera somente o diretório.|
|`/a`|Gera o nome de arquivo absoluto.|

## <a name="examples"></a>Exemplos

O comando a seguir recupera a chave privada para John Doe:

```console
FindPrivateKey My CurrentUser -n "CN=John Doe"
```

O comando a seguir recupera a chave privada para o computador local:

```console
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52" –a
```
