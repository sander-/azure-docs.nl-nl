---
title: 'Snelstart: Azure AD-selfservice voor wachtwoordherstel'
description: In deze snelstart gaat u de Azure AD-selfservice voor wachtwoordherstel snel configureren, zodat gebruikers hun eigen wachtwoorden opnieuw kunnen instellen
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: quickstart
ms.date: 07/17/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: d04d27ee6136edec8d9af16f9133cf9a7cc0720c
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53311555"
---
# <a name="quickstart-self-service-password-reset"></a>Snelstart: Self-service voor wachtwoord opnieuw instellen

In deze snelstart wordt het configureren van de selfservice voor wachtwoordherstel (SSPR) uitgelegd. Deze service biedt een eenvoudige manier voor IT-beheerders om gebruikers in staat te stellen hun eigen wachtwoord opnieuw in te stellen of account te ontgrendelen.

## <a name="prerequisites"></a>Vereisten

* Een werkende Azure AD-tenant waarop minimaal een proeflicentie is ingeschakeld.
* Een account met de bevoegdheden van een globale beheerder.
* Zie het artikel [Snelstart: Nieuwe gebruikers toevoegen aan Azure Active Directory](../add-users-azure-active-directory.md) als een testgebruiker zonder beheerdersbevoegdheden een wachtwoord heeft dat u kent, en u een gebruiker moet maken.
* Zie het artikel [Een groep maken en leden toevoegen in Azure Active Directory](../active-directory-groups-create-azure-portal.md) als u een pilotgroep hebt om mee te testen waarvan de testgebruiker zonder beheerdersbevoegdheden lid is, en u een groep wilt maken.

## <a name="enable-self-service-password-reset"></a>Selfservice voor wachtwoordherstel inschakelen

> [!VIDEO https://www.youtube.com/embed/Pa0eyqjEjvQ]

1. Selecteer vanuit uw bestaande Azure AD-tenant in **Azure Portal** onder **Azure Active Directory** de optie **Wachtwoord opnieuw instellen**.

2. Op de pagina **Eigenschappen** kiest u onder **Selfservice voor wachtwoord opnieuw instellen is ingeschakeld** de optie **Geselecteerd**.
    * Selecteer bij **Groep selecteren** de pilotgroep die u hebt gemaakt als onderdeel van het gedeelte over vereisten in dit artikel.
    * Klik op **Opslaan**.

3. Op de pagina **Verificatiemethoden** kiest u het volgende:
   * Het aantal methoden dat is vereist om het wachtwoord opnieuw in te stellen: **1**
   * Methoden voor gebruikers:
      * **Mobiele telefoon**
      * **Telefoon (werk)**
   * Klik op **Opslaan**.

    ![Verificatie][Authentication]

4. Op de pagina **Registratie** kiest u het volgende:
   * Vereisen dat gebruikers zich bij aanmelding registreren: **Ja**
   * Het aantal dagen instellen waarna gebruikers wordt gevraagd om de verificatiegegevens opnieuw te bevestigen: **365**

## <a name="test-self-service-password-reset"></a>Selfservice voor wachtwoord opnieuw instellen testen

We gaan nu de configuratie van de selfservice voor wachtwoordherstel met een testgebruiker testen. Aangezien Microsoft sterke verificatievereisten afdwingt voor Azure-beheerdersaccounts, kan het testen met een beheerdersaccount het resultaat beïnvloeden. Zie ons [artikel over wachtwoordbeleid](concept-sspr-policy.md) voor meer informatie over het wachtwoordbeleid voor beheerders.

1. Open een nieuw browservenster in de InPrivate- of incognitomodus en browse naar [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).
2. Meld u aan met een testgebruiker die geen beheerder is en registreer uw telefoon voor verificatie.
3. Als u klaar bent, klikt u op de knop **ziet er goed uit** en sluit u het browservenster.
4. Open een nieuw browservenster in de InPrivate- of incognitomodus en browse naar [https://aka.ms/sspr](https://aka.ms/sspr).
5. Geef de gebruikers-id van uw testgebruiker die geen beheerder is op, plus de tekens uit de CAPTCHA, en klik vervolgens op **Volgende**.
6. Volg de verificatiestappen om uw wachtwoord opnieuw in te stellen

## <a name="clean-up-resources"></a>Resources opschonen

Selfservice voor wachtwoordherstel kan eenvoudig worden uitgeschakeld. Open uw Azure AD-tenant en ga naar **Eigenschappen** > **Wachtwoord opnieuw instellen** en selecteer vervolgens **Geen** onder **Selfservice voor wachtwoord opnieuw instellen is ingeschakeld**.

## <a name="next-steps"></a>Volgende stappen

In deze snelstart hebt u geleerd hoe u selfservice voor wachtwoordherstel snel kunt configureren voor uw cloudgebruikers. Als u wilt weten hoe u een gedetailleerdere implementatie uitvoert, kunt u verder gaan met onze implementatiehandleiding.

> [!div class="nextstepaction"]
> [Selfservice voor wachtwoordherstel implementeren](howto-sspr-deployment.md)

[Authentication]: ./media/quickstart-sspr/sspr-authentication-methods.png "Azure Active Directory-verificatiemethoden die beschikbaar zijn en hoeveel er vereist zijn"
