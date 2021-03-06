---
title: Hoge beschikbaarheid - Azure toegewezen HSM | Microsoft Docs
description: Voorbeeld van een hoge beschikbaarheid Azure toegewezen HSM en algemene overwegingen
services: dedicated-hsm
author: barclayn
manager: mbaldwin
ms.custom: mvc, seodec18
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 12/07/2018
ms.author: barclayn
ms.openlocfilehash: 991482d3d6be4d09b37014e5bb03708987e0f74e
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53078171"
---
# <a name="azure-dedicated-hsm-high-availability"></a>Azure toegewezen HSM hoge beschikbaarheid

Azure toegewezen HSM wordt ondersteund door de maximaal beschikbare datacenters van Microsoft. Een zeer beschikbaar datacenter is echter kwetsbaar gelokaliseerde fouten en in extreme omstandigheden, storingen in andere niveaus. Microsoft implementeert HSM-apparaten in verschillende datacenters binnen een regio om te controleren of het inrichten van meerdere apparaten niet leidt tot die apparaten delen van één rack. Nog een niveau van maximale beschikbaarheid kan worden bereikt door het koppelen van deze HSM's in de datacenters in een regio. Het is ook mogelijk op apparaten van de combinatie van verschillende regio's om de regionale failover in een herstel na noodgevallen situatie. Met deze configuratie met meerdere lagen hoge beschikbaarheid wordt een storing van het apparaat automatisch opgelost om te voorkomen dat toepassingen werken. Alle datacenters ook hebben spare apparaten en -onderdelen on-site zodat elk apparaat is mislukt in tijdig kan worden vervangen.

## <a name="high-availability-example"></a>Voorbeeld van hoge beschikbaarheid

Informatie over het configureren van HSM-apparaten voor hoge beschikbaarheid op het softwareniveau van de is in de 'Gemalto Luna netwerk HSM Administration Guide'. Dit document vindt u op de [Gemalto Customer Support Portal](https://supportportal.gemalto.com/csm/).

Het volgende diagram toont een architectuur met hoge beschikbaarheid. Maakt gebruik van meerdere apparaten in de regio en meerdere apparaten die zijn gekoppeld in een apart gebied. Deze architectuur maakt gebruik van ten minste vier HSM-apparaten en virtuele netwerkonderdelen.

![Diagram van hoge beschikbaarheid](media/high-availability/high-availability.png)

## <a name="next-steps"></a>Volgende stappen

Het is raadzaam dat alle belangrijke concepten van de service, zoals hoge beschikbaarheid en beveiliging, voor apparaatinrichting en ontwerp van toepassingen of implementatie goed wordt begrepen.
Verdere concept niveau onderwerpen:

* [Implementatie-architectuur](deployment-architecture.md)
* [Fysieke beveiliging](physical-security.md)
* [Netwerken](networking.md)
* [Ondersteuning](supportability.md)
* [Controle](monitoring.md)

Verwijzen naar de Portal voor Gemalto klanten ondersteuning voor de Administrator-handleidingen en Zie sectie 6 voor specifieke informatie over het configureren van HSM-apparaten voor hoge beschikbaarheid.
