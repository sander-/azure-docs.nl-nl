---
title: 'Snelstartgids: Een Azure IoT Edge-apparaat maken in Linux | Microsoft Docs'
description: In deze snelstartgids leert u hoe u een IoT Edge-apparaat maakt en daarna kant-en-klare code op afstand implementeert vanuit Azure Portal.
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 12/31/2018
ms.topic: quickstart
ms.service: iot-edge
services: iot-edge
ms.custom: mvc, seodec18
ms.openlocfilehash: dcfbc014eaa191c7992a2da195f9bcd10b44194f
ms.sourcegitcommit: 63b996e9dc7cade181e83e13046a5006b275638d
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/10/2019
ms.locfileid: "54191476"
---
# <a name="quickstart-deploy-your-first-iot-edge-module-to-a-linux-x64-device"></a>Snelstartgids: Uw eerste IoT Edge-module implementeren op een Linux x64-apparaat

Met Azure IoT Edge kunt u profiteren van de kracht van de cloud op uw Internet of Things-apparaten. In deze snelstart gebruikt u de cloudinterface om vooraf geschreven code op afstand te implementeren op een IoT Edge-apparaat.

In deze snelstart leert u de volgende zaken:

1. Een IoT Hub maken.
2. Een IoT Edge-apparaat registreren in uw IoT-hub.
3. De IoT Edge-runtime op uw apparaat installeren en starten.
4. Op afstand een module implementeren op een IoT Edge-apparaat.

![Diagram - Snelstartarchitectuur voor apparaat en cloud](./media/quickstart-linux/install-edge-full.png)

In deze snelstart verandert u uw Linux-computer of virtuele machine in een IoT Edge-apparaat. Vervolgens implementeert u een module vanuit Azure Portal op uw apparaat. De module die u in deze snelstart implementeert, is een gesimuleerde sensor waarmee temperatuur-, luchtvochtigheids- en drukgegevens worden gegenereerd. De andere Azure IoT Edge-zelfstudies bouwen voort op het werk dat u hier doet door modules te implementeren waarmee de gesimuleerde gegevens worden geanalyseerd voor zakelijke inzichten.

Als u nog geen actief abonnement op Azure hebt, maakt u een [gratis Azure-account](https://azure.microsoft.com/free) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

U gebruikt de Azure CLI om veel van de stappen in deze snelstart uit te voeren, en Azure IoT heeft een extensie om extra functionaliteit in te schakelen. 

Voeg de Azure IoT-extensie toe aan het exemplaar van Cloud Shell.

   ```azurecli-interactive
   az extension add --name azure-cli-iot-ext
   ```

## <a name="prerequisites"></a>Vereisten

Cloudresources: 

* Een resourcegroep voor het beheren van alle resources die u in deze snelstart maakt. 

   ```azurecli-interactive
   az group create --name IoTEdgeResources --location westus2
   ```

IoT Edge-apparaat:

* Een virtueel Linux-apparaat of een virtuele Linux-computer die fungeert als uw IoT Edge-apparaat. Als u een virtuele machine in Azure wilt maken, gebruikt u de volgende opdracht om snel aan de slag te gaan:

   ```azurecli-interactive
   az vm create --resource-group IoTEdgeResources --name EdgeVM --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username azureuser --generate-ssh-keys --size Standard_DS1_v2
   ```

   Het maken en starten van de nieuwe virtuele machine kan een paar minuten duren. 

   Wanneer u een nieuwe virtuele machine maakt, noteert u het **publicIpAddress**, dat deel uitmaakt van de uitvoer van de opdracht create. U gebruikt dit openbare IP-adres later in deze quickstart om verbinding te maken met de virtuele machine.

## <a name="create-an-iot-hub"></a>Een IoT Hub maken

Begin met de snelstart door een IoT Hub met Azure CLI te maken.

![Diagram - Een IoT-hub maken in de cloud](./media/quickstart-linux/create-iot-hub.png)

Het gratis niveau van IoT Hub werkt voor deze snelstart. Als u in het verleden IoT Hub hebt gebruikt en al een gratis hub hebt gemaakt, kunt u die IoT-hub gebruiken. Elk abonnement biedt toegang tot slechts één gratis IoT-hub. 

Met de volgende code wordt een gratis **F1**-hub gemaakt in de resourcegroep **IoTEdgeResources**. Vervang *{hub_name}* door een unieke naam voor uw IoT-hub.

   ```azurecli-interactive
   az iot hub create --resource-group IoTEdgeResources --name {hub_name} --sku F1 
   ```

   Als er een fout optreedt omdat er al één gratis hub in uw abonnement is, wijzigt u de SKU in **S1**. Als u het foutbericht ontvangt dat de naam van de IoT Hub niet beschikbaar is, betekent dit dat iemand anders al een hub met die naam heeft. Probeer een andere naam. 

## <a name="register-an-iot-edge-device"></a>Een IoT Edge-apparaat registreren

Registreer een IoT Edge-apparaat bij uw net gemaakte IoT Hub.
![Diagram - Een apparaat registreren met een IoT Hub-entiteit](./media/quickstart-linux/register-device.png)

Maak een apparaat-id voor uw gesimuleerde apparaat, zodat het met uw IoT-hub kan communiceren. De apparaat-id is opgeslagen in de cloud, en u gebruikt een unieke apparaatverbindingsreeks om een fysiek apparaat te koppelen aan een apparaat-id. 

Omdat IoT Edge-apparaten zich anders gedragen en anders kunnen worden beheerd dan gewone IoT-apparaten, declareert u deze identiteit met een `--edge-enabled`-vlag als een identiteit van een IoT Edge-apparaat. 

1. Voer in Azure Cloud Shell de volgende opdracht in om een ​​apparaat met de naam **myEdgeDevice** in uw hub te maken.

   ```azurecli-interactive
   az iot hub device-identity create --hub-name {hub_name} --device-id myEdgeDevice --edge-enabled
   ```

   Als u een foutbericht over iothubowner-beleidssleutels ontvangt, controleer dan of in de cloudshell de meest recente versie van de azure-cli-iot-ext-extensie wordt uitgevoerd. 

2. Haal de verbindingsreeks voor uw apparaat op, zodat uw fysieke apparaat aan de bijbehorende identiteit in IoT Hub wordt gekoppeld. 

   ```azurecli-interactive
   az iot hub device-identity show-connection-string --device-id myEdgeDevice --hub-name {hub_name}
   ```

3. Kopieer de verbindingsreeks van de JSON-uitvoer en sla deze op. U gebruikt deze waarde voor het configureren van de IoT Edge-runtime in de volgende sectie.

   ![Verbindingsreeks ophalen uit de CLI-uitvoer](./media/quickstart/retrieve-connection-string.png)

## <a name="install-and-start-the-iot-edge-runtime"></a>De IoT Edge-runtime installeren en starten

Installeer en start de Azure IoT Edge-runtime op uw IoT Edge-apparaat. 
![Diagram - De runtime op apparaat starten](./media/quickstart-linux/start-runtime.png)

De IoT Edge-runtime wordt op alle IoT Edge-apparaten geïmplementeerd. Deze bevat drie onderdelen. De **IoT Edge-beveiligingsdaemon** wordt telkens gestart wanneer een Edge-apparaat wordt opgestart en start het apparaat op door de IoT Edge-agent te starten. De **IoT Edge-agent** faciliteert de implementatie en bewaking van modules op het IoT Edge-apparaat, inclusief de IoT Edge-hub. Met de **IoT Edge-hub** wordt de communicatie tussen modules op het IoT Edge-apparaat en tussen het apparaat en IoT Hub beheerd. 

Tijdens de installatie van de runtime geeft u een apparaatverbindingsreeks op. Gebruik de tekenreeks die u hebt opgehaald via de Azure CLI. Deze tekenreeks koppelt uw fysieke apparaat aan de IoT Edge-apparaat-id in Azure. 

### <a name="connect-to-your-iot-edge-device"></a>Verbinding maken met uw IoT Edge-apparaat

De stappen in deze sectie worden allemaal uitgevoerd op uw IoT Edge-apparaat. Als u uw eigen computer als IoT Edge-apparaat gebruikt, kunt u doorgaan naar het volgende gedeelte. Als u een virtuele machine of secundaire hardware gebruikt, wilt u nu verbinding maken met die computer. 

Als u in deze quickstart een virtuele Azure-machine hebt gemaakt, haalt u het openbare IP-adres op dat is uitgevoerd door de opdracht create. U kunt het openbare IP-adres ook vinden op de overzichtspagina van de virtuele machine in de Azure-portal. Gebruik de volgende opdracht om verbinding te maken met uw virtuele machine. Vervang **{publicIpAddress}** door het adres van de computer. 

```azurecli-interactive
ssh azureuser@{publicIpAddress}
```

### <a name="register-your-device-to-use-the-software-repository"></a>Uw apparaat registreren voor gebruik van de softwareopslagplaats

De pakketten die u nodig hebt voor het uitvoeren van de IoT Edge-runtime worden beheerd in een softwareopslagplaats. Configureer uw IoT Edge-apparaat voor toegang tot deze opslagplaats. 

De stappen in deze sectie zijn bestemd voor x64-apparaten met **Ubuntu 16.04**. Raadpleeg [De Azure IoT Edge-runtime installeren in Linux (x64)](how-to-install-iot-edge-linux.md) of [Linux (ARM32v7/armhf)](how-to-install-iot-edge-linux-arm.md) voor toegang tot de softwareopslagplaats in andere versies van Linux of apparaatarchitecturen.

1. Installeer de opslagplaatsconfiguratie op de computer die u als een IoT Edge-apparaat gebruikt.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
   sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
   ```

2. Installeer een openbare sleutel voor toegang tot de opslagplaats.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
   ```

### <a name="install-a-container-runtime"></a>Een container-runtime installeren

De IoT Edge-runtime is een set van containers, en de logica die u op uw IoT Edge-apparaat implementeert, wordt geleverd als containers. Bereid uw apparaat voor op deze onderdelen door een container-runtime te installeren.

1. Werk **apt get-** bij.

   ```bash
   sudo apt-get update
   ```

2. Installeer **Moby**, een container-runtime.

   ```bash
   sudo apt-get install moby-engine
   ```

3. Installeer de CLI-opdrachten voor Moby. 

   ```bash
   sudo apt-get install moby-cli
   ```

### <a name="install-and-configure-the-iot-edge-security-daemon"></a>De IoT Edge-beveiligingsdeamon installeren en configureren

De beveiligingsdeamon wordt geïnstalleerd als een systeemservice, zodat de IoT Edge-runtime elke keer wordt gestart wanneer uw apparaat wordt opgestart. De installatie bevat ook een versie van **hsmlib** waarmee de beveiligingsdeamon kan communiceren met de hardwarebeveiliging van het apparaat. 

1. Download en installeer de IoT Edge-beveiligingsdaemon. 

   ```bash
   sudo apt-get update
   sudo apt-get install iotedge
   ```

2. Open het IoT Edge-configuratiebestand. Het is een beveiligd bestand, dus mogelijk moet u verhoogde bevoegdheden gebruiken om het te openen.
   
   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

3. Voeg de verbindingsreeks van het IoT Edge-apparaat toe. Zoek de variabele **device_connection_string** en werk de waarde bij met de tekenreeks die u hebt gekopieerd na de registratie van uw apparaat. Deze verbindingsreeks koppelt uw fysieke apparaat aan de apparaat-id die u in Azure hebt gemaakt.

4. Sla het bestand op en sluit het. 

   `CTRL + X`, `Y`, `Enter`

5. Start de IoT Edge-beveiligingsdaemon opnieuw op om uw wijzigingen toe te passen.

   ```bash
   sudo systemctl restart iotedge
   ```

### <a name="view-the-iot-edge-runtime-status"></a>De IoT Edge runtime-status bekijken

Controleer of de runtime goed is geïnstalleerd en geconfigureerd.

>[!TIP]
>U hebt verhoogde bevoegdheden nodig om `iotedge`-opdrachten uit te voeren. Nadat u zich de eerste keer na de installatie van de IoT Edge-runtime hebt afgemeld en opnieuw hebt aangemeld, worden uw machtigingen automatisch bijgewerkt. Gebruik tot die tijd **sudo** voorafgaand aan de opdrachten. 

1. Controleer of de Edge-beveiligingsdaemon wordt uitgevoerd als een systeemservice.

   ```bash
   sudo systemctl status iotedge
   ```

   ![Zie hoe de Edge-beveiligingsdeamon wordt uitgevoerd als een systeemservice](./media/quickstart-linux/iotedged-running.png)

2. Als u problemen met de service moet oplossen, haalt u de servicelogboeken op. 

   ```bash
   journalctl -u iotedge
   ```

3. Bekijk de modules die op uw apparaat worden uitgevoerd. 

   ```bash
   sudo iotedge list
   ```

   ![Eén module op uw apparaat bekijken](./media/quickstart-linux/iotedge-list-1.png)

Uw IoT Edge-apparaat is nu geconfigureerd. Het is gereed voor de uitvoering van modules die in de cloud zijn geïmplementeerd. 

## <a name="deploy-a-module"></a>Een module implementeren

Beheer uw Azure IoT Edge-apparaat vanuit de cloud om een module te implementeren waarmee telemetriegegevens worden verzonden naar IoT Hub.
![Diagram - Module implementeren vanuit cloud op apparaat](./media/quickstart-linux/deploy-module.png)

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]

## <a name="view-generated-data"></a>Gegenereerde gegevens weergeven

In deze snelstart hebt u een nieuw IoT Edge-apparaat gemaakt en de IoT Edge-runtime erop geïnstalleerd. Vervolgens hebt u de Azure-portal gebruikt om een IoT Edge-module te implementeren om te worden uitgevoerd op het apparaat zonder dat er wijzigingen aan het apparaat zelf hoefden te worden aangebracht. 

In dit geval worden met de module die u hebt gepusht voorbeeldgegevens gemaakt die u voor testen kunt gebruiken. De gesimuleerde temperatuursensormodule genereert omgevingsgegevens die u later kunt gebruiken voor testen. De gesimuleerde sensor bewaakt zowel een machine als de omgeving rond die machine. Deze sensor kan zich bijvoorbeeld in een serverruimte, in een fabriek of op een windturbine bevinden. Het bericht bevat informatie over de omgevingstemperatuur, de luchtvochtigheid, de machinetemperatuur en de druk, evenals een tijdstempel. In de IoT Edge-zelfstudies worden gegevens van deze module gebruikt als testgegevens voor analyses.

Open de opdrachtprompt op uw IoT Edge-apparaat opnieuw. Bevestig dat de module die vanuit de cloud is geïmplementeerd, op uw IoT Edge -apparaat wordt uitgevoerd:

   ```bash
   sudo iotedge list
   ```

   ![Drie modules op uw apparaat bekijken](./media/quickstart-linux/iotedge-list-2.png)

De berichten bekijken die vanuit de temperatuursensormodule worden verzonden:

   ```bash
   sudo iotedge logs SimulatedTemperatureSensor -f
   ```

   >[!TIP]
   >IoT Edge-opdrachten zijn hoofdlettergevoelig wanneer u naar modulenamen verwijst.

   ![De gegevens van uw module bekijken](./media/quickstart-linux/iotedge-logs.png)

U kunt de berichten ook zien binnenkomen bij uw IoT Hub door de [Azure IoT Hub Toolkit-extensie voor Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) (voorheen Azure IoT Toolkit-extensie) te gebruiken. 

## <a name="clean-up-resources"></a>Resources opschonen

Als u wilt doorgaan met de IoT Edge-zelfstudies, kunt u het apparaat gebruiken dat u hebt geregistreerd en ingesteld in deze snelstart. Anders kunt u de Azure-resources die u hebt gemaakt en de IoT Edge-runtime van uw apparaat verwijderen.

### <a name="delete-azure-resources"></a>Azure-resources verwijderen

Als u uw virtuele machine en IoT-hub in een nieuwe resourcegroep hebt gemaakt, kunt u die groep en alle bijbehorende resources verwijderen. Controleer de inhoud van de resourcegroep zorgvuldig om te na te gaan of er niets is dat u wilt behouden. Als u niet de hele groep wilt verwijderen, kunt u in plaats daarvan afzonderlijke resources verwijderen.

Verwijder de groep **IoTEdgeResources**.

   ```azurecli-interactive
   az group delete --name IoTEdgeResources 
   ```

### <a name="remove-the-iot-edge-runtime"></a>De IoT Edge-runtime verwijderen

Als u de installaties van uw apparaat wilt verwijderen, gebruikt u de volgende opdrachten.  

Verwijder de IoT Edge-runtime.

   ```bash
   sudo apt-get remove --purge iotedge
   ```

Verwijder de container-runtime.

   ```bash
   sudo apt-get remove --purge moby-cli
   sudo apt-get remove --purge moby-engine
   ```

## <a name="next-steps"></a>Volgende stappen

Deze snelstart is vereist voor alle IoT Edge-zelfstudies. U kunt doorgaan met elke andere zelfstudie om te leren hoe Azure IoT Edge u verder kan helpen bij het omzetten van uw gegevens in bedrijfsinzichten.

> [!div class="nextstepaction"]
> [Sensorgegevens filteren met behulp van een Azure-functie](tutorial-deploy-function.md)
