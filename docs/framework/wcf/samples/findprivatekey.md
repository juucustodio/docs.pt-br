---
description: 'Saiba mais sobre: exemplo de FindPrivateKey'
title: Exemplo de FindPrivateKey
ms.date: 12/04/2017
helpviewer_keywords:
- FindPrivateKey
ms.assetid: 16b54116-0ceb-4413-af0c-753bb2a785a6
ms.openlocfilehash: 0e876aa3e1f6dde16acbb3ddd2a130ad49d369fc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732417"
---
# <a name="findprivatekey-sample"></a>Exemplo de FindPrivateKey

Pode ser difícil encontrar o local e o nome do arquivo de chave privada associado a um certificado X. 509 específico no repositório de certificados. A ferramenta FindPrivateKey.exe facilita esse processo.

> [!IMPORTANT]
> FindPrivateKey é um exemplo que precisa ser compilado antes do uso. Consulte a seção [para criar o projeto FindPrivateKey](#to-build-the-findprivatekey-project) para obter instruções sobre como criar a ferramenta FindPrivateKey.

Os certificados X. 509 são instalados por um administrador ou qualquer usuário no computador. No entanto, o certificado pode ser acessado por um serviço em execução em uma conta diferente. Por exemplo, a conta de serviço de rede.

Essa conta pode não ter acesso ao arquivo de chave privada porque o certificado não foi instalado originalmente. A ferramenta FindPrivateKey fornece o local de um determinado arquivo de chave privada do certificado X. 509. Você pode adicionar permissões ou remover permissões para esse arquivo quando souber o local do arquivo de chave privada de certificados X. 509 específico.

Os exemplos que usam certificados para segurança usam a ferramenta FindPrivateKey no arquivo *Setup.bat* . Depois que o arquivo de chave privada for encontrado, você poderá usar outras ferramentas, como *Cacls.exe* , para definir os direitos de acesso apropriados no arquivo.

Ao executar um serviço de Windows Communication Foundation (WCF) em uma conta de usuário, como um executável auto-hospedado, verifique se a conta de usuário tem acesso somente leitura ao arquivo. Ao executar um serviço WCF em Serviços de Informações da Internet (IIS), as contas padrão nas quais o serviço é executado são o serviço de rede no IIS 7 e versões anteriores, ou a identidade do pool de aplicativos no IIS 7,5 e versões posteriores. Para obter mais informações, consulte [identidades do pool de aplicativos](/iis/manage/configuring-security/application-pool-identities).

## <a name="examples"></a>Exemplos

Ao acessar um certificado para o qual o processo não tem privilégio de leitura, você verá uma mensagem de exceção semelhante ao exemplo a seguir:

```output
System.ArgumentException was unhandled
Message="The certificate 'CN=localhost' must have a private key that is capable of key exchange.  The process must have access rights for the private key."
Source="System.ServiceModel"
```

Quando isso ocorrer, use a ferramenta FindPrivateKey para localizar o arquivo de chave privada e, em seguida, defina o direito de acesso para o processo em que o serviço está sendo executado. Por exemplo, isso pode ser feito com a ferramenta de Cacls.exe, conforme mostrado no exemplo a seguir:

```console
cacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /E /G "NETWORK SERVICE":R
```

#### <a name="to-build-the-findprivatekey-project"></a>Para criar o projeto FindPrivateKey

Para baixar o projeto, visite [exemplos de Windows Communication Foundation (WCF) e Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459).

1. Abra o explorador de arquivos e navegue até a pasta *WF_WCF_Samples \wcf\setup\findprivatekey\cs* no local do diretório em que você instalou o exemplo.

2. Clique duas vezes no ícone de arquivo. sln para abrir o arquivo no Visual Studio.

3. No menu **Compilar** , selecione **Recompilar solução**.

4. A criação da solução gera o arquivo: FindPrivateKey.exe.

## <a name="conventionscommand-line-entries"></a>Convenções — entradas de linha de comando

 "[*Option*]" representa um conjunto opcional de parâmetros.

 "{*Option*}" representa um conjunto obrigatório de parâmetros.

 "*opção 1* &#124; *opção 2*" representa uma opção entre conjuntos de opções.

 " \<*value*> " representa um valor de parâmetro a ser inserido.

## <a name="usage"></a>Uso

```console
FindPrivateKey <storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]
```

Em que:

| Parâmetro         | Descrição                                                                       |
|-----------------|-----------------------------------------------------------------------------------|
| `<subjectName>` | O nome do assunto do certificado                                               |
| `<thumbprint>`  | A impressão digital do certificado (você pode usar a ferramenta de Certmgr.exe para encontrá-la) |
| `-f`            | somente nome do arquivo de saída                                                             |
| `-d`            | somente diretório de saída                                                             |
| `-a`            | nome de arquivo de saída absoluto                                                         |

Se nenhum parâmetro for especificado no prompt de comando, o texto de ajuda com essas informações será exibido.

## <a name="examples"></a>Exemplos

Este exemplo localiza o nome de arquivo do certificado com um nome de assunto "CN = localhost", no repositório pessoal do usuário atual.

```console
FindPrivateKey My CurrentUser -n "CN=localhost"
```

Este exemplo localiza o nome do arquivo do certificado com um nome de assunto "CN = localhost", no repositório pessoal do usuário atual e gera o caminho completo do diretório.

```console
FindPrivateKey My CurrentUser -n "CN=localhost" -a
```

Este exemplo localiza o nome de arquivo do certificado com uma impressão digital de "03 33 98 63 D0 47 E7 48 71 33 62 64 76 5C 4C 9d 42 1D 6B 52", no repositório pessoal do computador local.

```console
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52"
```
