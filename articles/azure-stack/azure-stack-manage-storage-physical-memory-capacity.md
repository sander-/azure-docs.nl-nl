---
title: Beheren van de capaciteit van het fysieke geheugen voor Azure Stack | Microsoft Docs
description: Controleren en beheren van beschikbare opslagruimte voor Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 84518E90-75E1-4037-8D4E-497EAC72AAA1
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/14/2019
ms.author: mabrigg
ms.reviewer: thoroet
ms.openlocfilehash: 928e4c7b6f7711dcad8190b6c368bd7f1df2b66c
ms.sourcegitcommit: 70471c4febc7835e643207420e515b6436235d29
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/15/2019
ms.locfileid: "54305890"
---
# <a name="manage-physical-memory-capacity-for-azure-stack"></a>Capaciteit van het fysieke geheugen voor Azure Stack beheren

*Van toepassing op: Azure Stack-geïntegreerde systemen*

Als u wilt de capaciteit van de totale beschikbare geheugen voor Azure Stack vergroten, kunt u extra geheugen toevoegen. In Azure Stack uw fysieke server wordt ook wel een *scale unit knooppunt*. Alle knooppunten van de schaal-eenheid die lid van een enkele schaaleenheid zijn moeten de dezelfde hoeveelheid geheugen hebben.

> [!note]  
> Voordat u doorgaat, raadpleegt u de documentatie van de hardwarefabrikant van uw om te controleren of een fabrikant van uw biedt ondersteuning voor de upgrade van een fysiek geheugen. Uw OEM hardware leverancier-ondersteuningscontract is mogelijk dat de leverancier van de fysieke server rack plaatsing en de firmware-update van het apparaat uitvoeren.

Het volgende stroomdiagram ziet u het algemene proces geheugen toevoegen aan elk knooppunt van de eenheid schaal.

![Geheugen op elk knooppunt van de eenheid schaal toevoegen](media/azure-stack-manage-storage-physical-capacity/process-to-add-memory-to-scale-unit.png)

## <a name="add-memory-to-an-existing-node"></a>Geheugen aan een bestaand knooppunt toevoegen
De volgende stappen bevatten een overzicht op hoog niveau van het toevoegproces-geheugen. 

> [!Warning]  
Volg deze stappen niet zonder te verwijzen naar de OEM-documentatie.

> [!Warning]  
De volledige schaaleenheid moet worden afgesloten, zoals een rolling geheugenupgrade wordt niet ondersteund.

1. Stoppen van de Azure Stack met behulp van de stappen die zijn beschreven de [starten en stoppen Azure Stack](azure-stack-start-and-stop.md) artikel.
2. De hoeveelheid geheugen op elke fysieke computer met behulp van de documentatie van de hardwarefabrikant van uw een upgrade uitvoert.
3. Start Azure Stack met behulp van de stappen in de [starten en stoppen Azure Stack](azure-stack-start-and-stop.md) artikel.

## <a name="next-steps"></a>Volgende stappen

 - Zie voor meer informatie over het beheren van storage-accounts in Azure Stack om te zoeken, herstellen en opslagcapaciteit op basis van bedrijfsbehoeften vrijmaken, [opslagaccounts in Azure Stack beheren](azure-stack-manage-storage-accounts.md).
 - Zie voor meer informatie de Azure Stack-cloud-operator bewaakt en beheert de opslagcapaciteit van hun Azure Stack-implementatie, [beheren opslagcapaciteit voor Azure Stack](azure-stack-manage-storage-shares.md). 
