---
title: Veelgestelde vragen over Azure Active Directory-rapporten | Microsoft Docs
description: Veelgestelde quesitons rond Azure Active Directory-rapporten.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: report-monitor
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 98a1dd3fb3fd733cc17ac9c6ccf9d0dfc77737e1
ms.sourcegitcommit: b0f39746412c93a48317f985a8365743e5fe1596
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52868018"
---
# <a name="frequently-asked-questions-around-azure-active-directory-reports"></a>Veelgestelde vragen over Azure Active Directory-rapporten

In dit artikel bevat antwoorden op veelgestelde vragen over Azure Active Directory (Azure AD) rapportage. Zie [Azure Active Directory-rapportage](overview-reports.md) voor meer informatie. 

## <a name="getting-started"></a>Aan de slag 

**V: ik momenteel gebruiken de https://graph.windows.net/&lt; tenant-naam&gt;/reports/ eindpunt API's voor het pull-Azure AD-controle en gebruik van de geïntegreerde toepassing via een programma in ons systeem reporting-rapporten. Wat moet ik overschakelen naar?**

**A:** opzoeken de [API-verwijzing](https://developer.microsoft.com/graph/) om te zien hoe u kunt [de API's gebruiken voor toegang tot activiteitenrapporten](concept-reporting-api.md). Dit eindpunt heeft twee rapporten (**Audit** en **aanmeldingen**) Hier vindt u alle gegevens die u hebt verkregen in het oude API-eindpunt. Dit nieuwe eindpunt heeft ook een rapport-aanmeldingen met de Azure AD Premium-licentie die u gebruiken kunt om app-gebruik, gebruik van het apparaat en aanmelding bij gebruikersgegevens te verkrijgen.

--- 

**V: ik momenteel gebruiken de https://graph.windows.net/&lt; tenant-naam&gt;/reports/ eindpunt API's voor het ophalen van Azure AD-beveiligingsrapporten (specifieke typen detectie, zoals de referenties zijn gelekt of aanmeldingen vanaf anonieme IP-adressen) in onze reporting systemen via een programma. Wat moet ik overschakelen naar?**

**A:** kunt u de [risicogebeurtenissen Identity Protection API](../identity-protection/graph-get-started.md) naar beveiligingsdetecties toegang via Microsoft Graph. Deze nieuwe indeling biedt meer flexibiliteit in hoe u van gegevens, met Geavanceerd filteren, mapselectie en meer opvragen kunt, en risicogebeurtenissen standaardiseert in één type voor eenvoudiger integratie met siem's en andere hulpmiddelen voor het verzamelen van gegevens. Omdat de gegevens zich in een andere indeling, kunt u een nieuwe query voor uw oude query's niet vervangen. Echter, [de nieuwe API maakt gebruik van Microsoft Graph](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/identityriskevent), dit is de Microsoft-standaard voor deze API's als Office 365 of Azure AD. U begint de overgang naar deze nieuwe standard-platform, zodat het werk vereist kunt uitbreiden van uw huidige investeringen in MS Graph of de help.

--- 

**V: hoe krijg ik een premium-licentie?**

**A:** Zie [aan de slag met Azure Active Directory Premium](../fundamentals/active-directory-get-started-premium.md) upgrade uw versie van Azure Active Directory.

---

**V: hoe snel moet ik activiteiten gegevens zien nadat u een premium-licentie?**

**A:** als u al gegevens hebt die activiteiten als een gratis licentie, dan kunt u deze meteen zien. Als u geen gegevens, duurt het een of twee dagen voor de gegevens worden weergegeven in de rapporten.

---

**V: kan ik van afgelopen maand gegevens zien nadat u een Azure AD premium-licentie?**

**A:** als u hebt onlangs is overgeschakeld naar een premiumversie (met inbegrip van een evaluatieversie), u kunt gegevens van 7 dagen in eerste instantie zien. Wanneer gegevens worden bij elkaar opgeteld, ziet u gegevens voor de afgelopen 30 dagen.

---

**V: ik moet een globale beheerder om te zien van de activiteit aanmeldingen bij de Azure portal of het opvragen van gegevens via de API?**

**A:** Nee, u kunt ook toegang tot de rapportagegegevens via de portal of via de API als u een **Beveiligingslezer** of **beveiligingsbeheerder** voor de tenant. Natuurlijk **globale beheerders** hebben ook toegang tot deze gegevens.

---


## <a name="activity-logs"></a>Activiteitenlogboeken


**V: Wat is de bewaarperiode voor activiteitenlogboeken (Audit en -aanmeldingen) in Azure portal?** 

**A:** de volgende tabel bevat de bewaarperiode voor activiteitenlogboeken. Zie voor meer informatie, [bewaarbeleid voor gegevens voor Azure AD-rapporten](reference-reports-data-retention.md).

| Rapport                 | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Controlelogboeken             | 7 dagen        | 30 dagen             | 30 dagen             |
| Aanmeldingen               | N/A           | 30 dagen             | 30 dagen             |
| Azure MFA-gebruik        | 30 dagen       | 30 dagen             | 30 dagen             |

--- 

**V: hoe lang duurt het tot ik de activiteitsgegevens zien kan nadat ik mijn taak hebt voltooid?**

**A:** auditlogboeken hebben een latentie, variërend van 15 minuten tot een uur. Aanmelden activiteitenlogboeken kunnen tot maximaal twee uur voor sommige records tussen 15 minuten duren.

---

**V: kan ik Office 365-activiteitenlogboekinformatie via Azure portal krijgen?**

**A:** Hoewel Office 365-activiteit en Azure AD-activiteit logboeken delen veel directoryresources, als u wilt dat een volledig overzicht van de Office 365-activiteitenlogboeken moet gaat u naar het Office 365-beheercentrum om op te halen van Office 365-activiteitenlogboekinformatie.

---

**Vraag: welke API's gebruik ik voor informatie over Office 365-activiteitenlogboeken?**

**A:** gebruiken de [Management API's van Office 365](https://docs.microsoft.com/office/office-365-management-api/office-365-management-apis-overview) voor toegang tot de Office 365-activiteitenlogboeken via een API.

---

**V: hoe veel records ik kunt downloaden vanuit Azure portal?**

**A:** u kunt maximaal 5000 records downloaden via de Azure-portal. De records worden gesorteerd op *meest recente* en standaard, krijgt u de meest recente 5000 records.

---

## <a name="risky-sign-ins"></a>Riskante aanmeldingen

**Vraag: Er is een risicogebeurtenis in Identity Protection, maar ik zie niet bijbehorende aanmelden in het rapport-aanmeldingen. Is dit verwacht?**

**A:** Ja, Identity Protection risico's voor alle verificatiestromen beoordeelt of interactieve of niet-interactieve. Alleen rapport voor alle aanmeldingen wordt echter alleen de interactieve aanmeldingen.

---

**V: hoe weet ik waarom een aanmelding bij of een gebruiker is gemarkeerd riskante in Azure portal?**

**A:** hebt u een **Azure AD Premium** abonnement, u kunt meer informatie over de onderliggende risicogebeurtenissen door het selecteren van de gebruiker in **gebruikers die zijn gemarkeerd voor risico's** of door het selecteren van een record in de  **Riskante aanmeldingen** rapport. Als u hebt een **gratis** of **Basic** abonnement, dan hebt u de gebruikers op risico's en rapporten over riskante aanmeldingen kunt weergeven, maar kunt u de onderliggende gegevens van risicogebeurtenissen niet zien.

---

**V: hoe worden de IP-adressen in de aanmeldingen en het rapport riskante aanmeldingen berekend?**

**A:** IP-adressen worden uitgegeven zodanig dat er is geen definitieve verbinding tussen een IP-adres en waar de computer met dit adres zich fysiek bevindt. Toewijzing van IP-adressen is nog gecompliceerder door factoren zoals mobiele providers en VPN's uitgeven van IP-adressen uit de centrale pools vaak zeer ver ligt waar het client-apparaat daadwerkelijk wordt gebruikt. In Azure AD-rapporten is IP-adres converteren naar een fysieke locatie momenteel een best-effort op basis van traceringen, register, omgekeerde zoekopdrachten en andere gegevens. 

---

**V: wat de risicogebeurtenis overheen "Aanmelden met extra risico gedetecteerd" biedt?**

**A:** zodat u inzicht in alle riskante aanmeldingen in uw omgeving, "aanmelden met de extra risico gedetecteerd" fungeert als tijdelijke aanduiding voor aanmeldingen voor detecties die uitsluitend tot de Azure AD Identity Protection-abonnees behoren.

---

## <a name="conditional-access"></a>Voorwaardelijke toegang

**V: Wat is er nieuw in deze functie?**

**A:** klanten kunnen nu beleidsregels voor voorwaardelijke toegang via alle aanmeldingen rapport oplossen. Klanten kunnen de status voor voorwaardelijke toegang en informatie over de details van het beleid toegepast op de aanmelding en het resultaat voor elk beleid te lezen.

**V: hoe ga ik aan de slag?**

**A:** aan de slag:
    * Navigeer naar het rapport aanmeldingen in de [Azure-portal](https://portal.azure.com). 
    * Klik op de aanmelding die u wilt oplossen.
    * Navigeer naar de **voorwaardelijke toegang** tabblad. Hier vindt u alle beleidsregels die invloed hebben de aanmelding en het resultaat voor elk beleid. 
    
**V: wat zijn alle mogelijke waarden voor de status voor voorwaardelijke toegang?**

**A:** status voor voorwaardelijke toegang kan de volgende waarden hebben:
    * **Niet toegepast**: dit betekent dat er geen CA-beleid met de gebruiker en de app binnen het bereik is. 
    * **Succes**: dit betekent dat er een CA-beleid met de gebruiker en de app binnen het bereik is en CA-beleid is voldaan. 
    * **Fout**: dit betekent dat er een CA-beleid met de gebruiker en de app binnen het bereik is en CA-beleid niet wordt voldaan. 
    
**V: wat zijn alle mogelijke waarden voor het resultaat van de beleid voor voorwaardelijke toegang?**

**A:** beleid voor voorwaardelijke toegang kan hebben de volgende resultaten:
    * **Succes**: Er is met succes is voldaan aan het beleid.
    * **Fout**: het beleid is niet voldaan aan.
    * **Niet toegepast**: dit zijn omdat het niet voldeed aan de voorwaarden van het beleid.
    * **Niet ingeschakeld**: dit wordt veroorzaakt door het beleid is uitgeschakeld. 
    
**V: de beleidsnaam in het rapport voor alle aanmelden komt niet overeen met de naam van het beleid in de CA. Waarom is dat?**

**A:** de naam van het beleid in het rapport voor alle aanmelden is gebaseerd op de naam van de CA-beleid op het moment van de aanmelding. Dit kan niet consistent met de naam van het beleid in de CA zijn, als u de beleidsnaam later, dat wil zeggen, na de aanmelding bijgewerkt.

**V: Mijn aanmelding is geblokkeerd vanwege een beleid voor voorwaardelijke toegang, maar het rapport van aanmeldingsactiviteiten bevat of de aanmelding is geslaagd. Waarom is dat?**

**A:** op dit moment dat het rapport niet nauwkeurige resultaten voor Exchange ActiveSync-scenario's kan weergeven wanneer voorwaardelijke toegang wordt toegepast. Kunnen er gevallen wanneer het resultaat aanmelden in het rapport een geslaagde aanmelding bevat, maar de aanmelding daadwerkelijk is mislukt vanwege een beleid voor voorwaardelijke toegang. 
