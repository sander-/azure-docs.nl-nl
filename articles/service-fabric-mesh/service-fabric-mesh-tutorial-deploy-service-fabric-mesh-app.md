---
title: 'Zelfstudie: een Service Fabric Mesh-toepassing implementeren | Microsoft Docs'
description: Leer hoe u Visual Studio gebruikt om een Azure Service Fabric Mesh-toepassing te publiceren die bestaat uit een ASP.NET Core-website die met een back-end-webservice communiceert.
services: service-fabric-mesh
documentationcenter: .net
author: TylerMSFT
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: service-fabric-mesh
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/18/2018
ms.author: twhitney
ms.custom: mvc, devcenter
ms.openlocfilehash: ec282bc1159e8a8cf21b88b8430bbf3067686528
ms.sourcegitcommit: 295babdcfe86b7a3074fd5b65350c8c11a49f2f1
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/27/2018
ms.locfileid: "53788613"
---
# <a name="tutorial-deploy-a-service-fabric-mesh-application"></a>Zelfstudie: Een Service Fabric Mesh-toepassing implementeren

Deze zelfstudie is deel drie van een reeks en laat u zien hoe u een Azure Service Fabric Mesh-webtoepassing rechtstreeks vanuit Visual Studio implementeert.

In deze zelfstudie leert u het volgende:
> [!div class="checklist"]
> * De app publiceren in Azure met Visual Studio.
> * De implementatiestatus van de toepassing controleren
> * Alle toepassingen bekijken die momenteel in uw abonnement zijn geïmplementeerd

In deze zelfstudiereeks leert u het volgende:
> [!div class="checklist"]
> * [Een Service Fabric Mesh-app maken in Visual Studio](service-fabric-mesh-tutorial-create-dotnetcore.md)
> * [Fouten opsporen in een Service Fabric Mesh-app die wordt uitgevoerd in de lokale ontwikkelcluster](service-fabric-mesh-tutorial-debug-service-fabric-mesh-app.md)
> * Een Service Fabric Mesh-app implementeren
> * [Een Service Fabric Mesh-app bijwerken](service-fabric-mesh-tutorial-upgrade.md)
> * [Service Fabric Mesh-bronnen opschonen](service-fabric-mesh-tutorial-cleanup-resources.md)

[!INCLUDE [preview note](./includes/include-preview-note.md)]

## <a name="prerequisites"></a>Vereisten

Voor u met deze zelfstudie begint:

* Als u nog geen abonnement op Azure hebt, kunt u een [gratis account maken](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.

* Controleer of u [uw ontwikkelomgeving hebt ingesteld](service-fabric-mesh-howto-setup-developer-environment-sdk.md). Hieronder valt het installeren van de Service Fabric-runtime, SDK, Docker en Visual Studio 2017.

## <a name="download-the-to-do-sample-application"></a>De voorbeeldtoepassing voor taken downloaden

Als u in [deel twee van deze zelfstudiereeks](service-fabric-mesh-tutorial-debug-service-fabric-mesh-app.md) niet de voorbeeldtoepassing voor taken hebt gemaakt, kunt u deze downloaden. Voer in een opdrachtvenster de volgende opdracht uit om de voorbeeld-app-opslagplaats te klonen op de lokale computer.

```
git clone https://github.com/azure-samples/service-fabric-mesh
```

U vindt de toepassing in de map `src\todolistapp`.

## <a name="publish-to-azure"></a>Publiceren naar Azure

Als u uw Service Fabric Mesh-project in Azure wilt publiceren, klikt u met de rechtermuisknop op **todolistapp** in Visual Studio en selecteert u **Publiceren...**.

Vervolgens ziet u het dialoogvenster **Service Fabric-toepassing publiceren**.

![Dialoogvenster in Visual Studio over Service Fabric Mesh-publicatie](./media/service-fabric-mesh-tutorial-deploy-dotnetcore/visual-studio-publish-dialog.png)

Selecteer uw Azure-account en -abonnement. Kies een **Locatie**. In dit artikel wordt gebruikgemaakt van **US - oost**.

Selecteer onder **Resourcegroep** **\<Nieuwe resourcegroep maken...>**. Er verschijnt een dialoogvenster waarin u uw nieuwe resourcegroep maakt. In dit artikel wordt de locatie **US - oost** gebruikt en krijgt de groep de naam **sfmeshTutorial1RG** (kies een unieke groepsnaam als meerdere mensen in uw organisatie gebruikmaken van hetzelfde abonnement).  Druk op **Maken** om de resourcegroep te maken en ga terug naar het publicatiedialoogvenster.

![Dialoogvenster in Visual Studio over nieuwe resourcegroep in Service Fabric Mesh](./media/service-fabric-mesh-tutorial-deploy-dotnetcore/visual-studio-publish-new-resource-group-dialog.png)

In het dialoogvenster **Service Fabric-toepassing publiceren** selecteert u onder **Azure Container Registry** **\<Nieuw containerregister maken...>**. In het dialoogvenster **Containerregister maken** gebruikt u een unieke naam voor de **Containerregisternaam**. Geef een **Locatie** op (in deze tutorial wordt gebruikgemaakt van **US - oost**). Selecteer in de vervolgkeuzelijst de **Resourcegroep** die u eerder hebt gemaakt, bijvoorbeeld **sfmeshTutorial1RG**. Stel de **SKU** in op **Basic** en druk op **Maken** om het persoonlijke Azure-containerregister te maken en terug te gaan naar het dialoogvenster Publiceren.

![Dialoogvenster in Visual Studio over nieuw containerregister in Service Fabric Mesh](./media/service-fabric-mesh-tutorial-deploy-dotnetcore/visual-studio-publish-new-container-registry-dialog.png)

Als u een fout krijgt dat er voor uw abonnement geen resourceprovider is geregistreerd, kunt u er een registreren. Controleer eerst of de resourceprovider beschikbaar is voor uw abonnement:

```Powershell
Get-AzureRmResourceProvider -ListAvailable
```

Als de containerregisterprovider (`Microsoft.ContainerRegistry`) beschikbaar is, registreert u deze vanuit PowerShell:

```Powershell
Connect-AzureRmAccount
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ContainerRegistry
```

In het publicatiedialoogvenster drukt u op de knop **Publiceren** om uw Service Fabric-toepassing te implementeren in Azure.

Wanneer u voor het eerst in Azure implementeert, wordt de docker-installatiekopie naar de Azure Container Registry (ACR) gepushed, wat afhankelijk van de grootte van de kopie even kan duren. Volgende publicaties voor hetzelfde project zullen sneller verlopen. U kunt de voortgang van de implementatie bekijken door het deelvenster **Service Fabric Tools** in het Visual Studio-venster **Uitvoer** te selecteren. Nadat de implementatie is voltooid, toont de uitvoer van de **Service Fabric Tools** het IP-adres en de poort van uw toepassing in de vorm van een URL.

```json
Packaging Application...
Building Images...
Web1 -> C:\Code\ServiceFabricMeshApp\ToDoService\bin\Any CPU\Release\netcoreapp2.0\ToDoService.dll
Uploading the images to Azure Container Registy...
Deploying application to remote endpoint...
The application was deployed successfully and it can be accessed at http://10.000.38.000:20000.
```

Open een webbrowser en navigeer naar de URL om de website in Azure uitgevoerd te zien worden.

## <a name="set-up-service-fabric-mesh-cli"></a>Service Fabric Mesh CLI instellen 
U kunt de Azure Cloud Shell of een lokale installatie van de Azure CLI gebruiken voor de resterende stappen. Installeer de Azure Service Fabric Mesh CLI-uitbreidingsmodule door de volgende [instructies](service-fabric-mesh-howto-setup-cli.md) te volgen.

## <a name="check-application-deployment-status"></a>De implementatiestatus van de toepassing controleren

Op dit punt is uw toepassing geïmplementeerd. Met de opdracht `app show` kunt u de status van de toepassing bekijken. 

De naam van de toepassing voor de zelfstudie-app is `todolistapp`. Haal de details van de toepassing op met de volgende opdracht:

```azurecli-interactive
az mesh app show --resource-group $rg --name todolistapp
```

## <a name="see-all-applications-currently-deployed-to-your-subscription"></a>Alle toepassingen bekijken die momenteel in uw abonnement zijn geïmplementeerd

U kunt de opdracht 'app list' gebruiken om een lijst met toepassingen die u in uw abonnement hebt geïmplementeerd op te halen.

```azurecli-interactive
az mesh app list --output table
```

## <a name="next-steps"></a>Volgende stappen

In dit deel van de zelfstudie hebt u het volgende geleerd:
> [!div class="checklist"]
> * De app publiceren in Azure.
> * De implementatiestatus van de toepassing controleren
> * Alle toepassingen bekijken die u momenteel hebt geïmplementeerd in uw abonnement

Ga door naar de volgende zelfstudie:
> [!div class="nextstepaction"]
> [Een Service Fabric Mesh-app bijwerken](service-fabric-mesh-tutorial-upgrade.md)

[azure-cli-install]: https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest
