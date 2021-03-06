---
title: Bekijk de Azure Site Recovery Deployment Planner kosten van het rapport met kostenramingen voor herstel na noodgevallen van Hyper-V-machines naar Azure | Microsoft Docs
description: Dit artikel wordt beschreven hoe u controleert de kosten schatten rapport gegenereerd in de Azure Site Recovery Deployment Planner voor Hyper-V-noodherstel naar Azure.
services: site-recovery
author: mayurigupta13
manager: rochakm
ms.service: site-recovery
ms.topic: conceptual
ms.date: 11/27/2018
ms.author: mayg
ms.openlocfilehash: 03f71e4e10b65d9f295e13cdd8bc6881622c523d
ms.sourcegitcommit: 3ba9bb78e35c3c3c3c8991b64282f5001fd0a67b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/15/2019
ms.locfileid: "54320274"
---
# <a name="cost-estimation-report-by-azure-site-recovery-deployment-planner"></a>Rapport met kostenramingen van Azure Site Recovery Deployment Planner 

Het Azure Site Recovery Deployment Planner-rapport geeft een samenvatting van de kostenraming in de werkbladen [Aanbevelingen](hyper-v-deployment-planner-analyze-report.md#recommendations). Een gedetailleerde kostenanalyse vindt u in het werkblad Kostenramingen. Hier vindt u de uitgebreide kostenanalyse per VM. 

### <a name="cost-estimation-summary"></a>Samenvatting kostenramingen 
De grafiek toont de weergave Samenvatting van de geschatte totale kosten voor noodherstel (DR) voor Azure van de gekozen doelregio en de valuta die u hebt opgegeven voor het genereren van rapporten.

![Samenvatting kostenramingen](media/hyper-v-azure-deployment-planner-cost-estimation/cost-estimation-summary-h2a.png)

De samenvatting helpt u bij het begrijpen van de kosten die u moet betalen voor opslag, berekenen, netwerk en licenties wanneer u compatibele virtuele machines met Azure Site Recovery beveiligt. De kosten worden berekend op basis van compatibele virtuele machines en niet op basis van alle geprofileerde virtuele machines. 
 
U kunt de kosten maandelijks of jaarlijks weergeven. Meer informatie over [ondersteunde doelregio's](./hyper-v-deployment-planner-cost-estimation.md#supported-target-regions) en [ondersteunde valuta's](./hyper-v-deployment-planner-cost-estimation.md#supported-currencies).

**Kosten per onderdelen**: De totale kosten voor Noodherstel zijn onderverdeeld in vier onderdelen: compute, opslag, netwerk en Site Recovery-licentiekosten. De kosten worden berekend op basis van het verbruik tijdens de replicatie en de tijd van noodherstelanalyse. Rekenkosten, opslag (Premium en Standard), de ExpressRoute/VPN die is geconfigureerd tussen de on-premises site en Azure, en de Site Recovery-licentie worden gebruikt voor de berekeningen.

**Kosten per status**: De totale disaster recovery (DR) kostencategorie is gebaseerd op twee verschillende statussen: replicatie en noodherstelanalyse. 

**Replicatiekosten**: De kosten die tijdens de replicatie is gemaakt. Dit zijn de kosten voor de opslag, het netwerk en de Site Recovery-licentie. 

**Kosten voor DR-oefeningen**: De kosten die is gemaakt tijdens testfailovers. Site Recovery laat virtuele machines draaien tijdens de testfailover. De kosten voor noodherstelanalyse omvatten de berekenings- en opslagkosten van de actieve virtuele machines. 

**Azure-opslagkosten per maand/jaar**: De totale opslagkosten die worden gemaakt voor premium en standard-opslag voor replicatie en noodherstelanalyse.

## <a name="detailed-cost-analysis"></a>Gedetailleerde kostenanalyse
Azure-prijzen voor berekenen, opslag en netwerk kunnen variëren per Azure-regio. U kunt een kostenramingsrapport genereren met de meest recente Azure-prijzen op basis van uw abonnement, de aanbieding die aan uw abonnement is gekoppeld en de opgegeven Azure-doelregio in de opgegeven valuta. Het hulpprogramma gebruikt standaard de Azure-regio US - west 2 en als valuta de Amerikaanse dollar (USD). Als u een andere regio en valuta gebruikt, worden de volgende keer dat u een rapport zonder abonnements-id, aanbiedings-id, doelregio en valuta genereert, de prijzen van de laatst gebruikte doelregio en valuta voor de raming van kosten gebruikt.

In dit gedeelte worden de abonnements-id en aanbiedings-id weergegeven die u hebt gebruikt voor het genereren van rapporten. Als u deze niet hebt gebruikt, zijn de velden leeg.

Voor het hele rapport geldt dat de cellen die grijs zijn gemarkeerd, alleen-lezen zijn. Witte cellen kunnen worden gewijzigd overeenkomstig uw vereisten.

![Details kostenraming](media/hyper-v-azure-deployment-planner-cost-estimation/cost-estimation1-h2a.png)

### <a name="overall-dr-costs-by-components"></a>Totale kosten voor herstel na noodgeval per onderdeel
In de eerste sectie ziet u de totale DR-kosten per onderdelen en per statussen. 

**COMPUTE**: De kosten van IaaS-VM's die worden uitgevoerd op Azure voor DR-behoeften. Hieronder vallen virtuele machines die zijn gemaakt door Site Recovery tijdens noodherstelanalyses (testfailovers). Het gaat hierbij ook om virtuele machines die worden uitgevoerd op Azure, zoals SQL Server met AlwaysOn-beschikbaarheidsgroepen en domeincontrollers of domeinnaamservers.

**Opslag**: De kosten van Azure storage-verbruik voor DR-behoeften. Deze omvatten de kosten voor het opslagverbruik voor replicatie en tijdens DR-oefeningen.

**Netwerk**: ExpressRoute- en site-naar-site VPN-kosten voor DR-behoeften. 

**ASR-licentie**: De Site Recovery-licentiekosten voor alle compatibele virtuele machines. Als u handmatig een virtuele machine in de tabel met de gedetailleerde kostenanalyse hebt ingevoerd, worden de kosten voor de Site Recovery-licentie ook voor die VM inbegrepen.

### <a name="overall-dr-costs-by-states"></a>Totale kosten voor herstel na noodgeval per status
De totale kosten voor herstel na noodgeval zijn gebaseerd op twee verschillende statussen: replicatie en noodherstelanalyse.

**Replicatie**: De kosten in rekening gebracht op het moment van replicatie. Dit zijn de kosten voor de opslag, het netwerk en de Site Recovery-licentie. 

**DR-oefening**: De kosten in rekening gebracht op het moment van DR-oefeningen. Site Recovery laat virtuele machines draaien tijdens noodherstelanalyse. De kosten voor noodherstelanalyse omvatten berekenings- en opslagkosten voor de actieve virtuele machines.

* Totale duur van noodherstelanalyse in een jaar = aantal analyses x duur van elke analyse (dagen)
* Gemiddelde kosten van noodherstelanalyse (per maand) = totale kosten voor noodherstelanalyse / 12

### <a name="storage-cost-table"></a>Tabel met opslagkosten
Deze tabel bevat de Premium- en Standard-opslagkosten die worden gemaakt voor replicatie en noodherstelanalyses, met en zonder korting.

### <a name="site-to-azure-network"></a>Site-naar-Azure-netwerk
Selecteer de gewenste instelling overeenkomstig uw vereisten. 

**ExpressRoute**: Het hulpprogramma selecteert standaard de dichtstbijzijnde ExpressRoute-abonnement dat met de vereiste netwerkbandbreedte voor replicatie van verschillen overeenkomt. U kunt het abonnement wijzigen overeenkomstig uw vereisten.

**VPN-Gateway van het type**: Selecteer de Azure VPN-Gateway als u in uw omgeving hebt. Dit is standaard niet van toepassing.

**Doelregio**: Opgegeven Azure-regio voor herstel na Noodgevallen. De prijs die in het rapport wordt gebruikt voor het berekenen, de opslag, het netwerk en de licentie, is gebaseerd op de Azure-prijzen voor die regio. 

### <a name="vm-running-on-azure"></a>VM uitgevoerd op Azure
Mogelijk hebt u een domeincontroller of virtuele DNS-machine of SQL Server-VM met AlwaysOn-beschikbaarheidsgroepen die worden uitgevoerd op Azure voor herstel na noodgeval. U kunt het aantal virtuele machines en de grootte opgeven om de rekenkosten te bekijken als onderdeel van de totale kosten voor herstel na noodgeval. 

### <a name="apply-overall-discount-if-applicable"></a>Algemene korting toepassen, indien van toepassing
Als u een Azure-partner of -klant bent en recht hebt op korting op algemene Azure-prijzen, kunt u dit veld gebruiken. Het hulpprogramma past de korting toe (in %) op alle onderdelen.

### <a name="number-of-virtual-machines-type-and-compute-cost-per-year"></a>Aantal typen virtuele machines en de rekenkosten (per jaar)
Deze tabel toont het aantal virtuele machines (Windows en niet-Windows), en voor elk ervan de rekenkosten voor noodherstelanalyse.

### <a name="settings"></a>Instellingen 
**Beheerde schijf gebruiken**: Deze instelling geeft aan of een beheerde schijf wordt gebruikt op het moment van DR-oefeningen. De standaardinstelling is **Ja**. Als u **-UseManagedDisks** instelt op **Nee**, wordt de prijs voor onbeheerde schijf gebruikt in de kostenberekening.

**Valuta**: De valuta waarin het rapport wordt gegenereerd.

**Duur van de kosten**: U kunt alle kosten weergeven voor de maand of voor het hele jaar. 

## <a name="detailed-cost-analysis-table"></a>Tabel Gedetailleerde kostenanalyse
![Gedetailleerde kostenanalyse](media/hyper-v-azure-deployment-planner-cost-estimation/detailed-cost-analysis-h2a.png)

In de tabel wordt de verdeling van kosten weergegeven voor elke compatibele virtuele machine. U kunt deze tabel ook gebruiken voor inzicht in de geschatte kosten voor herstel na noodgeval van niet-geprofileerde virtuele machines in Azure. Hiervoor voegt u handmatig virtuele machines toe. Deze informatie is handig wanneer u Azure-kosten wilt ramen voor een nieuwe implementatie na een noodgeval, zonder gedetailleerde profilering.

Handmatig VM's toevoegen:

1. Selecteer **Rij invoegen** als u een nieuwe rij wilt invoegen tussen de rijen **Begin** en **Eind**.

1. Vul de volgende kolommen in op basis van de geschatte VM-grootte en het aantal VM's dat overeenkomt met de volgende configuratie: 

    a. **Aantal VM's**

    b. **Grootte van IaaS (uw selectie)**

    c. **Opslagtype Standard/Premium**

    d. **Totale VM-opslagruimte (GB)**

    e. **Aantal noodherstelanalyses in een jaar**

    f. **Duur van elke noodherstelanalyse (dagen)**

    g. **Type besturingssysteem**

    h. **Gegevensredundantie**

    i. **Azure Hybrid Use Benefit**

1. U kunt dezelfde waarde toepassen op alle virtuele machines in de tabel door **Op alles toepassen** te selecteren voor **Aantal noodherstelanalyses in een jaar**, **Duur van elke noodherstelanalyse (dagen)**, **Gegevensredundantie** en **Azure Hybrid Use Benefit**.

1. Selecteer **Kosten opnieuw berekenen** om de kosten bij te werken.

**VM-naam**: De naam van de virtuele machine.

**Aantal virtuele machines**: Het aantal virtuele machines die overeenkomen met de configuratie. U kunt het aantal bestaande virtuele machines bijwerken als een vergelijkbare configuratie van virtuele machines niet is geprofileerd maar wel wordt beveiligd.

**Grootte van IaaS (aanbeveling)**: De rol van VM-grootte van de compatibele VM die het hulpprogramma wordt aanbevolen. 

**Grootte van IaaS (uw selectie)**: De grootte is standaard hetzelfde als de aanbevolen grootte van de VM-rol. U kunt de rol aanpassen aan uw behoefte. De kosten voor het rekenen zijn gebaseerd op de geselecteerde grootte van de VM-rol.

**Opslagtype**: Het type opslag dat wordt gebruikt door de virtuele machine. Dit is Standard- of Premium-opslag.

**Grootte van VM-totale opslag (GB)**: De totale opslagruimte van de virtuele machine.

**Aantal DR-oefeningen in een jaar**: Het aantal keren dat die u DR-oefeningen in een jaar uitvoert. Dit is standaard vier keer per jaar. U kunt de periode voor bepaalde VM's wijzigen of de nieuwe waarde toepassen op alle VM's. Geef de nieuwe waarde op in de bovenste rij en selecteer **Toepassen op alles**. Op basis van het aantal noodherstelanalyses in een jaar en de duur van elke analyse worden de totale kosten voor noodherstelanalyse berekend. 

**De duur van elke DR-oefening (dagen)**: De duur van elke DR-oefening. Standaard is dit 7 dagen om de 90 dagen, overeenkomstig [Disaster Recovery Software Assurance Benefit](https://azure.microsoft.com/pricing/details/site-recovery). U kunt de periode voor bepaalde VM's wijzigen of een nieuwe waarde toepassen op alle VM's. Geef een nieuwe waarde op in de bovenste rij en selecteer **Toepassen op alles**. De totale kosten voor noodherstelanalyse worden berekend op basis van het aantal analyses in een jaar en de duur van elke analyse.
 
**Type besturingssysteem**: Het besturingssysteemtype (OS) van de virtuele machine. Dit is Windows of Linux. Als het type besturingssysteem Windows is, kan Azure Hybrid Use Benefit op die VM worden toegepast. 

**Gegevensredundantie**: Lokaal redundante opslag, geografisch redundante opslag of geografisch redundante opslag met leestoegang kan het zijn. De standaardinstelling is lokaal redundante opslag. U kunt het type wijzigen op basis van uw opslagaccount voor bepaalde VM's of u kunt het nieuwe type toepassen op alle VM's. Wijzig het type van de bovenste rij en selecteer **Toepassen op alles**. De opslagkosten voor replicatie worden berekend op basis van de prijs van de gegevensredundantie die u hebt geselecteerd. 

**Azure Hybrid Use Benefit**: U kunt de Azure Hybrid Use Benefit toepassen op Windows-VM's, indien van toepassing. De standaardinstelling is **Ja**. U kunt de instelling voor bepaalde VM's wijzigen of alle VM's bijwerken. Selecteer **Toepassen op alles**.

**Totaal Azure-verbruik**: De compute-, opslag- en Site Recovery-licentiekosten voor herstel na Noodgeval. Afhankelijk van wat u hebt geselecteerd, worden hier de maandelijkse of jaarlijkse kosten weergegeven.

**Replicatiekosten juiste gereedstatus**: De opslagkosten voor replicatie.

**Totale kosten DR-oefening (gemiddeld)**: De berekenings- en opslagkosten voor noodherstelanalyse.

**Kosten ASR-licentie**: De Site Recovery-licentie kosten.

## <a name="supported-target-regions"></a>Ondersteunde doelregio's
Azure Site Recovery Deployment Planner biedt een schatting van de kosten voor de volgende Azure-regio's. Als uw regio hieronder niet wordt vermeld, kunt u een van de volgende regio's gebruiken waarvan de prijzen het dichtst bij die van uw regio liggen:

eastus, eastus2, westus, centralus, northcentralus, southcentralus, northeurope, westeurope, eastasia, southeastasia, japaneast, japanwest, australiaeast, australiasoutheast, brazilsouth, southindia, centralindia, westindia, canadacentral, canadaeast, westus2, westcentralus, uksouth, ukwest, koreacentral, koreasouth 

## <a name="supported-currencies"></a>Ondersteunde valuta's
Met Azure Site Recovery Deployment Planner kunt u het kostenrapport genereren met een van de volgende valuta's.

|Valuta|Name||Valuta|Name||Valuta|Name|
|---|---|---|---|---|---|---|---|
|ARS|Argentijnse peso ($)||AUD|Australische dollar ($)||BRL|Braziliaanse real (R$)|
|CAD|Canadese dollar ($)||CHF|Zwitserse frank (chf)||DKK|Deense kroon (kr)|
|EUR|Euro (€)||GBP|Britse pond (£)||HKD|Hongkongse dollar (HK$)|
|IDR|Indonesische roepia (Rp)||INR|Indiase roepie (₹)||JPY|Japanse yen (¥)|
|KRW|Koreaanse won (₩)||MXN|Mexicaanse peso (MX$)||MYR|Maleisische ringgit (RM$)|
|NOK|Noorse kroon (kr)||NZD|Nieuw-Zeelandse dollar ($)||RUB|Russische roebel (руб)|
|SAR|Saudische riyal (SR)||SEK|Zweedse kroon (kr)||TWD|Taiwanese dollar (NT$)|
|TRY|Turkse lira (TL)||USD| Amerikaanse dollar ($)||ZAR|Zuid-Afrikaanse rand (R)|

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe u [Hyper-V-VM's naar Azure met Site Recovery](hyper-v-azure-tutorial.md) beveiligt.
