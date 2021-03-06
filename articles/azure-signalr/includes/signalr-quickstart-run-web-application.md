---
title: bestand opnemen
description: bestand opnemen
author: anthonychu
ms.service: signalr
ms.topic: include
ms.date: 09/14/2018
ms.author: antchu
ms.custom: include file
ms.openlocfilehash: 73d40bfb5a7e691cead5a84be70398e9cbf6656a
ms.sourcegitcommit: 1c1f258c6f32d6280677f899c4bb90b73eac3f2e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/11/2018
ms.locfileid: "53262748"
---
## <a name="run-the-web-application"></a>De webtoepassing uitvoeren

1. Voor uw gemak wordt een voorbeeldwebtoepassing van één pagina in GitHub gehost. Open uw browser naar [https://azure-samples.github.io/signalr-service-quickstart-serverless-chat/demo/chat/](https://azure-samples.github.io/signalr-service-quickstart-serverless-chat/demo/chat/).

    > [!NOTE]
    > De bron van het HTML-bestand bevindt zich in [/docs/demo/chat/index.html](https://github.com/Azure-Samples/signalr-service-quickstart-serverless-chat/blob/master/docs/demo/chat/index.html).

1. Wanneer u om de basis-URL van de functie-app wordt gevraagd, voert u *http://localhost:7071* in.

1. Voer een gebruikersnaam in wanneer hierom wordt gevraagd.

1. De webtoepassing roept de functie *GetSignalRInfo* in de functie-app aan om de verbindingsgegevens voor het verbinden met Azure SignalR Service op te halen. Wanneer de verbinding is voltooid, wordt het invoervak voor het chat-bericht weergegeven.

1. Typ een bericht en druk op Enter. Het bericht wordt verzonden naar de functie *SendMessage* in de Azure-functie-app die vervolgens de SignalR-uitvoerbinding gebruikt om het bericht naar alle verbonden clients te verzenden. Als alles goed werkt, wordt het bericht weergegeven in de toepassing.

    ![De toepassing uitvoeren](../media/signalr-quickstart-azure-functions-csharp/signalr-quickstart-run-application.png)

1. Open een ander exemplaar van de webtoepassing in een ander browservenster. U ziet dat alle verzonden berichten in alle exemplaren van de toepassing worden weergegeven.