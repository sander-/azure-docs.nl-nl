---
title: Een Universal Windows Platform-app (UWP) maken die gebruikmaakt van Mobile Apps | Microsoft Docs
description: Volg deze zelfstudie om aan de slag te gaan met back-ends voor mobiele apps van Azure voor Universal Windows Platform (UWP)-app-ontwikkeling in C#, Visual Basic of JavaScript.
services: app-service\mobile
documentationcenter: windows
author: conceptdev
manager: crdun
editor: ''
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/17/2018
ms.author: crdun
ms.openlocfilehash: c8bd6430b362fde81c3133c2c16cf369aa050103
ms.sourcegitcommit: 2469b30e00cbb25efd98e696b7dbf51253767a05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/06/2018
ms.locfileid: "52999377"
---
# <a name="create-a-windows-app"></a>Een Windows-app maken

[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overzicht

Deze zelfstudie laat zien hoe u een back-endservice toevoegt aan een Universal Windows Platform (UWP)-app in de cloud. Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie. Hier volgen enkele schermopnamen van een voltooide app:

![Voltooide bureaublad-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)

Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor UWP-apps.

## <a name="prerequisites"></a>Vereisten

Voor het voltooien van deze zelfstudie hebt u het volgende nodig:

* Een actief Azure-account. Als u geen account hebt, kunt u zich aanmelden voor een proefversie van Azure en maximaal tien gratis mobiele apps krijgen die u ook na de proefperiode kunt blijven gebruiken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
* [Visual Studio Community 2017]

## <a name="create-a-new-azure-mobile-app-backend"></a>Een nieuwe back-end voor mobiele apps van Azure maken

Volg deze stappen voor het maken van een nieuwe back-end voor mobiele apps.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen. Nu gaat u een serverproject downloaden voor een eenvoudige back-end voor takenlijsten en deze publiceren naar Azure.

## <a name="configure-the-server-project"></a>Het serverproject configureren

[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a>Het clientproject downloaden en uitvoeren

Zodra u de back-end voor mobiele apps hebt geconfigureerd, kunt u een nieuwe client-app maken of een bestaande app wijzigen om verbinding te maken met Azure. In deze sectie downloadt u een project voor een voorbeeld-UWP-app die is aangepast om verbinding te kunnen maken met de back-end van uw mobiele apps.

1. Op de blade **Snel starten** voor de back-end voor uw mobile app klikt u op **Een nieuwe app maken** > **Downloaden**. Pak de gecomprimeerde projectbestanden uit op de lokale computer.

    ![Het project Windows-snelstartgids downloaden](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)

2. Open het UWP-project en druk op F5 om de app te implementeren en uit te voeren.
3. Typ zinvolle tekst in de app, zoals *Voltooi de zelfstudie*, in het tekstvak **Nieuwe taak invoegen** en klik op **Opslaan**.

    ![Windows-snelstartgids: bureaublad voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Hierdoor wordt een POST-aanvraag verzonden naar de nieuwe back-end voor mobiele apps die wordt gehost in Azure.

> [!TIP]
> U kunt het UWP-app-project aan dezelfde oplossing toevoegen als het serverproject, mits u de .NET-back-end gebruikt. Hierdoor kunt u zowel de app als de back-end makkelijker debuggen en testen in dezelfde Visual-Studio-oplossing. Als u een UWP-app-project aan de back-endoplossing wilt toevoegen, dient u Visual Studio 2017 te gebruiken.

## <a name="next-steps"></a>Volgende stappen

* [Verificatie toevoegen aan uw app](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Ontdek hoe u gebruikers van uw app verifieert met een id-provider.
* [Pushmeldingen toevoegen aan uw app](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Informatie over het toevoegen van ondersteuning van pushmeldingen aan uw app en het configureren van de backend voor mobiele apps voor gebruik van Azure Notification Hubs voor het verzenden van pushmeldingen.
* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Informatie over het toevoegen van offlineondersteuning aan uw app met een back-end voor mobiele apps. Met offlinesynchronisatie kunnen eindgebruikers interactie aangaan met een mobiele app&mdash;gegevens weergeven, toevoegen of wijzigen&mdash;ook als er geen netwerkverbinding is.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: https://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: https://go.microsoft.com/fwLink/p/?LinkID=534203
