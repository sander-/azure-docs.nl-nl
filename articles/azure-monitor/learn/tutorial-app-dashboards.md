---
title: Aangepaste dashboards maken in Azure Application Insights | Microsoft Docs
description: Zelfstudie over het maken van aangepaste KPI-dashboards met behulp van Azure Application Insights.
keywords: ''
services: application-insights
author: lgayhardt
ms.author: lagayhar
ms.date: 01/11/2019
ms.service: application-insights
ms.custom: mvc
ms.topic: tutorial
manager: carmonm
ms.openlocfilehash: 5ce99e06ea1a8e72a8767367ddfd7bbb845c8400
ms.sourcegitcommit: 3ba9bb78e35c3c3c3c8991b64282f5001fd0a67b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/15/2019
ms.locfileid: "54318420"
---
# <a name="create-custom-kpi-dashboards-using-azure-application-insights"></a>Aangepaste KPI-dashboards maken met behulp van Azure Application Insights

U kunt in Azure Portal meerdere dashboards maken die elk tegels bevatten die gegevens weergeven vanuit meerdere Azure-resources in verschillende resourcegroepen en abonnementen.  U kunt verschillende grafieken en weergaven van Azure Application Insights vastmaken om aangepaste dashboards te maken die u een volledig overzicht geven van de status en prestaties van uw toepassing.  Deze zelfstudie helpt u bij het maken van een aangepast dashboard met meerdere typen gegevens en visualisaties uit Azure Application Insights.  In deze zelfstudie leert u procedures om het volgende te doen:

> [!div class="checklist"]
> * Een aangepast dashboard maken in Azure
> * Een tegel uit de Tegelgalerie toevoegen
> * Standaard metrische gegevens in Application Insights aan het dashboard toevoegen 
> * Een aangepaste grafiek met metrische gegevens uit Application Insights aan het dashboard toevoegen
> * De resultaten van een Analytics-query aan het dashboard toevoegen 



## <a name="prerequisites"></a>Vereisten

Vereisten om deze zelfstudie te voltooien:

- Implementeer een .NET-toepassing in Azure en [schakel de Application Insights-SDK](../../azure-monitor/app/asp-net.md)in. 

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.
Meld u aan bij de Azure-portal op [https://portal.azure.com](https://portal.azure.com).

## <a name="create-a-new-dashboard"></a>Een nieuw dashboard maken
Een dashboard kan resources uit meerdere toepassingen, resourcegroepen en abonnementen bevatten.  Begin deze zelfstudie met het maken van een nieuw dashboard voor uw toepassing.  

2.  Selecteer in het dashboarddeelvenster de optie **Nieuw dashboard**.

    ![Nieuw dashboard](media/tutorial-app-dashboards/1newdashboard.png)

3. Typ een naam voor het dashboard.
4. Bekijk de **Tegelgalerie** voor de verschillende tegels die u aan het dashboard kunt toevoegen.  U kunt niet alleen tegels uit de galerie toevoegen, maar ook grafieken en andere weergaven rechtstreeks vanuit Application Insights aan het dashboard vastmaken.
5. Zoek de tegel **Markdown** en sleep deze naar uw dashboard.  Met deze tegel kunt u tekst opmaken in Markdown, wat ideaal is om beschrijvende tekst toe te voegen aan uw dashboard.
6. Voeg tekst toe aan de tegeleigenschappen en wijzig het formaat van de tegel op het canvas van het dashboard.
    
    ![Tegel Markdown bewerken](media/tutorial-app-dashboards/2dashboard-text.png)

6. Klik op **Aanpassen voltooid** boven aan het scherm om de modus voor het aanpassen van tegels af te sluiten.

## <a name="add-health-overview"></a>Statusoverzicht toevoegen
Een dashboard met alleen statische tekst is niet erg interessant. Voeg daarom een tegel toe vanuit Application Insights die informatie over uw toepassing weergeeft.  U kunt Application Insights-tegels toevoegen uit de Tegelgalerie of ze rechtstreeks vanuit Application Insights-schermen vastmaken.  Hiermee kunt u grafieken en weergaven die u al kent, configureren voordat u ze aan uw dashboard vastmaakt.  Voeg eerst het standaardstatusoverzicht voor uw toepassing toe.  Hiervoor is geen configuratie vereist en er is minimale aanpassing mogelijk in het dashboard.


1. Open uw **Application Insights**-resource op het startscherm.
2. In het deelvenster **Overzicht** klikt u op het punaisepictogram om de tegel toe te voegen aan het laatste dashboard dat u hebt weergegeven.  

    ![Overzicht tijdlijn vastmaken](media/tutorial-app-dashboards/3overview.png)
 
3. In de rechterbovenhoek wordt de melding weergegeven dat de tegel is vastgemaakt aan uw dashboard. Klik op **Aan dashboard vastgemaakt** in de melding om terug te keren naar het dashboard of om het dashboarddeelvenster te gebruiken.
4. De tegel is nu aan uw dashboard toegevoegd. Selecteer **Bewerken** om de plaatsing van de tegel te wijzigen. Klik erop en sleep de tegel naar de gewenste positie. Klik vervolgens op **Aanpassen voltooid**. Uw dashboard heeft nu een tegel met nuttige informatie.

    ![Dashboard met Overzicht tijdlijn](media/tutorial-app-dashboards/4dashboard-edit.png)



## <a name="add-custom-metric-chart"></a>Aangepaste grafiek met metrische gegevens toevoegen
In het venster **Metrische gegevens** kunt u waarden die gedurende een periode door Application Insights zijn verzameld, met optionele filters en groepering in een grafiek weergeven.  Net als alle andere items in Application Insights kunt u deze grafiek aan het dashboard toevoegen.  Hiervoor is wel enige aanpassing vereist.

1. Open uw **Application Insights**-resource in het startscherm.
1. Selecteer **Metrische gegevens**.  
2. Er is al een lege grafiek gemaakt en u wordt gevraagd een waarde toe te voegen.  Voeg een waarde toe aan de grafiek en eventueel een filter en groepering.  In het volgende voorbeeld ziet u het aantal serververzoeken gegroepeerd op of ze geslaagd zijn.  Het resultaat is een actieve weergave van geslaagde en mislukte aanvragen.

    ![Waarde toevoegen](media/tutorial-app-dashboards/5sumserverrequests.png)

4. Selecteer **Vastmaken aan dashboard** aan de rechterkant. Hierdoor wordt de weergave toegevoegd aan het laatste dashboard dat u hebt gebruikt.

    ![Metrische grafiek vastmaken](media/tutorial-app-dashboards/6sumserverrequests-pin.png)

3.  In de rechterbovenhoek wordt de melding weergegeven dat de tegel is vastgemaakt aan uw dashboard. Klik op **Aan dashboard vastgemaakt** in de melding om terug te keren naar het dashboard of om de dashboardblade te gebruiken.

4. De tegel is nu aan uw dashboard toegevoegd. Selecteer **Bewerken** om de plaatsing van de tegel te wijzigen. Klik erop en sleep de tegel naar de gewenste positie. Klik vervolgens op **Aanpassen voltooid**.

    ![Dashboard met metrische gegevens](media/tutorial-app-dashboards/7dashboard-edit2.png)

## <a name="add-analytics-query"></a>Analytics-query toevoegen
Azure Application Insights Analytics biedt een uitgebreide querytaal om alle met Application Insights verzamelde gegevens te analyseren.  Net als andere weergaven en grafieken kunt u de uitvoer van een Analytics-query aan uw dashboard toevoegen.   

Aangezien Azure Application Insights Analytics een afzonderlijke service is, dient u uw dashboard te delen voordat u er een Analytics-query in kunt opnemen. Wanneer u een Azure-dashboard deelt, kunt u het publiceren als een Azure-resource en het beschikbaar maken voor andere gebruikers en resources.  

1. Klik bovenaan het dashboardscherm op **Delen**.

    ![Dashboard publiceren](media/tutorial-app-dashboards/8dashboard-share.png)

2. Behoud de **Dashboardnaam** en selecteer de **Abonnementsnaam** om het dashboard te delen.  Klik op **Publish**.  Het dashboard is nu beschikbaar voor andere services en abonnementen.  Desgewenst kunt u specifieke gebruikers opgeven die toegang tot het dashboard moeten krijgen.
1. Open uw **Application Insights**-resource in het startscherm.
2. Klik bovenaan het scherm op **Analytics** om de Analytics-portal te openen.

    ![Analytics starten](media/tutorial-app-dashboards/9analytics.png)

3. Typ de volgende query die de 10 meest aangevraagde pagina's en het bijbehorende aantal aanvragen retourneert:

    ```
    requests
    | summarize count() by name
    | sort by count_ desc
    | take 10 
    ```

4. Klik op **Uitvoeren** om de resultaten van de query te valideren.
5. Klik op het speldpictogram en selecteer de naam van het dashboard. De reden dat u bij deze optie een dashboard dient te selecteren, in tegenstelling tot de vorige stappen waarbij het laatste dashboard werd gebruikt, is dat de Analytics-console een afzonderlijke service is en moet kiezen uit alle beschikbare gedeelde dashboards.

    ![Analytics-query vastmaken](media/tutorial-app-dashboards/10query.png)

5. Voordat u teruggaat naar het dashboard, voegt u nog een query toe, maar deze keer geeft u het dashboard weer als een diagram. Zo kunt u de verschillende manieren zien waarop u een Analytics-query in een dashboard kunt weergeven.  Begin met de volgende query die de top 10 bewerkingen met de meeste uitzonderingen weergeeft.

    ```
    exceptions
    | summarize count() by operation_Name
    | sort by count_ desc
    | take 10 
    ```

6. Selecteer **Grafiek** en schakel vervolgens over naar een **Ringdiagram** om de uitvoer weer te geven.

    ![Analytics-grafiek](media/tutorial-app-dashboards/11querychart.png)

6. Klik op het speldpictogram om de grafiek aan uw dashboard vast te maken. Selecteer deze keer de link om naar uw dashboard terug te gaan.
4. De resultaten van de query's worden nu aan uw dashboard toegevoegd in de indeling die u hebt geselecteerd.  Klik en sleep elke query naar de gewenste plek en klik vervolgens op **Aanpassen voltooid**.
5. Selecteer het potloodpictogram bij elke titel om een beschrijvende titel toe te voegen.

    ![Dashboard met Analytics](media/tutorial-app-dashboards/12edit-title.png)

5. Selecteer **Delen** om de wijzigingen op uw dashboard opnieuw te publiceren. Dit bevat nu verschillende grafieken en visualisaties vanuit Application Insights.


## <a name="next-steps"></a>Volgende stappen
Nu u weet hoe u aangepaste dashboards maakt, kunt u de verdere Application Insights-documentatie bekijken, waaronder een casestudy.

> [!div class="nextstepaction"]
> [Diepe diagnostische gegevens](../../azure-monitor/app/devops.md)
