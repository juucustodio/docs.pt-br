---
title: Infraestrutura como código
description: Adotando a infraestrutura como código (IaC) com aplicativos nativos de nuvem
ms.date: 05/13/2020
ms.openlocfilehash: d130705e19e0d3d7a9e15c73f4758a22ee8ecd43
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91163733"
---
# <a name="infrastructure-as-code"></a>Infraestrutura como código

Os sistemas nativos de nuvem adotam microserviços, contêineres e design de sistema moderno para atingir velocidade e agilidade. Eles fornecem estágios automatizados de Build e versão para garantir o código consistente e de qualidade. Mas isso é apenas parte da história. Como provisionar os ambientes de nuvem nos quais esses sistemas são executados?

Os aplicativos nativos de nuvem modernos adotam a prática amplamente aceita da [Infraestrutura como código](/azure/devops/learn/what-is-infrastructure-as-code)ou `IaC` .  Com o IaC, você automatiza o provisionamento de plataforma. Essencialmente, você aplica práticas de engenharia de software, como teste e controle de versão, às suas práticas de DevOps. Sua infraestrutura e implantações são automatizadas, consistentes e reproduzíveis. Assim como a entrega contínua automatizada do modelo tradicional de implantações manuais, a infraestrutura como código (IaC) está evoluindo como os ambientes de aplicativos são gerenciados.

Ferramentas como Azure Resource Manager (ARM), Terraform e a CLI (interface de linha de comando) do Azure permitem gerar um script de forma declarativa para a infraestrutura de nuvem necessária.

## <a name="azure-resource-manager-templates"></a>Modelos do Azure Resource Manager

ARM significa [Azure Resource Manager](/azure/azure-resource-manager/management/overview). É um mecanismo de provisionamento de API que é incorporado ao Azure e exposto como um serviço de API. O ARM permite que você implante, atualize, exclua e gerencie os recursos contidos no grupo de recursos do Azure em uma única operação coordenada. Você fornece ao mecanismo um modelo baseado em JSON que especifica os recursos necessários e sua configuração. O ARM orquestra automaticamente a implantação na ordem correta que respeita as dependências. O mecanismo garante Idempotência. Se um recurso desejado já existir com a mesma configuração, o provisionamento será ignorado.

Os modelos de Azure Resource Manager são uma linguagem baseada em JSON para definir vários recursos no Azure. O esquema básico é semelhante a Figura 10-14.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "",
  "apiProfile": "",
  "parameters": {  },
  "variables": {  },
  "functions": [  ],
  "resources": [  ],
  "outputs": {  }
}
```

**Figura 10-14** -o esquema para um modelo do Resource Manager

Nesse modelo, é possível definir um contêiner de armazenamento dentro da seção de recursos da seguinte forma:

```json
"resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "location": "[parameters('location')]",
      "apiVersion": "2018-07-01",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "StorageV2",
      "properties": {}
    }
  ],
```

**Figura 10-15** -um exemplo de uma conta de armazenamento definida em um modelo do Resource Manager

Um modelo de ARM pode ser parametrizado com informações de ambiente dinâmico e configuração. Isso permite que ele seja reutilizado para definir ambientes diferentes, como desenvolvimento, p e r ou produção. Normalmente, o modelo cria todos os recursos em um único grupo de recursos do Azure. É possível definir vários grupos de recursos em um único modelo do Resource Manager, se necessário. Você pode excluir todos os recursos em um ambiente excluindo o próprio grupo de recursos. A análise de custo também pode ser executada no nível do grupo de recursos, permitindo uma rápida contabilidade de quanto cada ambiente está custando.

Há muitos exemplos ou modelos de ARM disponíveis no projeto de [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) no github. Eles podem ajudar a acelerar a criação de um novo modelo ou a modificação de um existente.

Os modelos do Resource Manager podem ser executados de várias maneiras. Talvez a maneira mais simples seja simplesmente colá-las no portal do Azure. Para implantações experimentais, esse método pode ser rápido. Eles também podem ser executados como parte de um processo de compilação ou versão no Azure DevOps. Há tarefas que usarão conexões no Azure para executar os modelos. As alterações nos modelos do Resource Manager são aplicadas incrementalmente, o que significa que, para adicionar um novo recurso, é necessário apenas adicioná-lo ao modelo. As ferramentas irão reconciliar as diferenças entre os recursos atuais e os definidos no modelo. Os recursos serão criados ou alterados para que correspondam ao que está definido no modelo.  

## <a name="terraform"></a>Terraform

Em geral, os aplicativos nativos da nuvem são construídos `cloud agnostic` . Sendo assim, isso significa que o aplicativo não está rigidamente acoplado a um fornecedor de nuvem específico e pode ser implantado em qualquer nuvem pública.

O [Terraform](https://www.terraform.io/) é uma ferramenta de modelagem de negócios que pode provisionar aplicativos nativos de nuvem em todos os principais players de nuvem: Azure, Google Cloud Platform, AWS e o antiicloud. Em vez de usar JSON como a linguagem de definição de modelo, ele usa o YAML ligeiramente mais conciso.

Um arquivo Terraform de exemplo que faz o mesmo que o modelo do Resource Manager anterior (Figura 10-15) é mostrado na Figura 10-16:

```terraform
provider "azurerm" {
  version = "=1.28.0"
}

resource "azurerm_resource_group" "test" {
  name     = "production"
  location = "West US"
}

resource "azurerm_storage_account" "testsa" {
  name                     = "${var.storageAccountName}"
  resource_group_name      = "${azurerm_resource_group.testrg.name}"
  location                 = "${var.region}"
  account_tier             = "${var.tier}"
  account_replication_type = "${var.replicationType}"

}
```

**Figura 10-16** -um exemplo de um modelo do Resource Manager

O Terraform também fornece mensagens de erro intuitivas para modelos de problemas. Também há uma tarefa de validação prática que pode ser usada na fase de compilação para detectar erros de modelo no início.

Assim como acontece com os modelos do Resource Manager, as ferramentas de linha de comando estão disponíveis para implantar modelos Terraform. Também há tarefas criadas pela Comunidade no Azure Pipelines que podem validar e aplicar modelos Terraform.

Às vezes, os modelos Terraform e ARM geram valores significativos, como uma cadeia de conexão para um banco de dados recém-criado. Essas informações podem ser capturadas no pipeline de compilação e usadas em tarefas subsequentes.

## <a name="azure-cli-scripts-and-tasks"></a>CLI do Azure scripts e tarefas

Por fim, você pode aproveitar [CLI do Azure](/cli/azure/) para gerar um script declarativa de sua infraestrutura de nuvem. CLI do Azure scripts podem ser criados, encontrados e compartilhados para provisionar e configurar quase todos os recursos do Azure. A CLI é simples de usar com uma curva de aprendizado de AdaBoost. Os scripts são executados no PowerShell ou bash. Eles também são simples de depurar, especialmente quando comparados com modelos ARM.

CLI do Azure scripts funcionam bem quando você precisa desmontar e reimplantar sua infraestrutura. A atualização de um ambiente existente pode ser complicada. Muitos comandos da CLI não são idempotentes. Isso significa que eles recriarão o recurso toda vez que forem executados, mesmo que o recurso já exista. Sempre é possível adicionar código que verifica a existência de cada recurso antes de criá-lo. Mas, ao fazer isso, seu script pode ficar inflado e difícil de gerenciar.

Esses scripts também podem ser inseridos em pipelines do Azure DevOps como `Azure CLI tasks` . A execução do pipeline invoca o script.

A Figura 10-17 mostra um trecho de código YAML que lista a versão do CLI do Azure e os detalhes da assinatura. Observe como CLI do Azure comandos são incluídos em um script embutido.

```yaml
- task: AzureCLI@2
  displayName: Azure CLI
  inputs:
    azureSubscription: <Name of the Azure Resource Manager service connection>
    scriptType: ps
    scriptLocation: inlineScript
    inlineScript: |
      az --version
      az account show
```

**Figura 10-17** -CLI do Azure script

No artigo, [o que é infraestrutura como código](/azure/devops/learn/what-is-infrastructure-as-code), autor Sam Guckenheimer descreve como "as equipes que implementam o IaC podem fornecer ambientes estáveis rapidamente e em escala. As equipes evitam a configuração manual de ambientes e impõem a consistência, representando o estado desejado de seus ambientes por meio de código. Implantações de infraestrutura com IaC são repetíveis e evitam problemas de tempo de execução causados por descompasso de configuração ou dependências ausentes. As equipes do DevOps podem trabalhar junto com um conjunto unificado de práticas e ferramentas para fornecer aplicativos e sua infraestrutura de suporte de forma rápida, confiável e em escala. "

>[!div class="step-by-step"]
>[Anterior](feature-flags.md) 
> [Avançar](application-bundles.md)
