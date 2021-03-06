---
title: Active Directory verbinden met Azure Active Directory. | Microsoft Docs
description: Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit bieden voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD.
keywords: inleiding tot Azure AD Connect, overzicht Azure AD Connect, wat is Azure AD Connect, Active Directory installeren
services: active-directory
author: billmath
manager: mtillman
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.topic: get-started-article
ms.date: 11/28/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 1e85ab5eb0d8c96fb4c90332a2fbc41d216369f7
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53098936"
---
# <a name="what-is-hybrid-identity"></a>Wat is hybride identiteit? 

Vandaag de dag maken organisaties en bedrijven steeds meer gebruik van een mix van on-premises toepassingen en cloudtoepassingen.  Gebruikers hebben zowel on-premises als in de cloud toegang tot deze toepassingen nodig. Deze vereiste is een uitdaging geworden. 

De identiteitsoplossingen van Microsoft kunnen zowel on-premises als in de cloud worden gebruikt.  Met deze oplossingen wordt een algemene gebruikersidentiteit gemaakt voor verificatie en autorisatie voor alle resources, ongeacht de locatie. We noemen dit **hybride identiteit**.

Voor het verwezenlijken van hybride identiteit kan, afhankelijk van uw scenario's, gebruik worden gemaakt van drie verificatiemethoden.   Deze methoden zijn: 

- **[Synchronisatie van wachtwoord-hashes (PHS)](whatis-phs.md)**  
- **[Pass-through-verificatie (PTA)](how-to-connect-pta.md)**  
- **[Federatie](whatis-fed.md)** 

Met deze verificatiemethoden is tevens [eenmalige aanmelding](how-to-connect-sso.md) mogelijk.  Met eenmalige aanmelding worden gebruikers aangemeld als hun bedrijfsapparaten zijn verbonden met het bedrijfsnetwerk.

Zie [Selecteer de juiste verificatiemethode voor uw Azure Active Directory-oplossing voor hybride identiteit](https://docs.microsoft.com/azure/security/azure-ad-choose-authn) voor meer informatie. 

## <a name="common-scenarios-and-recommendations"></a>Veelvoorkomende scenario's en aanbevelingen 

Hieronder volgen enkele veelvoorkomende hybride identiteits- en beheerscenario's met aanbevelingen voor de meest geschikte hybride identiteitsoptie(s) voor elk scenario. 

|Ik wil graag:|PHS en eenmalige aanmelding<sup>1</sup>| PTA en eenmalige aanmelding<sup>2</sup> | AD FS<sup>3</sup>| 
|-----|-----|-----|-----| 
|nieuwe accounts van gebruikers, contactpersonen en groepen die in mijn on-premises Active Directory zijn gemaakt, automatisch met de cloud synchroniseren.|![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| ![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png) |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|mijn tenant instellen voor hybride Office 365-scenario's|![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| ![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png) |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|mijn gebruikers in staat stellen zich aan te melden bij cloudservices met hun on-premises wachtwoord|![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| ![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png) |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|eenmalige aanmelding implementeren met bedrijfsreferenties|![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| ![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png) |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)|  
|ervoor zorgen dat wachtwoord-hashes in de cloud worden opgeslagen| |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)|![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|oplossingen voor meervoudige verificatie in de cloud mogelijk maken| |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)|![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|oplossingen voor meervoudige verificatie on-premises mogelijk maken| | |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|verificatie van smartcards voor mijn gebruikers mogelijk maken<sup>4</sup>| | |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 
|meldingen voor verlopen wachtwoorden weergeven in de Office-portal en op het Windows 10-bureaublad| | |![Aanbevolen](./media/whatis-hybrid-identity/ic195031.png)| 

> <sup>1</sup> Wachtwoordhashsynchronisatie met eenmalige aanmelding. 
> 
> <sup>2</sup> Pass-through-verificatie en eenmalige aanmelding.  
> 
> <sup>3</sup> Federatieve eenmalige aanmelding met AD FS.  
>  
> <sup>4</sup> AD FS kan worden geïntegreerd met uw Enterprise PKI om aanmelding met certificaten toe te staan. Deze certificaten kunnen voorlopige certificaten zijn die worden geïmplementeerd via vertrouwde inrichtingskanalen, zoals MDM-, GPO- of smartcardcertificaten (waaronder PIV/CAC-kaarten) of Hello voor Bedrijven (cert-trust). Zie [dit blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/) (Engelstalig) voor meer informatie over ondersteuning voor smartcardverificatie. 
> 

## <a name="next-steps"></a>Volgende stappen 

- [Wat zijn Azure AD Connect en Connect Health?](whatis-azure-ad-connect.md) 
- [Wat is synchronisatie van wachtwoord-hashes (PHS)?](whatis-phs.md) 
- [Wat is pass-through-verificatie (PTA)?](how-to-connect-pta.md) 
- [Wat is federatie?](whatis-fed.md) 
- [Wat is eenmalige aanmelding?](how-to-connect-sso.md) 

