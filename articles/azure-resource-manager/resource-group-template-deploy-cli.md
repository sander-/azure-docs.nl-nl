---
title: Resources implementeren met Azure CLI en een sjabloon | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure CLI om een resources implementeren op Azure. De resources zijn gedefinieerd in een Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/14/2018
ms.author: tomfitz
ms.openlocfilehash: 5f27b34bda930d020461bd5f4f7986091ffd5549
ms.sourcegitcommit: b254db346732b64678419db428fd9eb200f3c3c5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/14/2018
ms.locfileid: "53413656"
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Resources implementeren met Resource Manager-sjablonen en Azure CLI

In dit artikel wordt uitgelegd hoe u Azure CLI met Resource Manager-sjablonen gebruiken voor het implementeren van uw resources in Azure. Als u niet bekend bent met de concepten van het implementeren en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).  

De Resource Manager-sjabloon die u implementeert, kunnen een lokaal bestand op uw computer of een extern bestand dat zich bevindt in een opslagplaats, zoals GitHub. De sjabloon die u in dit artikel implementeert is beschikbaar als een [sjabloon van de storage-account in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Als u geen Azure CLI is geïnstalleerd, kunt u de [Cloud Shell](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Lokale sjabloon implementeren

Bij het implementeren van resources naar Azure, u:

1. Aanmelden bij uw Azure-account
2. Maak een resourcegroep die als de container voor de geïmplementeerde resources fungeert. De naam van de resourcegroep kan alleen alfanumerieke tekens, punten, onderstrepingstekens, afbreekstreepjes en haakjes bevatten. Het kan maximaal 90 tekens zijn. Deze mag niet eindigen op een punt.
3. Implementeren in de resourcegroep van de sjabloon die u de resources definieert te maken

Een sjabloon kunt parameters waarmee u kunt het aanpassen van de implementatie bevatten. U kunt bijvoorbeeld waarden die zijn toegesneden opgeven voor een bepaalde omgeving (zoals ontwikkelen, testen en productie). De voorbeeldsjabloon definieert een parameter voor de SKU van het opslagaccount. 

Het volgende voorbeeld wordt een resourcegroep en implementeert u een sjabloon van uw lokale computer:

```azurecli-interactive
az group create --name ExampleGroup --location "Central US"
az group deployment create \
  --name ExampleDeployment \
  --resource-group ExampleGroup \
  --template-file storage.json \
  --parameters storageAccountType=Standard_GRS
```

De implementatie kan enkele minuten duren. Als deze is voltooid, ziet u een bericht dat het resultaat bevat:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Externe-sjabloon implementeren

In plaats van Resource Manager-sjablonen op uw lokale computer, wellicht kunt u beter om op te slaan in een externe locatie. U kunt sjablonen opslaan in een opslagplaats voor bronbeheer (zoals GitHub). Of u kunt ze opslaan in Azure storage-account voor gedeelde toegang in uw organisatie.

Voor het implementeren van een externe-sjabloon, gebruiken de **sjabloon-uri** parameter. Gebruik de URI in het voorbeeld om de voorbeeldsjabloon uit GitHub te implementeren.
   
```azurecli-interactive
az group create --name ExampleGroup --location "Central US"
az group deployment create \
  --name ExampleDeployment \
  --resource-group ExampleGroup \
  --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
  --parameters storageAccountType=Standard_GRS
```

Het vorige voorbeeld vereist een openbaar toegankelijke URI voor de sjabloon die voor de meeste scenario's, werkt omdat de sjabloon mag niet de gevoelige gegevens bevatten. Als u nodig hebt om op te geven van gevoelige gegevens (zoals een beheerderswachtwoord), moet u die waarde als een beveiligde parameter. Echter, als u niet dat de sjabloon openbaar toegankelijk moeten zijn wilt, kunt u deze beschermen door in een persoonlijke opslagcontainer op te slaan. Zie voor meer informatie over het implementeren van een sjabloon die de token van een shared access signature (SAS) is vereist, [persoonlijke sjablonen implementeren met SAS-token](resource-manager-cli-sas-token.md).

[!INCLUDE [resource-manager-cloud-shell-deploy.md](../../includes/resource-manager-cloud-shell-deploy.md)]

Gebruik de volgende opdrachten in de Cloud Shell:

```azurecli-interactive
az group create --name examplegroup --location "South Central US"
az group deployment create --resource-group examplegroup \
  --template-uri <copied URL> \
  --parameters storageAccountType=Standard_GRS
```

## <a name="deploy-to-more-than-one-resource-group-or-subscription"></a>Implementeren naar meer dan één resourcegroep of abonnement

Normaal gesproken implementeren u alle resources in uw sjabloon één resourcegroep bestaan. Er zijn echter scenario's waarin u wilt een set met resources samen te implementeren, maar plaats deze in verschillende resourcegroepen of abonnementen. U kunt implementeren met slechts vijf resourcegroepen in een enkele implementatie. Zie voor meer informatie, [implementeren-Azure-resources aan meer dan één abonnement of resourcegroep](resource-manager-cross-resource-group-deployment.md).

## <a name="redeploy-when-deployment-fails"></a>Opnieuw implementeren wanneer de implementatie mislukt

Voor implementaties die niet voldoen, kunt u opgeven dat van de implementatiegeschiedenis van uw van een eerdere implementatie automatisch opnieuw worden geïmplementeerd. Als u wilt deze optie gebruikt, moeten uw implementaties unieke namen hebben, zodat ze kunnen worden geïdentificeerd in de geschiedenis. Als u geen unieke namen, overschrijft de huidige mislukte implementatie mogelijk de eerder geslaagde implementatie in de geschiedenis. U kunt deze optie alleen gebruiken met niveau root-implementaties. Implementaties van een geneste sjabloon zijn niet beschikbaar voor opnieuw implementeren.

Toevoegen als u wilt implementeren in de laatste geslaagde implementatie, de `--rollback-on-error` parameter als een vlag.

```azurecli-interactive
az group deployment create \
  --name ExampleDeployment \
  --resource-group ExampleGroup \
  --template-file storage.json \
  --parameters storageAccountType=Standard_GRS \
  --rollback-on-error
```

Als u wilt implementeren op een specifieke implementatie, gebruikt u de `--rollback-on-error` parameter en geef de naam van de implementatie.

```azurecli-interactive
az group deployment create \
  --name ExampleDeployment02 \
  --resource-group ExampleGroup \
  --template-file storage.json \
  --parameters storageAccountType=Standard_GRS \
  --rollback-on-error ExampleDeployment01
```

De opgegeven implementatie moet zijn geslaagd.

## <a name="parameters"></a>Parameters

Als u wilt doorgeven van parameterwaarden, kunt u parameters inline of een parameterbestand. De voorgaande voorbeelden in dit artikel weergeven inline parameters.

### <a name="inline-parameters"></a>Inline-parameters

Als u wilt in line-parameters kunt toevoegen, geeft u de waarden in `parameters`. Bijvoorbeeld, een tekenreeks of matrix doorgeven aan een sjabloon is een Bash-shell, gebruiken:

```azurecli
az group deployment create \
  --resource-group testgroup \
  --template-file demotemplate.json \
  --parameters exampleString='inline string' exampleArray='("value1", "value2")'
```

U kunt ook de inhoud van bestand ophalen en verstrekken die inhoud als een inline-parameter.

```azurecli
az group deployment create \
  --resource-group testgroup \
  --template-file demotemplate.json \
  --parameters exampleString=@stringContent.txt exampleArray=@arrayContent.json
```

Een parameterwaarde ophalen uit een bestand is handig wanneer u moet opgeven-configuratiewaarden. U kunt bijvoorbeeld opgeven [cloud-init-waarden voor een virtuele Linux-machine](../virtual-machines/linux/using-cloud-init.md).

De arrayContent.json-indeling is:

```json
[
    "value1",
    "value2"
]
```

### <a name="parameter-files"></a>Parameterbestanden

In plaats van de parameters doorgeven als inline-waarden in het script, wellicht vindt u het eenvoudiger te gebruiken van een JSON-bestand met de parameterwaarden. De parameterbestand moet een lokaal bestand. Externe parameterbestanden worden niet ondersteund met Azure CLI.

De parameterbestand moet zich in de volgende indeling:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

U ziet dat de parametersectie bevat een parameternaam op die overeenkomt met de parameter die is gedefinieerd in uw sjabloon (parameter). Het parameterbestand bevat een waarde voor de parameter. Deze waarde wordt automatisch doorgegeven aan de sjabloon tijdens de implementatie. U kunt meer dan één parameterbestand maken, en geeft u in de juiste parameter-bestand voor het scenario. 

Kopieer het voorgaande voorbeeld en sla deze op als een bestand met de naam `storage.parameters.json`.

Gebruik het volgende om door te geven van een lokale parameterbestand, `@` om op te geven van een lokaal bestand met de naam storage.parameters.json.

```azurecli-interactive
az group deployment create \
  --name ExampleDeployment \
  --resource-group ExampleGroup \
  --template-file storage.json \
  --parameters @storage.parameters.json
```

### <a name="parameter-precedence"></a>Parameter-prioriteit

U kunt gebruiken in line-parameters en een lokale parameterbestand in dezelfde implementatiebewerking. U kunt bijvoorbeeld enkele waarden in de lokale parameterbestand opgeven en toevoegen van andere waarden inline tijdens de implementatie. Als u waarden voor een parameter in de lokale parameterbestand en inline opgeeft, wordt de waarde inline voorrang.

```azurecli
az group deployment create \
  --resource-group testgroup \
  --template-file demotemplate.json \
  --parameters @demotemplate.parameters.json \
  --parameters exampleArray=@arrtest.json
```


## <a name="test-a-template-deployment"></a>Een sjabloonimplementatie testen

U kunt de waarden van uw sjabloon en de parameterbestanden testen zonder daadwerkelijk de resources te implementeren met [az group deployment valideren](/cli/azure/group/deployment#az-group-deployment-validate). 

```azurecli-interactive
az group deployment validate \
  --resource-group ExampleGroup \
  --template-file storage.json \
  --parameters @storage.parameters.json
```

Als er geen fouten worden aangetroffen, retourneert de opdracht de gegevens over de testimplementatie. In het bijzonder u ziet dat de **fout** waarde null is.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Als er een fout wordt gedetecteerd, wordt de opdracht een foutbericht weergegeven. Doorgeven van een onjuiste waarde voor het opslagaccount-SKU, retourneert bijvoorbeeld de volgende fout:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Als uw sjabloon een syntaxisfout heeft, retourneert de opdracht een foutbericht met dat de sjabloon kan niet worden geparseerd. Het bericht geeft aan dat het regelnummer en de positie van de fout bij het parseren.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

## <a name="next-steps"></a>Volgende stappen
* De voorbeelden in dit artikel worden resources implementeren op een resourcegroep in uw standaardabonnement. Zie voor het gebruik van een ander abonnement [meerdere Azure-abonnementen beheren](/cli/azure/manage-azure-subscriptions-azure-cli).
* Als u wilt opgeven voor het verwerken van resources die aanwezig zijn in de resourcegroep, maar niet zijn gedefinieerd in de sjabloon, Zie [Azure Resource Manager-implementatiemodi](deployment-modes.md).
* Zie voor meer informatie over het definiëren van parameters in uw sjabloon, [inzicht in de structuur en de syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).
* Zie voor tips over het oplossen van veelvoorkomende implementatiefouten [veelvoorkomende problemen oplossen Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjablonen implementeren met SAS-token](resource-manager-cli-sas-token.md).
* Zie voor veilig implementatie uw service in meer dan één regio, [Azure Deployment Manager](deployment-manager-overview.md).
