---
title: Containers installeren en uitvoeren
titleSuffix: Text Analytics -  Azure Cognitive Services
description: Het downloaden, installeren en uitvoeren van containers voor Tekstanalyse overschrijd in deze zelfstudie met stapsgewijze instructies.
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 01/02/2019
ms.author: diberry
ms.openlocfilehash: e3b1655207f3baba6ea6e3cf2f00e3540a3602ad
ms.sourcegitcommit: 803e66de6de4a094c6ae9cde7b76f5f4b622a7bb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/02/2019
ms.locfileid: "53969366"
---
# <a name="install-and-run-text-analytics-containers"></a>Installeren en uitvoeren van de Text Analytics-containers

De Text Analytics-containers bieden geavanceerde verwerking van natuurlijke talen via onbewerkte tekst en bevat drie hoofdfuncties: sentimentanalyse, sleuteltermextractie en taaldetectie. Entiteiten koppelen wordt momenteel niet ondersteund in een container. 

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="prerequisites"></a>Vereisten

Om uit te voeren op een van de Text Analytics-containers, moet u het volgende hebt:

## <a name="preparation"></a>Voorbereiding

U moet voldoen aan de volgende vereisten voordat u met behulp van Text Analytics-containers:

|Vereist|Doel|
|--|--|
|Docker-Engine| U moet de Docker-Engine zijn geïnstalleerd op een [hostcomputer](#the-host-computer). Docker biedt pakketten die de Docker-omgeving configureren op [macOS](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), en [Linux](https://docs.docker.com/engine/installation/#supported-platforms). Zie voor een uitleg van de basisprincipes van Docker en containers, de [dockeroverzicht](https://docs.docker.com/engine/docker-overview/).<br><br> Docker moet worden geconfigureerd, zodat de containers om te verbinden met en facturering gegevens verzenden naar Azure. <br><br> **Op Windows**, Docker moet ook worden geconfigureerd ter ondersteuning van Linux-containers.<br><br>|
|Vertrouwd zijn met Docker | U hebt een basiskennis hebt van Docker-kernconcepten zoals registers, -opslagplaatsen, containers, en containerinstallatiekopieën, evenals kennis van basic `docker` opdrachten.| 
|Text Analytics-resource |Als u wilt gebruiken in de container, moet u het volgende hebben:<br><br>Een [ _Tekstanalyse_ ](text-analytics-how-to-access-key.md) Azure-resource om de bijbehorende facturering sleutel en facturering URI van het eindpunt te verkrijgen. Beide waarden zijn beschikbaar op de pagina overzicht van de Text Analytics en sleutels van de Azure portal en zijn verplicht om de container te starten.<br><br>**{BILLING_KEY}** : bronsleutel<br><br>**{BILLING_ENDPOINT_URI}** : voorbeeld van de eindpunt-URI is: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0`|

### <a name="the-host-computer"></a>De hostcomputer

De **host** is de computer met de docker-container. Het kan zijn dat een computer op uw locatie of een docker die als host fungeert de service in Azure, waaronder:

* [Azure Kubernetes Service](../../../aks/index.yml)
* [Azure Container Instances](../../../container-instances/index.yml)
* [Kubernetes](https://kubernetes.io/) cluster geïmplementeerd op [Azure Stack](../../../azure-stack/index.yml). Zie voor meer informatie, [Kubernetes met Azure Stack implementeren](../../../azure-stack/user/azure-stack-solution-template-kubernetes-deploy.md).


### <a name="container-requirements-and-recommendations"></a>Containervereisten en aanbevelingen

De volgende tabel beschrijft de minimale en aanbevolen CPU-kernen, ten minste 2,6 GHz (gigahertz) of sneller, en het geheugen, in gigabytes (GB), om toe te wijzen voor elke container Text Analytics.

| Container | Minimum | Aanbevolen |
|-----------|---------|-------------|
|Sleuteltermextractie | 1 core, 2 GB geheugen | 1 core, 4 GB geheugen |
|Taaldetectie | 1 core, 2 GB geheugen | 1 core, 4 GB geheugen |
|Sentimentanalyse | 1 core, 2 GB geheugen | 1 core, 4 GB geheugen |

Kernen en geheugen komen overeen met de `--cpus` en `--memory` instellingen die worden gebruikt als onderdeel van de `docker run` opdracht.

## <a name="get-the-container-image-with-docker-pull"></a>Met de installatiekopie van de container ophalen `docker pull`

Containerinstallatiekopieën voor Text Analytics zijn beschikbaar via Microsoft Container Registry. 

| Container | Opslagplaats |
|-----------|------------|
|Sleuteltermextractie | `mcr.microsoft.com/azure-cognitive-services/keyphrase` |
|Taaldetectie | `mcr.microsoft.com/azure-cognitive-services/language` |
|Sentimentanalyse | `mcr.microsoft.com/azure-cognitive-services/sentiment` |

Gebruik de [ `docker pull` ](https://docs.docker.com/engine/reference/commandline/pull/) opdracht voor het downloaden van een containerinstallatiekopie vanuit Microsoft Container Registry...

Zie voor een volledige beschrijving van de beschikbare labels voor de Text Analytics-containers, de volgende containers op de Docker-Hub:

* [Sleuteltermextractie](https://go.microsoft.com/fwlink/?linkid=2018757)
* [Taaldetectie](https://go.microsoft.com/fwlink/?linkid=2018759)
* [Sentimentanalyse](https://go.microsoft.com/fwlink/?linkid=2018654)


### <a name="docker-pull-for-the-key-phrase-extraction-container"></a>Docker pull voor de sleutel woordgroep extractie-container

```Docker
docker pull mcr.microsoft.com/azure-cognitive-services/keyphrase:latest
```

### <a name="docker-pull-for-the-language-detection-container"></a>Docker pull voor de taal detecteren-container

```Docker
docker pull mcr.microsoft.com/azure-cognitive-services/language:latest
```

### <a name="docker-pull-for-the-sentiment-container"></a>Docker pull voor de container sentiment

```Docker
docker pull mcr.microsoft.com/azure-cognitive-services/sentiment:latest
```

### <a name="listing-the-containers"></a>De containers weergeven

U kunt de [docker-installatiekopieën](https://docs.docker.com/engine/reference/commandline/images/) opdracht om een lijst van uw gedownloade containerinstallatiekopieën. De volgende opdracht worden bijvoorbeeld de ID, de opslagplaats en het label van elke gedownloade containerinstallatiekopie, opgemaakt als een tabel:

```Docker
docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"
```


## <a name="how-to-use-the-container"></a>Het gebruik van de container

Als de container op de [hostcomputer](#the-host-computer), de volgende procedure gebruiken om te werken met de container.

1. [Uitvoeren van de container](#run-the-container-with-docker-run), facturering met de vereiste instellingen. Meer [voorbeelden](../text-analytics-resource-container-config.md#example-docker-run-commands) van de `docker run` opdrachten zijn beschikbaar. 
1. [Query van de container voorspelling eindpunt](#query-the-containers-prediction-endpoint). 

## <a name="run-the-container-with-docker-run"></a>De container met uitvoeren `docker run`

Gebruik de [docker uitvoeren](https://docs.docker.com/engine/reference/commandline/run/) opdracht uit te voeren op een van de drie containers. De opdracht maakt gebruik van de volgende parameters:

| Tijdelijke aanduiding | Waarde |
|-------------|-------|
|{BILLING_KEY} | Deze sleutel wordt gebruikt voor het starten van de container en is beschikbaar op de pagina van de Text Analytics sleutels van de Azure portal.  |
|{BILLING_ENDPOINT_URI} | Het eindpunt van de facturering URI-waarde is beschikbaar op de pagina van de Text Analytics overzicht van de Azure portal.|

Deze parameters vervangen door uw eigen waarden in het volgende voorbeeld `docker run` opdracht.

```bash
docker run --rm -it -p 5000:5000 --memory 4g --cpus 1 \
mcr.microsoft.com/azure-cognitive-services/keyphrase \
Eula=accept \
Billing={BILLING_ENDPOINT_URI} \
ApiKey={BILLING_KEY}
```

Met deze opdracht:

* Een container sleuteluitdrukkingen kan worden uitgevoerd van de container-installatiekopie
* Één CPU-kernen en 4 GB (Gigabyte) aan geheugen worden toegewezen
* Gebruikt TCP-poort 5000 en wijst er een pseudo-TTY voor de container
* De container worden automatisch verwijderd nadat deze is afgesloten. De containerinstallatiekopie is nog steeds beschikbaar op de hostcomputer. 

Meer [voorbeelden](../text-analytics-resource-container-config.md#example-docker-run-commands) van de `docker run` opdrachten zijn beschikbaar. 

> [!IMPORTANT]
> De `Eula`, `Billing`, en `ApiKey` opties moeten worden opgegeven voor het uitvoeren van de container; anders wordt de container niet start.  Zie voor meer informatie, [facturering](#billing).

## <a name="query-the-containers-prediction-endpoint"></a>Query uitvoeren op het eindpunt voorspelling van de container

De container biedt eindpunt van de voorspelling query op basis van REST API's. 

Gebruikmaken van de host https://localhost:5000, voor de container met API's.

## <a name="stop-the-container"></a>De container stoppen

[!INCLUDE [How to stop the container](../../../../includes/cognitive-services-containers-stop.md)]

## <a name="troubleshooting"></a>Problemen oplossen

Als u de container wordt uitgevoerd met een uitvoer [koppelen](../text-analytics-resource-container-config.md#mount-settings) en logboekregistratie is ingeschakeld, wordt de container genereert logboekbestanden die tot het oplossen van problemen die optreden tijdens het starten of uitvoeren van de container. 

## <a name="containers-api-documentation"></a>API-documentatie van de container

De container biedt een volledige set met documentatie voor de eindpunten, evenals een `Try it now` functie. Deze functie kunt u uw instellingen invoeren in een web gebaseerde HTML-formulier en de query zonder code te schrijven. Nadat de query retourneert, een voorbeeld van de CURL-opdracht om te laten zien hoe de HTTP-headers en hoofdtekst van de vereiste indeling is opgegeven. 

> [!TIP]
> Lees de [OpenAPI-specificatie](https://swagger.io/docs/specification/about/), met een beschrijving van de API-bewerkingen ondersteund door de container van de `/swagger` relatieve URI. Bijvoorbeeld:
>
>  ```http
>  http://localhost:5000/swagger
>  ```

## <a name="billing"></a>Billing

De Text Analytics containers verzenden factuurgegevens naar Azure, met behulp van een _Tekstanalyse_ resource voor uw Azure-account. 

Cognitive Services-containers zijn geen licentie om uit te voeren zonder verbinding met Azure voor het meten. Klanten moeten de containers om te communiceren factureringsgegevens met de softwarelicentiecontrole-service te allen tijde inschakelen. Cognitive Services-containers verzenden klantgegevens niet naar Microsoft. 

De `docker run` opdracht maakt gebruik van de volgende argumenten voor factureringsdoeleinden bepalen:

| Optie | Description |
|--------|-------------|
| `ApiKey` | De API-sleutel van de _Tekstanalyse_ resource gebruikt voor het bijhouden van informatie over facturering. |
| `Billing` | Het eindpunt van de _Tekstanalyse_ resource gebruikt voor het bijhouden van informatie over facturering.|
| `Eula` | Geeft aan dat u de licentie voor de container hebt geaccepteerd.<br/>De waarde van deze optie moet worden ingesteld op `accept`. |

> [!IMPORTANT]
> Alle drie de opties met geldige waarden moeten worden opgegeven of de container start niet.

Zie voor meer informatie over deze opties [containers configureren](../text-analytics-resource-container-config.md).

## <a name="summary"></a>Samenvatting

In dit artikel hebt u geleerd concepten en werkstroom voor het downloaden, installeren en Text Analytics-containers uitvoeren. Samenvatting:

* Text Analytics biedt drie Linux-containers voor Docker, encapsulating sleuteltermextractie, taaldetectie en sentimentanalyse.
* Containerinstallatiekopieën worden gedownload uit het Microsoft Container Registry (MCR) in Azure.
* Containerinstallatiekopieën uitvoeren in Docker.
* U kunt de REST-API of de SDK gebruiken om aan te roepen van bewerkingen in Text Analytics-containers door de host-URI van de container op te geven.
* Bij het instantiëren van een container, moet u informatie over facturering opgeven.

> [!IMPORTANT]
> Cognitive Services-containers zijn geen licentie om uit te voeren zonder verbinding met Azure voor het meten. Klanten moeten de containers om te communiceren factureringsgegevens met de softwarelicentiecontrole-service te allen tijde inschakelen. Cognitive Services-containers verzenden klantgegevens (zoals de afbeelding of tekst die wordt geanalyseerd) niet naar Microsoft.

## <a name="next-steps"></a>Volgende stappen

* Beoordeling [containers configureren](../text-analytics-resource-container-config.md) voor configuratie-instellingen
* Raadpleeg [Veelgestelde vragen (FAQ)](../text-analytics-resource-faq.md) het oplossen van problemen met betrekking tot functionaliteit.

