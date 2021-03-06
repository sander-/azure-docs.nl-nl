---
title: Offline - apparaten werkt Azure IoT Edge | Microsoft Docs
description: Begrijp hoe IoT Edge-apparaten en -modules kunnen werken zonder internetverbinding gedurende langere tijd wordt opgelost, en hoe normale IoT-apparaten offline te werken op IoT Edge kunt inschakelen.
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 09/20/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.custom: seodec18
ms.openlocfilehash: 4c4713bade487ba46f1abdc6d0a76db3e81e38b1
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53096941"
---
# <a name="understand-extended-offline-capabilities-for-iot-edge-devices-modules-and-child-devices-preview"></a>Meer informatie over uitgebreide offline mogelijkheden voor IoT Edge-apparaten, modules en onderliggende apparaten (preview)

Azure IoT Edge biedt ondersteuning voor uitgebreide offline bewerkingen op uw IoT Edge-apparaten en offline-bewerkingen op onderliggende van niet-Microsoft Edge-apparaten te kunnen. Als een IoT Edge-apparaat een mogelijkheid om te verbinden met IoT Hub heeft, kunnen het en eventuele onderliggende-apparaten blijven functie met onregelmatige of geen verbinding met internet. 

>[!NOTE]
>Offline ondersteuning voor IoT Edge is [preview-versie](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="how-it-works"></a>Hoe werkt het?

Wanneer een IoT Edge-apparaat in de offlinemodus bevindt gaat, neemt de Edge hub drie rollen. Eerst worden opgeslagen berichten die heengaat upstream en slaat ze op totdat het apparaat opnieuw verbinding maakt. Ten tweede, fungeert deze namens IoT Hub voor verificatie van modules en onderliggende apparaten zodat ze kunnen blijven functioneren. Ten slotte maakt communicatie tussen de apparaten van de onderliggende die normaal zou gaan via IoT Hub mogelijk. 

Het volgende voorbeeld ziet u de werking van een IoT Edge-scenario in de offlinemodus:

1. **Een IoT Edge-apparaat configureren.**

   IoT Edge-apparaten hebben automatisch offline-mogelijkheden ingeschakeld. Om uit te breiden die mogelijkheid met andere IoT-apparaten, moet u een bovenliggende / onderliggende relatie tussen de apparaten in IoT Hub declareren. 

2. **Synchronisatie met IoT Hub.**

   Ten minste eenmaal na de installatie van de IoT Edge-runtime, de IoT Edge-apparaat moet online zijn om te synchroniseren met IoT Hub. In deze synchronisatie haalt de IoT Edge-apparaat meer informatie over alle onderliggende apparaten zijn toegewezen. De IoT Edge-apparaat wordt ook veilig updates van de lokale cache om in te schakelen van offline-bewerkingen en worden instellingen voor lokale opslag van berichten over telemetrie opgehaald. 

3. **Offline gaan.**

   Terwijl niet verbonden met IoT Hub, kunnen de IoT Edge-apparaat, de geïmplementeerde modules en alle onderliggende items IoT-apparaten werken voor onbepaalde tijd. Modules en onderliggende apparaten kunnen starten en opnieuw opstarten door te verifiëren bij de Edge hub tijdens offline. Telemetrie upstream gebonden aan IoT Hub worden lokaal opgeslagen. Communicatie tussen modules of onderliggende IoT-apparaten wordt onderhouden door directe methoden of berichten. 

4. **Sluit en opnieuw synchroniseren met IoT Hub.**

   Zodra de verbinding met IoT Hub is hersteld, wordt de IoT Edge-apparaat weer wordt gesynchroniseerd. Lokaal opgeslagen berichten worden bezorgd in dezelfde volgorde als waarin ze zijn opgeslagen. Eventuele verschillen tussen de gewenste en gerapporteerde eigenschappen van de modules en -apparaten zijn afgestemd. De IoT Edge-apparaat bijwerken eventuele wijzigingen in een set toegewezen onderliggende IoT-apparaten.

## <a name="restrictions-and-limits"></a>Beperkingen en limieten

De uitgebreide offline-mogelijkheden die worden beschreven in dit artikel zijn beschikbaar in [IoT Edge versie 1.0.4 of hoger](https://github.com/Azure/azure-iotedge/releases). Eerdere versies hebben een subset van de offline functies. IoT Edge bestaande apparaten waarvoor geen uitgebreide mogelijkheden voor offline kunnen niet worden bijgewerkt door het veranderen van de runtimeversie, maar moeten opnieuw worden geconfigureerd met een nieuwe IoT Edge-apparaat-id te krijgen van deze functies. 

Uitgebreide offline ondersteuning is beschikbaar in alle regio's waar de IoT Hub verkrijgbaar is, **behalve** VS-Oost.

Alleen niet - Microsoft Edge-IoT-apparaten kunnen worden toegevoegd als onderliggende apparaten. 

IoT Edge-apparaten en hun apparaten toegewezen onderliggende kunnen worden gebruikt voor onbepaalde tijd offline na de initiële, eenmalige-synchronisatie. Opslag van berichten is afhankelijk van time to live (TTL) instelling en de beschikbare schijfruimte voor het opslaan van de berichten. 

## <a name="set-up-an-edge-device"></a>Een Edge-apparaat instellen

Voor een IoT Edge-apparaat uit te breiden zijn uitgebreide offline mogelijkheden voor het onderliggende IoT-apparaten, moet u op te geven van de bovenliggende / onderliggende relatie in Azure portal.

### <a name="assign-child-devices"></a>Onderliggende apparaten toewijzen

Onderliggende apparaten mag niet-Edge-apparaat dat is geregistreerd bij dezelfde IoT Hub. U kunt de bovenliggende / onderliggende relatie voor het maken van een nieuw apparaat of vanuit de detailpagina van het apparaat van de bovenliggende IoT Edge-apparaat of de onderliggende IoT-apparaat kunt beheren. 

   ![Onderliggende apparaten beheren vanaf de pagina met details van IoT Edge-apparaat](./media/offline-capabilities/manage-child-devices.png)

Bovenliggende apparaten kunnen meerdere onderliggende apparaten hebben, maar een onderliggend apparaat kan slechts één bovenliggend object hebben.

### <a name="specifying-dns-servers"></a>DNS-servers op te geven 

Het verdient ter verbetering van robuustheid biedt u de adressen van de DNS-server in uw omgeving gebruikt. Bijvoorbeeld: in Linux, werken **/etc/docker/daemon.json** (mogelijk moet u het bestand maken) om op te nemen:

```
{
    "dns": [“1.1.1.1”]
}
```

Als u een lokale DNS-server gebruikt, vervangt u de 1.1.1.1 met het IP-adres van de lokale DNS-server. Start de docker-service de wijzigingen van kracht te laten worden.


## <a name="optional-offline-settings"></a>Optionele offline-instellingen

Als u uw apparaten om lange offline perioden, waarna u wenst te verzamelen van alle berichten die zijn gegenereerd, verwacht dat de Edge hub configureren zodat deze alle berichten kunt opslaan. Er zijn twee wijzigingen die u Edge hub aanbrengen kunt om in te schakelen van langdurige berichtopslag. Eerst het time to live-instelling en voegt u extra schijfruimte voor de berichtopslag. 

### <a name="time-to-live"></a>Time To Live

Time to live-instelling is de hoeveelheid tijd (in seconden) die een bericht wachten kunt moet worden geleverd voordat deze verloopt. De standaardwaarde is 7200 seconden (twee uur). 

Deze instelling is een gewenste eigenschap van de Edge hub die is opgeslagen in de moduledubbel. U kunt deze configureren in Azure portal, in de **geavanceerde instellingen voor Edge-Runtime configureren** sectie of rechtstreeks in de implementatie van het manifest. 

```json
"$edgeHub": {
    "properties.desired": {
        "schemaVersion": "1.0",
        "routes": {},
        "storeAndForwardConfiguration": {
            "timeToLiveSecs": 7200
        }
    }
}
```

### <a name="additional-offline-storage"></a>Extra offline opslag

Berichten worden standaard opgeslagen in de Edge hub container bestandssysteem. Als deze hoeveelheid opslag niet voldoende voor de behoeften van uw offline is, kunt u speciaal aan lokale opslag op het IoT Edge-apparaat. U moet maken van een omgevingsvariabele voor de Edge hub die naar een opslagmap in de container verwijst. Vervolgens gebruikt u de opties voor het maken die opslagmap binden aan een map op de hostcomputer. 

U kunt omgevingsvariabelen en de opties voor het maken van de Edge hub-module configureren in Azure portal in de **geavanceerde instellingen voor Edge-Runtime configureren** sectie. Of u kunt deze rechtstreeks in het manifest van de implementatie configureren. 

```json
"edgeHub": {
    "type": "docker",
    "settings": {
        "image": "mcr.microsoft.com/azureiotedge-hub:1.0",
        "createOptions": "{\"HostConfig\":{\"Binds\":[\"<HostStoragePath>:<ModuleStoragePath>\"],\"PortBindings\":{\"8883/tcp\":[{\"HostPort\":\"8883\"}],\"443/tcp\":[{\"HostPort\":\"443\"}],\"5671/tcp\":[{\"HostPort\":\"5671\"}]}}}"
    },
    "env": {
        "storageFolder": {
            "value": "<ModuleStoragePath>"
        }
    },
    "status": "running",
    "restartPolicy": "always"
}
```

Vervang `<HostStoragePath>` en `<ModuleStoragePath>` opslagpad pad; de host en de module moet met uw storage-host en de module een absoluut pad zijn.  Bijvoorbeeld, `\"Binds\":[\"/etc/iotedge/storage/:/iotedge/storage/"` betekent hosten pad `/etc/iotedge/storage` is toegewezen aan containerpad `/iotedge/storage/`.  U vindt ook meer informatie over createOptions van [docker docs](https://docs.docker.com/engine/api/v1.32/#operation/ContainerCreate).

## <a name="next-steps"></a>Volgende stappen

Inschakelen van uitgebreide offline bewerkingen in uw [transparante gateway](how-to-create-transparent-gateway.md) scenario's.
