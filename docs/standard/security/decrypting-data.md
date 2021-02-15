---
title: Descriptografando dados
description: Saiba como descriptografar dados no .NET, usando um algoritmo simétrico ou um algoritmo assimétrico.
ms.date: 07/16/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [.NET], decryption
- symmetric decryption
- asymmetric decryption
- decryption
ms.assetid: 9b266b6c-a9b2-4d20-afd8-b3a0d8fd48a0
ms.openlocfilehash: cf286eeca8a9372c6532c56701e4775d5e09d786
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94831098"
---
# <a name="decrypting-data"></a>Descriptografando dados

A descriptografia é a operação inversa da criptografia. Para criptografia de chave secreta, você deve saber a chave e o IV que foram usados para criptografar os dados. Para criptografia de chave pública, você deve saber a chave pública (se os dados foram criptografados usando a chave privada) ou a chave privada (se os dados foram criptografados usando a chave pública).

## <a name="symmetric-decryption"></a>Descriptografia simétrica

A descriptografia de dados criptografados com algoritmos simétricos é semelhante ao processo usado para criptografar dados com algoritmos simétricos. A <xref:System.Security.Cryptography.CryptoStream> classe é usada com classes de criptografia simétrica fornecidas pelo .net para descriptografar dados lidos de qualquer objeto de fluxo gerenciado.

O exemplo a seguir ilustra como criar uma nova instância da classe de implementação padrão para o <xref:System.Security.Cryptography.Aes> algoritmo. A instância é usada para executar a descriptografia em um <xref:System.Security.Cryptography.CryptoStream> objeto. Este exemplo primeiro cria uma nova instância da <xref:System.Security.Cryptography.Aes> classe de implementação. Ele lê o valor do vetor de inicialização (IV) de uma variável de fluxo gerenciada, `myStream` . Em seguida, ele cria uma instância de um <xref:System.Security.Cryptography.CryptoStream> objeto e o inicializa para o valor da `myStream` instância. O <xref:System.Security.Cryptography.SymmetricAlgorithm.CreateDecryptor%2A?displayProperty=nameWithType> método da <xref:System.Security.Cryptography.Aes> instância passa o valor de IV e a mesma chave usada para criptografia.

```vb
Dim aes As Aes = Aes.Create()
Dim cryptStream As New CryptoStream(myStream, aes.CreateDecryptor(key, iv), CryptoStreamMode.Read)
```

```csharp
Aes aes = Aes.Create();
CryptoStream cryptStream = new CryptoStream(myStream, aes.CreateDecryptor(key, iv), CryptoStreamMode.Read);
```

O exemplo a seguir mostra todo o processo de criação de um fluxo, descriptografia do fluxo, leitura a partir do fluxo e fechamento dos fluxos. Um objeto de fluxo de arquivo é criado e lê um arquivo chamado *TestData.txt*. O fluxo de arquivo é então descriptografado usando a classe **CryptoStream** e a classe **AES** . Este exemplo especifica o valor de chave que é usado no exemplo de criptografia simétrica para [criptografar dados](encrypting-data.md). Ele não mostra o código necessário para criptografar e transferir esses valores.

:::code language="csharp" source="snippets/decrypting-data/csharp/aes-decrypt.cs":::
:::code language="vb" source="snippets/decrypting-data/vb/aes-decrypt.vb":::

O exemplo anterior usa a mesma chave e o algoritmo usado no exemplo de criptografia simétrica para [criptografar dados](encrypting-data.md). Ele descriptografa o arquivo de *TestData.txt* que é criado por esse exemplo e exibe o texto original no console.

## <a name="asymmetric-decryption"></a>Descriptografia assimétrica

Normalmente, uma entidade (parte A) gera uma chave pública e privada e armazena a chave na memória ou em um contêiner de chave de criptografia. Em seguida, a parte a envia a chave pública para outra parte (parte B). Usando a chave pública, a parte B criptografa dados e envia os dados de volta para a parte A. Depois de receber os dados, A parte A descriptografa usando a chave privada que corresponde. A descriptografia será bem-sucedida somente se a parte A usar a chave privada que corresponde à parte da chave pública B usada para criptografar os dados.

Para obter informações sobre como armazenar uma chave assimétrica no contêiner de chave criptográfica segura e como recuperar posteriormente a chave assimétrica, consulte [como armazenar chaves assimétricas em um contêiner de chave](how-to-store-asymmetric-keys-in-a-key-container.md).

O exemplo a seguir ilustra a descriptografia de duas matrizes de bytes que representam uma chave simétrica e um IV. Para obter informações sobre como extrair a chave pública assimétrica do <xref:System.Security.Cryptography.RSA> objeto em um formato que você pode enviar facilmente a terceiros, consulte [Criptografando dados](encrypting-data.md).

```vb
'Create a new instance of the RSA class.
Dim rsa As RSA = RSA.Create()

' Export the public key information and send it to a third party.
' Wait for the third party to encrypt some data and send it back.

'Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, RSAEncryptionPadding.Pkcs1)
symmetricIV = rsa.Decrypt(encryptedSymmetricIV, RSAEncryptionPadding.Pkcs1)
```

```csharp
//Create a new instance of the RSA class.
RSA rsa = RSA.Create();

// Export the public key information and send it to a third party.
// Wait for the third party to encrypt some data and send it back.

//Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, RSAEncryptionPadding.Pkcs1);
symmetricIV = rsa.Decrypt(encryptedSymmetricIV , RSAEncryptionPadding.Pkcs1);
```

## <a name="see-also"></a>Confira também

- [Gerando chaves para criptografia e descriptografia](generating-keys-for-encryption-and-decryption.md)
- [Criptografando dados](encrypting-data.md)
- [Serviços criptográficos](cryptographic-services.md)
- [Modelo de criptografia](cryptography-model.md)
- [Criptografia de plataforma cruzada](cross-platform-cryptography.md)
- [Vulnerabilidades de temporização com descriptografia simétrica no modo CBC usando preenchimento](vulnerabilities-cbc-mode.md)
- [Proteção de dados do ASP.NET Core](/aspnet/core/security/data-protection/introduction)
