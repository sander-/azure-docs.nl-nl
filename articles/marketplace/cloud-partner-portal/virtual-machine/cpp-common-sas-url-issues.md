---
title: Veelvoorkomende problemen met SAS-URL en oplossingen voor de Azure Marketplace | Microsoft Docs
description: Lijst met algemene problemen rond de handtekening voor gedeelde toegang URI's en mogelijke oplossingen.
services: Azure, Marketplace, Cloud Partner Portal,
documentationcenter: ''
author: pbutlerm
manager: Patrick.Butler
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 09/27/2018
ms.author: pbutlerm
ms.openlocfilehash: b20b1506dfcd32ea7d5bfca0847393d1652afb78
ms.sourcegitcommit: 17633e545a3d03018d3a218ae6a3e4338a92450d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/22/2018
ms.locfileid: "49639702"
---
# <a name="common-sas-url-issues-and-fixes"></a>Veelvoorkomende problemen met SAS-URL en oplossingen

De volgende tabel bevat enkele van de algemene problemen bij het werken met handtekeningen voor gedeelde toegang (die worden gebruikt om te bepalen en de geüploade VHD's voor uw oplossing delen), samen met voorgestelde oplossingen.

| **Probleem** | **Foutbericht** | **Fix** | 
| --------- | ------------------- | ------- | 
| &emsp;  *Fout bij het kopiëren van afbeeldingen* |  |  |  |
| '? ' is niet gevonden in de SAS-URL | `Failure: Copying Images. Not able to download blob using provided SAS Uri.` | Update de SAS-URL met behulp van aanbevolen hulpprogramma's. |
| parameters voor "st" en "se" niet in de SAS-URL | `Failure: Copying Images. Not able to download blob using provided SAS Uri.` | Bijwerken van de SAS-URL met de juiste **begindatum** en **einddatum** waarden. | 
| "sp = rl" niet in de SAS-URL | `Failure: Copying Images. Not able to download blob using provided SAS Uri` | Bijwerken van de SAS-URL met de machtigingen die zijn ingesteld als `Read` en `List`. | 
| SAS-URL heeft spaties in VHD-naam | `Failure: Copying Images. Not able to download blob using provided SAS Uri.` | De SAS-URL als u wilt verwijderen van spaties worden bijgewerkt. |
| SAS-URL-autorisatie-fout | `Failure: Copying Images. Not able to download blob due to authorization error` | Controleren en corrigeren van de SAS-URI-indeling. Genereer een nieuwe indien nodig. |
| SAS-URL "st" en 'se'-parameters hebben geen volledige datum / tijd-specificatie | `Failure: Copying Images. Not able to download blob due to incorrect SAS URL` | SAS-URL **begindatum** en **einddatum** parameters (`st` en` se` subtekenreeksen) zijn vereist om volledige datum-/ tijdindeling, zoals `11-02-2017T00:00:00Z`. Verkorte versies zijn niet geldig. (Sommige opdrachten in de Azure CLI kunnen afgekorte waarden genereren standaard.) | 
|  |  |  |

Zie voor meer informatie, [Using shared access signatures (SAS)](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/).
