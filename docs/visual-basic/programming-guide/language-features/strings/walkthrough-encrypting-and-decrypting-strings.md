---
description: 'Saiba mais sobre: Walkthrough: criptografar e descriptografar cadeias de caracteres em Visual Basic'
title: criptografar e descriptografar cadeias de caracteres
ms.date: 07/20/2015
helpviewer_keywords:
- encryption [Visual Basic], strings
- strings [Visual Basic], encrypting
- decryption [Visual Basic], strings
- strings [Visual Basic], decrypting
ms.assetid: 1f51e40a-2f88-43e2-a83e-28a0b5c0d6fd
ms.openlocfilehash: afc1eeaec85b2e430aead7f16401289b6e2e9e49
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100471078"
---
# <a name="walkthrough-encrypting-and-decrypting-strings-in-visual-basic"></a>Instruções passo a passo: criptografando e descriptografando cadeias de caracteres no Visual Basic

Este tutorial mostra como usar a <xref:System.Security.Cryptography.DESCryptoServiceProvider> classe para criptografar e descriptografar cadeias de caracteres usando a versão do CSP (provedor de serviços de criptografia) do algoritmo padrão de criptografia de dados triplo ( <xref:System.Security.Cryptography.TripleDES> ). A primeira etapa é criar uma classe wrapper simples que encapsula o algoritmo 3DES e armazena os dados criptografados como uma cadeia de caracteres codificada em base 64. Em seguida, esse wrapper é usado para armazenar com segurança dados de usuário privados em um arquivo de texto publicamente acessível.  
  
 Você pode usar a criptografia para proteger os segredos do usuário (por exemplo, senhas) e tornar as credenciais ilegíveis para usuários não autorizados. Isso pode proteger a identidade de um usuário autorizado de ser roubado, o que protege os ativos do usuário e fornece não-repúdio. A criptografia também pode proteger os dados de um usuário de serem acessados por usuários não autorizados.  
  
 Para obter mais informações, consulte [Serviços Criptográficos](../../../../standard/security/cryptographic-services.md).  
  
> [!IMPORTANT]
> Os algoritmos Rijndael (agora chamados de criptografia AES [AES]) e 3DES (Triple Data Encryption Standard) fornecem maior segurança do que o DES, pois são mais intensivas em computação. Para obter mais informações, consulte <xref:System.Security.Cryptography.DES> e <xref:System.Security.Cryptography.Rijndael>.  
  
### <a name="to-create-the-encryption-wrapper"></a>Para criar o wrapper de criptografia  
  
1. Crie a `Simple3Des` classe para encapsular os métodos de criptografia e descriptografia.  
  
     [!code-vb[VbVbalrStrings#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#38)]  
  
2. Adicione uma importação do namespace de criptografia ao início do arquivo que contém a `Simple3Des` classe.  
  
     [!code-vb[VbVbalrStrings#77](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#77)]  
  
3. Na `Simple3Des` classe, adicione um campo particular para armazenar o provedor de serviços criptográficos 3DES.  
  
     [!code-vb[VbVbalrStrings#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#39)]  
  
4. Adicione um método particular que cria uma matriz de bytes de um comprimento especificado a partir do hash da chave especificada.  
  
     [!code-vb[VbVbalrStrings#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#41)]  
  
5. Adicione um construtor para inicializar o provedor de serviços criptográficos 3DES.  
  
     O `key` parâmetro controla os `EncryptData` `DecryptData` métodos e.  
  
     [!code-vb[VbVbalrStrings#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#40)]  
  
6. Adicione um método público que criptografa uma cadeia de caracteres.  
  
     [!code-vb[VbVbalrStrings#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#42)]  
  
7. Adicione um método público que descriptografa uma cadeia de caracteres.  
  
     [!code-vb[VbVbalrStrings#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#43)]  
  
     A classe wrapper agora pode ser usada para proteger ativos do usuário. Neste exemplo, ele é usado para armazenar com segurança dados de usuário privados em um arquivo de texto publicamente acessível.  
  
### <a name="to-test-the-encryption-wrapper"></a>Para testar o wrapper de criptografia  
  
1. Em uma classe separada, adicione um método que usa o método do wrapper `EncryptData` para criptografar uma cadeia de caracteres e gravá-la na pasta meus documentos do usuário.  
  
     [!code-vb[VbVbalrStrings#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#78)]  
  
2. Adicione um método que leia a cadeia de caracteres criptografada da pasta meus documentos do usuário e descriptografe a cadeia de caracteres com o método do wrapper `DecryptData` .  
  
     [!code-vb[VbVbalrStrings#79](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class3.vb#79)]  
  
3. Adicione o código de interface do usuário para chamar os `TestEncoding` `TestDecoding` métodos e.  
  
4. Execute o aplicativo.  
  
     Ao testar o aplicativo, observe que ele não descriptografará os dados se você fornecer a senha incorreta.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Security.Cryptography>
- <xref:System.Security.Cryptography.DESCryptoServiceProvider>
- <xref:System.Security.Cryptography.DES>
- <xref:System.Security.Cryptography.TripleDES>
- <xref:System.Security.Cryptography.Rijndael>
- [Serviços criptográficos](../../../../standard/security/cryptographic-services.md)
