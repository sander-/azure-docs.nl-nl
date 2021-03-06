---
title: Gegevens modelleren compatibiliteitsniveau in Azure Analysis Services | Microsoft Docs
description: Inzicht in gegevens in tabelvorm model compatibiliteitsniveau.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 01/09/2019
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 31ca6deef6d81ca7beb08f6df1a15d52ef381a46
ms.sourcegitcommit: 63b996e9dc7cade181e83e13046a5006b275638d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/10/2019
ms.locfileid: "54190388"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Compatibiliteitsniveau voor tabellaire modellen van Analysis Services

*Compatibiliteitsniveau* verwijst naar de release-specifieke gedrag in de Analysis Services-engine. Wijzigingen in het compatibiliteitsniveau is doorgaans valt samen met belangrijke releases van SQL Server. Deze wijzigingen worden ook geïmplementeerd in Azure Analysis Services te onderhouden pariteit tussen beide platforms. Compatibiliteitsniveau verandert ook effect die beschikbaar zijn in uw modellen in tabelvorm. Bijvoorbeeld, hebben DirectQuery en metagegevens in tabelvorm object verschillende implementaties, afhankelijk van het compatibiliteitsniveau. Compatibiliteitsniveau is opgegeven in het project voor tabellair model in Visual Studio (SSDT). Modellen in tabelvorm in hebt gemaakt en worden geïmporteerd uit Power BI Desktop zijn op het compatibiliteitsniveau 1400 alleen.

Azure Analysis Services ondersteunt tabellaire modellen met het compatibiliteitsniveau 1200 en 1400. 

> [!NOTE]
> Power BI Desktop September 2018 en latere versies hebben een pbix-compatibiliteitsniveau van 1465. Deze compatibiliteitsniveau wordt ondersteund in Azure Analysis Services. Een Power BI Desktop-bestand importeren wordt echter niet aanbevolen voor productie-omgevingen. Zie voor meer informatie, [een Power BI Desktop-bestand importeren](analysis-services-import-pbix.md).

De meest recente versie van het compatibiliteitsniveau is 1400. Dit niveau overeenkomt met de SQL Server 2017 Analysis Services. Belangrijkste functies in het compatibiliteitsniveau 1400 zijn onder andere:

*  Nieuwe functies voor toegang tot gegevens en importeren met ondersteuning voor TOM APIs en het uitvoeren van TMSL-scripts. 
*  Gegevenstransformatie en mashup mogelijkheden om gegevens met behulp van gegevens ophalen en M-expressies.
*  Metingen ondersteuning voor detailrijen eigenschap met een DAX-expressie. Met deze eigenschap kunt clienthulpprogramma's zoals Microsoft Excel om te zoomen op gedetailleerde gegevens van een samengevoegde rapport. Wanneer gebruikers totale verkoop voor een regio en de maand bekijken, kunnen ze bijvoorbeeld de details van de bijbehorende weergeven. 
*  Beveiliging op objectniveau voor tabel- en kolomnamen, naast de gegevens daarin.
*  Verbeterde ondersteuning voor niet-aaneengesloten hiërarchieën.
*  Bewaking van prestaties en verbeteringen.
 
## <a name="set-compatibility-level"></a>Compatibiliteitsniveau van de set

 Als u een nieuw project voor tabellair model in SSDT, kunt u het compatibiliteitsniveau van de **ontwerpfunctie Tabellair model** dialoogvenster. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Als u selecteert de **dit bericht niet opnieuw weergeven** optie, alle volgende projecten wordt gebruikgemaakt van het compatibiliteitsniveau die u hebt opgegeven als de standaardwaarde. U kunt het standaardcompatibiliteitsniveau in SSDT in wijzigen **extra** > **opties**.  
  
 Als u wilt upgraden van een bestaand project voor tabellair model in SSDT, stel de **compatibiliteitsniveau** eigenschap in het model **eigenschappen** venster. Denk eraan dat, de uitbreiding van het compatibiliteitsniveau is niet ongedaan worden gemaakt.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Controleer het compatibiliteitsniveau voor een tabellaire modeldatabase in SQL Server Management Studio 

 In SSMS, met de rechtermuisknop op de databasenaam > **eigenschappen** > **compatibiliteitsniveau**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Ondersteunde compatibiliteitsniveau voor een server in SSMS controleren  

 In SSMS, met de rechtermuisknop op de servernaam > **eigenschappen** > **compatibiliteitsniveau ondersteund**.  
  
 Deze eigenschap geeft u het hoogste compatibiliteitsniveau van een database die wordt uitgevoerd op de server (exclusief Preview-versie). Het compatibiliteitsniveau van de ondersteunde kan niet worden gewijzigd.  

## <a name="next-steps"></a>Volgende stappen

  [Een model maken in Azure portal](analysis-services-create-model-portal.md)   
  [Analyseservices beheren](analysis-services-manage.md)  
