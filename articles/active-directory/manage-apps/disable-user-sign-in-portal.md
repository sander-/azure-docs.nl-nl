---
title: Gebruikersaanmeldingen voor een enterprise-app in Azure Active Directory uitschakelen | Microsoft Docs
description: Het uitschakelen van een bedrijfstoepassing, zodat er geen gebruikers me niet bij Azure Active Directory aanmelden kunnen
services: active-directory
documentationcenter: ''
author: barbkess
manager: daveba
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/28/2017
ms.author: barbkess
ms.reviewer: asteen
ms.custom: it-pro
ms.openlocfilehash: 4355b1a17f3cf9c8d25b97d63a39cdf8343181b8
ms.sourcegitcommit: cf88cf2cbe94293b0542714a98833be001471c08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/23/2019
ms.locfileid: "54476271"
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Gebruikersaanmeldingen voor een enterprise-app in Azure Active Directory uitschakelen
Het is eenvoudig om uit te schakelen van een bedrijfstoepassing, zodat er geen gebruikers me niet bij Azure Active Directory (Azure AD aanmelden kunnen). U moet de juiste machtigingen voor het beheren van de enterprise-app hebt en u moet globale beheerder voor de map.

## <a name="how-do-i-disable-user-sign-ins"></a>Hoe kan ik gebruikersaanmeldingen uitschakelen?
1. Meld u aan bij [Azure Portal](https://portal.azure.com) met een account van een globale beheerder voor de directory.
2. Selecteer **alle services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.
3. Op de **Azure Active Directory** -  ***directoryname*** deelvenster (dat wil zeggen, de Azure AD voor de map die u beheert), selecteer **bedrijfstoepassingen**.

    ![Bedrijfsapps openen](./media/disable-user-sign-in-portal/open-enterprise-apps.png)
4. Op de **bedrijfstoepassingen** venster **alle toepassingen**. U ziet een lijst van de apps die u kunt beheren.
5. Op de **bedrijfstoepassingen - alle toepassingen** deelvenster, selecteert u een app.
6. Op de ***appname*** deelvenster (dat wil zeggen, het deelvenster met de naam van de geselecteerde app in de titel), selecteer **eigenschappen**.

    ![De opdracht Alles toepassingen selecteren](./media/disable-user-sign-in-portal/select-app.png)
7. Op de ***appname*** - **eigenschappen** venster **Nee** voor **ingeschakeld voor gebruikers om aan te melden?**.
8. Selecteer de **opslaan** opdracht.

## <a name="next-steps"></a>Volgende stappen
* [Mijn groepen bekijken](../fundamentals/active-directory-groups-view-azure-portal.md)
* [Een gebruiker of groep toewijzen aan een enterprise-app](assign-user-or-group-access-portal.md)
* [De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app](remove-user-or-group-access-portal.md)
* [De naam of het logo van een zakelijke app wijzigen](change-name-or-logo-portal.md)
