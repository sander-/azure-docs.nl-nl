---
title: 'Azure Analysis Services-zelfstudie-les 12: Analyseren in Excel | Microsoft Docs'
description: In deze les wordt beschreven hoe u de analysefunctie van Excel gebruikt in de zelfstudie over Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 01/09/2019
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: e5ac04c7bd8174f823cacc67401af8a98b3d8170
ms.sourcegitcommit: 63b996e9dc7cade181e83e13046a5006b275638d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/10/2019
ms.locfileid: "54186478"
---
# <a name="analyze-in-excel"></a>Analyseren in Excel

In deze les gaat u de functie Analyse in Excel gebruiken om Microsoft Excel te openen, automatisch een verbinding tot stand te brengen met de modelwerkruimte en automatisch een draaitabel toe te voegen aan het werkblad. De functie Analyse in Excel is bedoeld om op een snelle en gemakkelijke manier de effectiviteit van uw modelontwerp te testen voordat u het model gaat implementeren. U gaat geen gegevensanalyse uitvoeren in deze les. Het doel van deze les is om u, de maker van het model, vertrouwd te maken met de hulpprogramma's die u kunt gebruiken om het modelontwerp te testen.   
  
U kunt deze les alleen voltooien als Excel is geïnstalleerd op dezelfde computer als Visual Studio.
  
Geschatte tijd voor het voltooien van deze les: **Vijf minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u de taken in deze les gaat uitvoeren, moet u de vorige les hebben voltooid: [Les 11: Rollen maken](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Bladeren met behulp van de perspectieven Default en Internet Sales  
In deze eerste taken gaat u door het model bladeren met behulp van zowel het perspectief Default, dat alle modelobjecten bevat, als het perspectief Internet Sales dat u eerder hebt gemaakt. Het perspectief Internet Sales zorgt ervoor dat het tabelobject DimCustomer wordt uitgesloten van weergave.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Bladeren met behulp van het perspectief Default:  
  
1.  Klik op het menu **Model** > **Analyze in Excel**.  
  
2.  Klik in het dialoogvenster **Analyze in Excel** op **OK**.  
  
    Excel wordt geopend met een nieuwe werkmap. Er wordt met behulp van het huidige gebruikersaccount verbinding gemaakt met de gegevensbron en het perspectief Default wordt gebruikt om te bepalen welke velden worden weergegeven. Er wordt automatisch een draaitabel toegevoegd aan het werkblad.  
  
3.  U ziet dat in**de lijst met** draaitabellen in Excel de metinggroepen **DimDate** en **FactInternetSales** worden weergegeven. De tabellen **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** en **FactInternetSales** met de bijbehorende kolommen worden ook weergegeven.  
  
4.  Sluit Excel af zonder de werkmap op te slaan.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Bladeren met behulp van het perspectief Internet Sales:  
  
1.  Klik op het menu **Model** en klik vervolgens op **Analyze in Excel**.  
  
2.  Laat in het dialoogvenster **Analyze in Excel** de optie **Current Windows User** geselecteerd en selecteer vervolgens **Internet Sales** in de vervolgkeuzelijst **Perspective** en klik op **OK**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  In Excel ziet u dat bij **Draaitabelvelden** de tabel DimCustomer niet wordt vermeld.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Sluit Excel af zonder de werkmap op te slaan.  
  
## <a name="browse-by-using-roles"></a>Bladeren met behulp van rollen  
Rollen zijn een belangrijk onderdeel van elke tabellair model. Gebruikers kunnen alleen gegevens raadplegen en analyseren met behulp van het model als ze ten minste één rol hebben. De functie Analyse in Excel is een manier om de rollen te testen die u hebt gedefinieerd.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Bladeren met behulp van de gebruikersrol Sales Manager:  
  
1.  Klik in SSDT op het menu **Model** en klik vervolgens op **Analyze in Excel**.  
  
2.  Selecteer **Role** bij **Specify the user name or role to use to connect to the model**, selecteer **Sales Manager** in de vervolgkeuzelijst en klik ten slotte op **OK**.  
  
    Excel wordt geopend met een nieuwe werkmap. Er wordt automatisch een draaitabel gemaakt. De lijst met draaitabelvelden bevat alle gegevensvelden die beschikbaar zijn in het nieuwe model.  
      
3.  Sluit Excel af zonder de werkmap op te slaan.  
  
## <a name="whats-next"></a>Volgende stappen
Ga naar de volgende les: [Les 13: Implementeer](../tutorials/aas-lesson-13-deploy.md).

  
  
  
