---
description: 'Saiba mais sobre: ferramentas'
title: Ferramentas
ms.date: 03/30/2017
ms.assetid: 89c907f9-313f-408c-992a-631f1eadf1da
ms.openlocfilehash: 1400cee5c626f015d5b9a6efcd9c04411f0ba4f6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686122"
---
# <a name="tools"></a>Ferramentas

Este tópico lista todas as exceções geradas pelas ferramentas do Windows Communication Foundation (WCF).

## <a name="exception-list"></a>Lista de exceções

|Código do recurso|Cadeia de caracteres de recurso|
|-------------------|---------------------|
|ParametersTarget|\<enum>|
|ParametersToolConfig|\<configFile>|
|ErrInvalidPath|O especificado é um caminho inválido. Verifique o argumento especificado.|
|ParametersReference|\<file path>|
|WrnCannotLoadConfigFileForValidation|Ocorreu um erro ao processar o arquivo de configuração carregado a partir do local especificado. Os serviços que estão definidos neste arquivo de configuração não podem ser validados.|
|MoreHelp|Para obter mais ajuda, digite "SvcUtil" com os argumentos especificados.|
|HelpMergeConfig|Faz com que a configuração gerada seja mesclada em um arquivo existente em vez de substituir o arquivo existente.|
|ErrCannotWriteFile|Não é possível gravar em um arquivo de saída.|
|ErrInvalidNamespaceArgument|O valor inválido especificado foi passado para a opção especificada. Especifique um namespace de destino separado por vírgula e um par de namespaces CLR.|
|HelpImportXmlType|Configura o serializador DataContract para importar tipos não DataContract como tipos IXmlSerializable.|
|ErrExclusiveOptionsSpecified|A opção especificada não pode ser usada quando a outra opção especificada tiver sido especificada.|
|WrnHttpGetFailed|Erro HTTP GET com o URI especificado.|
|ErrInputFileNotAssemblyOrMetadata|O arquivo no local especificado lido por meio do argumento de entrada especificado não parece ser um arquivo de metadados XML ou um assembly válido.|
|WrnUnknownMetadataFound|Não é possível salvar o documento de metadados não reconhecido do tipo especificado.|
|ErrDirectoryContainsInvalidCharacters|O valor inválido especificado foi passado para a opção especificada. O caractere especificado não é permitido em um caminho.|
|WrnCannotResolveServiceForValidation|Não é possível carregar um serviço com o ConfigName especificado. Para validar um serviço, forneça o assembly que contém o tipo de serviço e um executável com a configuração para esse serviço.|
|ErrUnexpectedValue|A opção especificada não oferece suporte a nenhum valor.|
|#InvalidArg|O especificado contém um argumento inválido.|
|ParametersExcludeType|\<type>|
|HelpXmlSerializer|Gerar tipos de dados que usam o XmlSerializer para serialização e desserialização.|
|#|---------------------------------------------------------------------------------------------------------------------=|
|ErrUnexpectedError|Ocorreu um erro na ferramenta.|
|HelpNologo|A mensagem de direitos autorais e de cabeçalho é suprimida.|
|ErrInputConflictsWithTarget|O tipo de entrada lida do especificado não tem suporte com a opção especificada definida para o valor especificado.|
|WrnCannotLoadServiceForExport|Ocorreu um erro ao carregar o tipo de serviço a ser exportado.|
|HelpMetadataDownloadCategory|-= DOWNLOAD DE METADADOS =-|
|WrnNoServiceContractTypes|Não é possível gerar tipos de XmlSerializer para o assembly especificado. Nenhum tipo de contrato de serviço foi encontrado.|
|WrnCouldNotLoadTypesFromReferenceAssemblyAt|Ocorreu um erro ao carregar tipos em um assembly que foi carregado a partir do especificado. Alguns tipos no assembly não podem ser carregados e estão indisponíveis para a ferramenta.|
|ErrDirectoryPointsToAFile|O valor inválido especificado foi passado para a opção especificada. O valor especificado é um caminho para um arquivo.|
|Erro do|Erro:|
|ErrDuplicateReferenceValues|O assembly especificado foi carregado duas vezes usando a opção especificada. Um assembly só pode ser referenciado uma vez.|
|WrnNoXmlSerializerOperationBehavior|Não é possível gerar XmlSerializer para o assembly especificado. Nenhum contrato de serviço no assembly tem uma operação com XmlSerializerOperationBehavior.|
|ErrCannotCreateDirectory|Não é possível criar o diretório especificado.|
|ErrCouldNotLoadTypesFromAssemblyAt|Não é possível carregar nenhum tipo no assembly especificado.|
|ErrUnknownSwitch|O comutador especificado é uma opção não reconhecida.|
|Logotipo|O logotipo da ferramenta é "ferramenta de metadados do Microsoft® Service Model" com a versão.|
|NoCodeWasGenerated|Nenhum código foi gerado.<br /><br /> Se você estiver tentando gerar um cliente, isso pode ser porque os documentos de metadados não continham nenhum contrato ou serviço válido<br /><br /> ou porque todos os contratos/serviços foram descobertos para existir em assemblies de referência. Verifique se você passou todos os documentos de metadados para a ferramenta.|
|WrnUnableToLoadContractForSGen|Ocorreu um erro ao carregar um tipo de contrato. Não é possível gerar o tipo de XmlSerializer para este contrato. O tipo e os detalhes são especificados.|
|WrnOptionConflictsWithInput|A opção especificada não pode ser usada com vários assemblies de entrada. A opção especificada é ignorada.|
|ErrUnableToImportMetadata|Ocorreu um erro crítico ao tentar importar metadados.|
|ErrInvalidSerializer|Um valor de serializador inválido foi passado para a opção especificada. Os serializadores com suporte são especificados.|
|SavingDownloadedMetadata|Salvando arquivos de metadados baixados...|
|WrnNoConfigForServices|Nenhum dos assemblies passados foram executáveis com o arquivo de configuração ou nenhum dos arquivos de configuração continha serviços com o nome de configuração especificado.|
|ErrInputConflictsWithOption|A entrada lida do especificado não pode ser usada com a opção especificada porque elas implicam modos diferentes de operação de ferramenta.|
|ErrUnableToExportEndpoints|Ocorreu um erro ao exportar o tipo de serviço especificado.|
|ErrInputSchemaParseError|Ocorreu um erro de análise de esquema XML ao ler o especificado. Verifique se o XML está bem formado e é válido.|
|ErrInputPolicyParseError|Ocorreu um erro de análise de WS-Policy ao ler o especificado. Verifique se o XML está bem formado e é válido.|
|ErrUnableToLoadReferenceType|Ocorreu um erro ao carregar um tipo de contrato referenciado. Esse tipo especificado é ignorado.|
|WrnCannotLoadServiceForValidation|Ocorreu um erro ao carregar o serviço a ser validado. O tipo e os detalhes são especificados.|
|HelpCodeGenerationCategory|-= GERAÇÃO DE CÓDIGO =-|
|RetreivingMetadataWithMexAndDisco|Tentativa de baixar metadados do especificado usando WS-Metadata Exchange ou DISCO.|
|ErrGeneralSchemaValidation|Ocorreu um erro ao verificar os esquemas XML que foram gerados durante a exportação.|
|ParametersDirectory|\<directory>|
|ErrCannotLoadSpecifiedType|Nenhum tipo pode ser carregado para o valor especificado que foi passado para a opção especificada. Verifique se o assembly ao qual este tipo pertence é especificado usando a opção especificada.|
|ErrOptionModeConflict|A opção especificada não pode ser usada com a opção especificada porque elas implicam tipos de saída diferentes.|
|ErrIsNotAnAssembly|Não é possível carregar o especificado como um assembly. Verifique se esse arquivo é um assembly .NET.|
|ErrInputConflictsWithMode|A entrada lida do especificado é inconsistente com outras opções.|
|ErrDuplicateValuePassedToTypeArg|O valor especificado foi passado para a opção especificada várias vezes. Cada tipo pode ser especificado apenas uma vez.|
|ErrInputEPRFileParseError|Não é possível ler a referência do ponto de extremidade do especificado. Verifique se o XML está bem formado e é válido.|
|ErrCouldNotCreateCodeProvider|Não é possível criar um provedor de código para o valor especificado que foi passado para o {1} argumento/. Verifique se o provedor de código está instalado e configurado corretamente.|
|ErrPathTooLongDirOnly|O caminho especificado resultante é muito longo. Examine o argumento especificado.|
|HelpDataContractSerializer|Gerar tipos de dados que usam o serializador DataContract para serialização e desserialização.|
|ErrUnableToExportEndpoint|Ocorreu um erro ao exportar o nome do ponto de extremidade especificado no namespace especificado no tipo de serviço especificado encontrado no arquivo de configuração carregado para o assembly.|
|HelpUsage1|Exibe o uso da ajuda.|
|HelpUsage2|Exibe o uso da ajuda.|
|HelpUsage3|Exibe o uso da ajuda.|
|HelpUsage4|Exibe o uso da ajuda.|
|HelpUsage5|Exibe o uso da ajuda.|
|ErrDirectoryNotFound|O diretório especificado não pode ser encontrado. Verifique se o diretório existe e se você tem as permissões apropriadas para lê-lo.|
|ErrUnableToLoadFile|Não é possível ler o arquivo especificado.|
|ErrNoFilesFound|O caminho de entrada especificado não parece se referir a nenhum arquivo existente.|
|ParametersConfig|\<configFile>|
|ErrDirectoryInsteadOfFile|O caminho de entrada especificado parece ser um diretório. A entrada deve ser URLs ou caminhos de arquivo.|
|HelpConfig|Instrui as ferramentas para gerar um arquivo de configuração com o nome fornecido. Padrão: output.config.|
|ErrSingleUseSwitch|A opção especificada não pode ser especificada várias vezes.|
|Aviso|Aviso:|
|WrnAmbiguousServiceConfig|Várias configurações de serviço foram encontradas com o nome de configuração especificado; os assemblies a seguir foram especificados.|
|ErrInvalidInputPath|O caminho de entrada especificado não parece fazer referência a nenhum arquivo existente e parece não ser um URI válido.|
|ErrUnableToLoadInputs|Ocorreu um erro ao ler os metadados carregados.|
|GeneratingSerializer|Gerando serializadores XML...|
|HelpToolConfig|Arquivo de configuração personalizada a ser usado no lugar do arquivo de configuração do aplicativo. Isso pode ser usado para alterar a configuração de metadados ou registrar extensões de configuração sem alterar o arquivo de configuração da ferramenta.|
|ErrValidateInvalidUse|A opção especificada não pode ser usada com a opção especificada.|
|WrnWSMExFailed|WS-Metadata erro do Exchange com o URI especificado.|
|HelpNoconfig|Não gerar configuração.|
|HelpCodeGenerationDescription|O especificado pode gerar contratos de serviço, clientes e tipos de dados de documentos de metadados.|
|HelpTargetMetadata|Metadados de saída. Se a entrada for uma URL, Svcutil.exe salvará os metadados em disco e não gerará código. Se a entrada for um ou mais assemblies, Svcutil.exe gerará metadados de tipos nos assemblies.|
|ErrAmbiguousOptionModeConflict|A opção especificada está em conflito com outras opções. Examine o uso da ferramenta.|
|ErrNotLanguageOrCodeDomType|O valor especificado que foi passado para o argumento especificado não representa uma linguagem definida e não pode ser carregado como um tipo CLR totalmente qualificado.|
|ErrUnableToUniquifyFilename|Não é possível criar o nome de arquivo de saída. Muitos arquivos estão sendo criados com o prefixo especificado.|
|ErrCannotCreateFile|Não é possível criar o arquivo de saída especificado.|
|ErrExpectedValue|A opção especificada requer que um valor seja especificado.|
|ErrCannotDisambiguateSpecifiedTypes|Existe mais de um tipo com o mesmo nome no conjunto de assemblies referenciados. Use nomes qualificados por assembly para distinguir entre os tipos especificados para a opção especificada.|
|RetreivingMetadataWithMexOnly|Tentativa de baixar metadados do local especificado usando o WS-Metadata Exchange. Esta URL não dá suporte a DISCO.|
|ErrInvalidTarget|O destino especificado é inválido quando especificado usando a opção especificada. Os destinos com suporte são especificados.|
|ErrPathTooLong|O caminho resultante é muito longo. Examine os argumentos especificados.|
|HelpCommonOptionsCategory|-= OPÇÕES COMUNS =-|
|ParametersServiceName|\<serviceConfigName>|
|ErrNoValidInputFilesSpecified|Nenhum arquivo de entrada válido especificado. Especifique documentos de metadados ou arquivos de assembly.|
|ParametersLanguage|\<language>|
|ErrUnableToLoadMetadataDocument|Ocorreu um erro ao ler os metadados de um dos documentos carregados. O identificador do documento foi especificado.|
|ErrConflictingInputs|O argumento de entrada especificado está em conflito com o especificado porque eles implicam modos diferentes de operação de ferramenta.|
|WrnUnableToLoadContractForValidation|Ocorreu um erro ao carregar um tipo de contrato. O tipo e os detalhes são especificados.|
|WrnAttributeReflectionErrors|Falha na reflexão do atributo para alguns dos tipos no assembly que foram carregados a partir do especificado. Verifique se esse assembly pode ser carregado a partir desse local com os privilégios de segurança corretos.|
|HelpMetadataExportCategory|-= EXPORTAÇÃO DE METADADOS =-|
|HelpValidationCategory|-= VALIDAÇÃO DE SERVIÇO =-|
|ValidationError|Erro de validação:|
|GeneratingFiles|Gerando arquivos...|
|ErrCannotSpecifyMultipleMappingsForNamespace|Um valor inválido foi passado para a opção especificada. O namespace de destino especificado não pode ser mapeado para vários namespaces CLR, conforme especificado.|
|ErrCouldNotLoadReferenceAssemblyAt|Não é possível carregar o assembly de referência especificado.|
|Parâmetros de logoff|\<file>|
|NoCodeWasGeneratedSuggestDCOnly|Para gerar contratos a partir dos esquemas, use a opção especificada.|
|ErrUnableToLoadInputConfig|Não é possível carregar o arquivo de configuração especificado.|
|ErrUnexpectedDelimiter|Um delimitador de argumento inválido (': ' ou ' = ') não pode iniciar a opção.|
|ErrMergeConfigUsedWithoutConfig|Não é possível usar a opção especificada sem especificar a outra opção especificada.|
|ErrUnableToExportContract|Ocorreu um erro ao exportar o contrato carregado do tipo especificado.|
|GeneratingMetadata|Gerando arquivos de metadados...|
|ErrNotCodeDomType|O tipo especificado que foi passado para o argumento especificado não é da classe derivada especificada.|
|WrnNoTypeForServices|Nenhum dos assemblies que foram passados continha tipos de serviço com o nome de configuração especificado.|
|ErrAssemblyLoadFailed|Não é possível carregar o arquivo especificado como um assembly. Verifique o FusionLogs para obter mais informações.|
|NoMetadataWasGenerated|Nenhum arquivo de metadados foi gerado. Nenhum contrato de serviço foi exportado.<br /><br /> Para exportar um serviço, use a opção especificado. Para exportar contratos de dados, especifique a opção.|
|WrnCannotResolveServiceForExport|Não é possível carregar um serviço com o ConfigName especificado. Para exportar um serviço, forneça o assembly que contém o tipo de serviço e um executável com configuração para esse serviço.|
|ParametersCollectionType|\<type>|
|ErrOptionConflictsWithTarget|Não há suporte para o uso da opção especificada com a opção especificada definida para o valor especificado.|
|ErrCodegenError|Ocorreu um erro ao gerar o código no idioma especificado.<br /><br /> O idioma não dá suporte a todos os elementos de código que estão sendo gerados. Outra linguagem deve ser usada.|
|ErrInputWsdlParseError|Ocorreu um erro de análise de WSDL ao ler o especificado. Verifique se o XML está bem formado e é válido.|
|ErrCouldNotCreateInstance|Não é possível criar uma instância do tipo especificado que foi passado para o argumento especificado.|
|ParametersNamespace|\<string,string>|
|HelpNostdlib|Não referencie bibliotecas padrão (por padrão mscorlib.dll e system.servicemodel.dll são referenciados.)|
|WrnCannotLoadConfigFileForExport|Ocorreu um erro ao processar o arquivo de configuração que foi carregado a partir do especificado. Os serviços que estão definidos neste arquivo de configuração não podem ser carregados.|
|WrnUnableToLoadContractForExport|Ocorreu um erro ao carregar um tipo de contrato. Esse tipo especificado não pode ser exportado.|
