---
title: Valideren van de oorspronkelijke leveranciers (OEM)-pakketten in de Azure Stack-validatie als een Service | Microsoft Docs
description: Informatie over het valideren van de oorspronkelijke leveranciers (OEM)-pakketten met validatie uit als een Service.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 1/07/2019
ms.author: mabrigg
ms.reviewer: johnhas
ROBOTS: NOINDEX
ms.openlocfilehash: 5ba290f442f4c27b510538d7c1f7b5e27467efc5
ms.sourcegitcommit: f4b78e2c9962d3139a910a4d222d02cda1474440
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/12/2019
ms.locfileid: "54246650"
---
# <a name="validate-oem-packages"></a>OEM-pakketten valideren

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

Wanneer er een wijziging in de firmware of stuurprogramma's voor de validatie van een voltooide oplossing is, kunt u een nieuw pakket voor OEM testen. Wanneer de test van het pakket is verstreken, wordt het ondertekend door Microsoft. Uw test moet het bijgewerkte OEM-uitbreidingspakket met de stuurprogramma's en firmware die zijn geslaagd voor Windows Server-logo en pc's tests bevatten.

[!INCLUDE [azure-stack-vaas-workflow-validation-completion](includes/azure-stack-vaas-workflow-validation-completion.md)]

> [!IMPORTANT]
> Bekijk voordat u uploaden of het verzenden van pakketten, [een OEM-pakket maken](azure-stack-vaas-create-oem-package.md) voor de indeling van de verwachte pakket en de inhoud.

## <a name="managing-packages-for-validation"></a>Beheren van pakketten voor validatie

Wanneer u de **validatie van het pakket** werkstroom voor het valideren van een pakket, moet u een URL naar een **Azure Storage-blob**. Deze blob is het OEM-pakket dat op de oplossing is geïnstalleerd tijdens de implementatie. Maken van de blob met behulp van de Azure Storage-Account die u hebt gemaakt tijdens de installatie (Zie [instellen dat uw gevalideerd als een serviceresources](azure-stack-vaas-set-up-resources.md)).

### <a name="prerequisite-provision-a-storage-container"></a>Voorwaarde: Inrichten van een storage-container

Maak een container in uw storage-account voor pakket-blobs. Deze container kan worden gebruikt voor al uw validatie van het pakket wordt uitgevoerd.

1. In de [Azure Portal](https://portal.azure.com), gaat u naar het storage-account hebt gemaakt in [instellen dat uw gevalideerd als een serviceresources](azure-stack-vaas-set-up-resources.md).
2. Op de blade links onder **Blob-Service**selecteert op **Containers**.
3. Selecteer **+ Container** in het menu van de balk en geef een naam voor de container, bijvoorbeeld `vaaspackages`.

### <a name="upload-package-to-storage-account"></a>Pakket uploaden naar storage-account

1. Bereid het pakket dat u wilt valideren. Als het pakket meerdere bestanden heeft, comprimeren in een `.zip` bestand.
2. In de [Azure Portal](https://portal.azure.com), selecteert u de pakket-container en uploaden van het pakket door te selecteren op **uploaden** in de menubalk.
3. Selecteer het pakket `.zip` dat u wilt uploaden. Laat de standaardwaarden staan **Blobtype** (dat wil zeggen, **blok-Blob**) en **blokgrootte**.

> [!NOTE]
> Zorg ervoor dat de `.zip` inhoud worden geplaatst in de hoofdmap van de `.zip` bestand. Er mogen zich geen submappen in het pakket.

### <a name="generate-package-blob-url-for-vaas"></a>URL van het pakket blob voor VaaS genereren

Bij het maken van een **validatie van het pakket** werkstroom in de portal VaaS, moet u een URL naar de Azure Storage-blob met uw pakket opgeven.

#### <a name="option-1-generating-an-account-sas-url"></a>Optie 1: Genereren van een account-SAS-URL

1. In de [Azure-portal](https://portal.azure.com/), gaat u naar uw storage-account en navigeer naar de ZIP met uw pakket

2. Selecteer **SAS genereren** in het contextmenu

3. Selecteer **lezen** van **machtigingen**

4. Instellen **begintijd** op de huidige tijd en **eindtijd** aan ten minste 48 uur vanaf **begintijd**. Als u andere tests worden uitgevoerd met hetzelfde pakket, kunt u overwegen verhogen **eindtijd** voor de lengte van de test. Alle tests gepland via VaaS na **eindtijd** zal mislukken en een nieuwe SAS moet worden gegenereerd.

5. Selecteer **blob SAS-token en URL genereren**

Gebruik **Blob SAS-URL** bij het starten van een nieuwe **validatie van het pakket** werkstroom in de portal VaaS.

#### <a name="option-2-using-public-read-container"></a>Optie 2: Met behulp van openbare lezen container

> [!CAUTION]
> Deze optie, opent u de container voor anonieme toegang voor alleen-lezen.

1. Verleen **openbare leestoegang voor blobs alleen** naar de container van het pakket door de instructies in de sectie [anonieme gebruikersmachtigingen verlenen voor containers en blobs](https://docs.microsoft.com/azure/storage/storage-manage-access-to-resources#grant-anonymous-users-permissions-to-containers-and-blobs).

2. Selecteer op de pakket-blob in de container in de container pakket om het eigenschappendeelvenster te openen.

3. Kopieer de **URL**. Deze waarde gebruiken bij het starten van een nieuwe **validatie van het pakket** werkstroom in de portal VaaS.

## <a name="apply-monthly-update"></a>Maandelijkse update van toepassing

[!INCLUDE [azure-stack-vaas-workflow-section_update-azs](includes/azure-stack-vaas-workflow-section_update-azs.md)]

## <a name="create-a-package-validation-workflow"></a>Een werkstroom voor validatie van het pakket maken

1. Aanmelden bij de [VaaS portal](https://azurestackvalidation.com).

2. [!INCLUDE [azure-stack-vaas-workflow-step_select-solution](includes/azure-stack-vaas-workflow-step_select-solution.md)]

3. Selecteer **Start** op de **validatie van het pakket** tegel.

    ![Pakket validaties werkstroom tegel](media/tile_validation-package.png)

4. [!INCLUDE [azure-stack-vaas-workflow-step_naming](includes/azure-stack-vaas-workflow-step_naming.md)]

5. Voer de URL van de Azure-opslag-blob naar de OEM-pakket dat is geïnstalleerd op de oplossing tijdens de implementatie. Zie voor instructies [pakket blob URL genereren voor VaaS](#generate-package-blob-url-for-vaas).

6. [!INCLUDE [azure-stack-vaas-workflow-step_upload-stampinfo](includes/azure-stack-vaas-workflow-step_upload-stampinfo.md)]

7. [!INCLUDE [azure-stack-vaas-workflow-step_test-params](includes/azure-stack-vaas-workflow-step_test-params.md)]

    > [!NOTE]
    > Omgeving parameters kunnen niet worden gewijzigd na het maken van een werkstroom.

8. [!INCLUDE [azure-stack-vaas-workflow-step_tags](includes/azure-stack-vaas-workflow-step_tags.md)]

9. [!INCLUDE [azure-stack-vaas-workflow-step_submit](includes/azure-stack-vaas-workflow-step_submit.md)]
    U wordt omgeleid naar de pagina overzicht van tests.

## <a name="run-package-validation-tests"></a>Pakket validatietests uit te voeren

1. In de **validatie van het pakket test samenvatting** pagina, ziet u een lijst van de tests voor het voltooien van de validatie is vereist. Tests in deze werkstroom wordt uitgevoerd voor ongeveer 24 uur.

    In de werkstromen validatie **planning** een test maakt gebruik van het niveau van de werkstroom algemene parameters die u hebt opgegeven tijdens het maken van de werkstroom (Zie [werkstroom algemene parameters voor Azure Stack-validatie als een Service](azure-stack-vaas-parameters.md)). Als een van de parameterwaarden test ongeldig geworden, moet u ze resupply volgens de instructies in [wijzigen werkstroomparameters](azure-stack-vaas-monitor-test.md#change-workflow-parameters).

    > [!NOTE]
    > Een bestaand exemplaar van een validatietest planning maakt een nieuw exemplaar in plaats van het oude-exemplaar in de portal. Logboeken voor het oude exemplaar worden bewaard, maar zijn niet toegankelijk is vanaf de portal.  
    Wanneer een test is voltooid en de **planning** actie wordt uitgeschakeld.

2. Selecteer de agent die de test wordt uitgevoerd. Voor informatie over het toevoegen van lokale WebTest-agents worden uitgevoerd, Zie [implementeren van de lokale agent](azure-stack-vaas-local-agent.md).

3. Stap voor elk van de volgende tests uit, 4 en 5:
    - OEM-extensie pakket verificatie
    - Engine voor cloud-simulatie

4. Selecteer **planning** in het contextmenu om een prompt voor het plannen van de test-exemplaar te openen.

5. Controleer de testparameters en selecteer vervolgens **indienen** voor het plannen van de test voor de uitvoering.

Wanneer alle tests zijn voltooid, stuurt u de naam van uw oplossing VaaS en validatie van het pakket naar [ vaashelp@microsoft.com ](mailto:vaashelp@microsoft.com) om aan te vragen pakket ondertekenen.

## <a name="next-steps"></a>Volgende stappen

- [Controleren en beheren van tests in de portal VaaS](azure-stack-vaas-monitor-test.md)